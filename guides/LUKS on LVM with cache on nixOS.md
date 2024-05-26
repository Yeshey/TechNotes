# Windows Dual boot, LUKS on LVM with LVM cache, btrfs, nixOS

- To set up your NixOS system with LUKS encryption on LVM, using `btrfs` for the root logical volume, and configuring a cache for faster operations, you will need to follow several steps. Here is how you can achieve this using your provided partitions (`/dev/nvme0n1p5` for SSD and `/dev/sdb1` for microSD).
- The LVM cache is going to steal space from your ssd only for cache, so I won't use the full ssd 
 > [What you can do in recent-ish LVM versions is create one “origin” LV on the HDD and one “cache pool” LV on the SSD, and then combine it into a single “cache” LV. It has the same size as the “origin” LV (i.  e., you only get as much space as is on the HDD), but frequently used blocks and metadata are cached on the SSD to improve performance.](https://unix.stackexchange.com/questions/120242/using-lvm-with-ssd-and-sata-drives#:~:text=What%20you%20can,to%20improve%20performance.)
### Overview of Steps:
1. Initialize physical volumes.
2. Create a volume group.
3. Create logical volumes for root and swap.
4. Set up encryption with LUKS.
5. Format the logical volumes.
6. Set up caching.
7. Configure NixOS to recognize and mount these volumes.

Based on:
- [ArchWiki guide](https://wiki.archlinux.org/title/Dm-crypt/Encrypting_an_entire_system#LUKSonLVM:~:text=parameters%20for%20details.-,LUKS%20on%20LVM,-To%20use%20encryption)
- [gabrieljcs' lvm cache on fedora guide](https://gist.github.com/gabrieljcs/805c183753046dcc6131)
- [LVM cache options explenation](https://blog.delouw.ch/2020/01/29/using-lvm-cache-for-storage-tiering/)

### Step-by-Step Guide:
#### 1. Initialize Physical Volumes:

```sh
sudo pvcreate /dev/nvme0n1p5
sudo pvcreate /dev/sdb1
```


#### 2. Create Volume Group:

```sh
sudo vgcreate VG /dev/nvme0n1p5 /dev/sdb1
```


#### 3. Create Logical Volumes:

```sh
sudo lvcreate -L 5G -n cryptswap VG /dev/nvme0n1p5
sudo lvcreate -L YMB -n meta VG /dev/nvme0n1p5 # for cache metadata
sudo lvcreate -L 15GB -n cache VG /dev/nvme0n1p5
sudo lvcreate -l 100%FREE -n cryptroot VG # uses rest of VG space, you could add /dev/sdb1 to the end for it to use the space only in that PV
```
Where Y is 1000 times smaller than the cache data LV, with a minimum of 8MB. e.g. if you have a 32 GB SSD, `Y = 32MB`.


#### 4. Set Up LUKS Encryption:

```sh
sudo cryptsetup luksFormat /dev/VG/cryptswap
sudo cryptsetup luksFormat /dev/VG/cryptroot

sudo cryptsetup open /dev/VG/cryptswap cryptswap
sudo cryptsetup open /dev/VG/cryptroot cryptroot
```

To decrypt the volumes later through a bootable USB, you might also have to make sure your logical volumes are active before running `cryptsetup open`:
```sh
sudo vgchange -ay VG
```

#### 5. Set Up Caching:
1. Create the cache pool LV, you might need to run `sudo modprobe dm-cache` first.

```sh
sudo lvconvert --type cache-pool --cachemode writeback --poolmetadata VG/meta VG/cache
```
This combines the cache data and metadata into a cache pool that uses writeback mode. Ommitting defaults to writethrough, which stores data in the cache and on the origin LV.

1. Create the cache:

```sh
sudo lvconvert --type cache --cachepool VG/cache VG/cryptroot
```
If you get an error like
> Volume group "VG" has insufficient free space (0 extents): 4 required.  

You can decrease the size of the root LV by 10 extents for example with `sudo lvreduce -l -10 /dev/VG/cryptroot` and you can also increase it afterwards with `sudo lvextend -l +100%FREE /dev/VG/cryptroot`. You will need to resize everything, including the LV, the luks container and the filesystem, refer to [resize](#resize) for help.  
The pool is then converted into a cache for the root partition.

#### 6. Check LV are created and using all LV space:

```sh
sudo lvs -o +vg_free
```
Should have zeros in the right like so:
| LV        | VG        | Attr       | LSize  | ... | VFree    |
|-----------|-----------|------------|--------|-----|----------|
| cryptroot | VG        | -wi-ao---- | 194.86g| ... | 0        |
| cryptswap | VG        | -wi-ao---- | 5.00g  | ... | 0        |
| meta      | VG        | -wi-a----- | 48.00m | ... | 0        |su

#### 7. Format the Logical Volumes:

```sh
sudo mkswap -L swap /dev/mapper/cryptswap
sudo mkfs.btrfs -L nixos /dev/mapper/cryptroot
```
You will need the labels below.

#### 8. Installation

Followed [this](https://fictionbecomesfact.com/nixos-installation-luks) guide.

```sh
sudo mount /dev/disk/by-label/nixos /mnt
sudo mkdir -p /mnt/boot
sudo mount /dev/disk/by-label/SYSTEM /mnt/boot # gert the label of the fat32 partition from gparted
sudo swapon /dev/mapper/cryptswap
```
Check results and UUIDs with `lsblk --fs`.
```sh
sudo nixos-generate-config --root /mnt
sudo nano /mnt/etc/nixos/configuration.nix
```
Some configuration you will likely [need to change](https://fictionbecomesfact.com/nixos-installation-luks#installing)

#### 7. Configure NixOS:

Add the following configurations to your NixOS configuration file (`/etc/nixos/configuration.nix`):

```nix
{ config, pkgs, ... }:

{
  boot.loader.systemd-boot = {
    enable = true;
    configurationLimit = 5; # You can leave it null for no limit, but it is not recommended, as it can fill your boot partition.
  };
  boot.loader.efi.canTouchEfiVariables = true;
  boot.loader.efi.efiSysMountPoint = "/boot/efi";

  fileSystems."/boot/efi" =
    { device = "/dev/disk/by-uuid/84A9-3C95";
      fsType = "vfat";
      #options = [ "fmask=0022" "dmask=0022" ]; 
      # ⚠️ fix the security issue ⚠️
      # https://github.com/NixOS/nixpkgs/issues/279362#issuecomment-1883970541
      options = [ "uid=0" "gid=0" "fmask=0077" "dmask=0077" ];
    };

  boot.initrd.preLVMCommands = lib.mkOrder 400 "sleep 3"; # in my case I had to wait a bit to let my hardware pick up on my microSD
  boot.initrd.luks.devices = {
    # Will already attempt to use the same password to decrypt both
    "cryptroot" = {
      device = "/dev/VG/cryptroot";
      allowDiscards = true; # for ssd primary?
      preLVM = false; # informs that its LUKS on LVM and not LVM on LUKS
    };
    "cryptswap" = {
      device = "/dev/VG/cryptswap";
      allowDiscards = true; # for ssd primary?
      preLVM = false; # informs that its LUKS on LVM and not LVM on LUKS
    };
  }; 

  fileSystems."/" =
    { #device = "/dev/disk/by-uuid/6e60cc35-882f-45bf-8402-719a14a74a74";
      device = "/dev/mapper/cryptroot";
      fsType = "btrfs";
      options = [ "compress=zstd" ];
    };
  swapDevices =
    [ 
      { device = "/dev/mapper/cryptswap"; }
    ];

  boot.initrd.lvm.enable = true;
  boot.kernelModules = [ 
    "dm_mod" # For LVM
    "dm-cache" "dm-cache-smq" "dm-writecache" # for cache
    "dm_crypt" # for encryption
  ];

  boot.supportedFilesystems = [ "btrfs" ]; # can read btrfs drives now
}
```

For integration with tpm and possibly passing the password to the loginm, you can also do this with `boot.initrd.systemd.enable`:
```nix
  boot.loader.systemd-boot = {
    enable = true;
    configurationLimit = 10; # You can leave it null for no limit, but it is not recommended, as it can fill your boot partition.
  };
  boot.loader.efi.canTouchEfiVariables = true;
  boot.loader.efi.efiSysMountPoint = "/boot/efi";

  boot.initrd.systemd.enable = true;
  #boot.initrd.systemd.emergencyAccess = true; # might need for debugging
  boot.initrd.luks.devices.cryptroot = {
    device = "/dev/VG/cryptroot";
  };
  boot.initrd.luks.devices.cryptswap = {
    device = "/dev/VG/cryptswap";
  };

  # make tpm work maybe?
  #boot.initrd.systemd.enableTpm2 = true;
  #security.tpm2.enable = true;
  #security.tpm2.pkcs11.enable = true;  # expose /run/current-system/sw/lib/libtpm2_pkcs11.so
  #security.tpm2.tctiEnvironment.enable = true;  # TPM2TOOLS_TCTI and TPM2_PKCS11_TCTI env variables

  fileSystems."/boot/efi" =
    { device = "/dev/disk/by-uuid/84A9-3C95";
      fsType = "vfat";
      #options = [ "fmask=0022" "dmask=0022" ]; 
      # ⚠️ fix the security issue ⚠️
      # https://github.com/NixOS/nixpkgs/issues/279362#issuecomment-1883970541
      options = [ "uid=0" "gid=0" "fmask=0077" "dmask=0077" ];
    };

  fileSystems."/" =
    { #device = "/dev/disk/by-uuid/6e60cc35-882f-45bf-8402-719a14a74a74"; # or
      device = "/dev/disk/by-label/nixos";
      fsType = "btrfs";
      options = [ "compress=zstd" ];
    };
  swapDevices =
    [ 
      { #device = "/dev/disk/by-uuid/aea2ed46-641d-4fe5-8551-880c8a8a034f"; # or 
        device = "/dev/disk/by-label/swap";
      }
    ];
```

### Troubleshoot

If you are stuck in stage 1 boot, you can add this to your config:
```nix
boot.kernelParams = [ "boot.shell_on_fail" ]; # from https://discourse.nixos.org/t/unable-to-boot-from-a-usb-device-with-a-luks-partition/26516/2
```
It will allow you to drop into a shell, you can then use `blkid` to see the available UUIDs, CTRL + ALT + DELETE to reboot

## Resize

ChatGPT: 
- When resizing a logical volume (LV) that is encrypted with LUKS, you need to ensure that both the logical volume and the encrypted container are resized properly. Here’s how you can safely resize an LV and adjust the LUKS container accordingly:
### Steps to Resize an Encrypted Logical Volume 
1. **Resize the Logical Volume (LV)** :
- First, ensure that the logical volume is not in use. If it’s mounted, you’ll need to unmount it. 
- Use the `lvresize` command to resize the logical volume. 
2. **Resize the LUKS Container** :
- After resizing the LV, you must also resize the LUKS container to match the new size of the LV. 
3. **Resize the Filesystem** :
- Finally, resize the filesystem within the LUKS container to make use of the new space.
### Detailed Procedure
#### 1. Unmount the Filesystem (if mounted):

```sh
sudo umount /mnt  # Replace /mnt with your mount point
```


#### 2. Close the LUKS Container (if open):

```sh
sudo cryptsetup close /dev/mapper/cryptroot  # Replace cryptroot with your LUKS mapping name
```


#### 3. Resize the Logical Volume:

Resize the LV to the desired size. For example, to increase the size to 40G:

```sh
sudo lvresize -L 40G /dev/VG/cryptroot  # Replace VG with your volume group name and cryptroot with your LV name
```



Alternatively, to extend the LV to use all available free space:

```sh
sudo lvresize -l +100%FREE /dev/VG/cryptroot  # Replace VG with your volume group name and cryptroot with your LV name
```


#### 4. Open the LUKS Container:

```sh
sudo cryptsetup open /dev/VG/cryptroot cryptroot  # Replace VG with your volume group name and cryptroot with your LV name
```


#### 5. Resize the LUKS Container:

Use the `cryptsetup` command to resize the LUKS container to match the new size of the LV:

```sh
sudo cryptsetup resize cryptroot  # Replace cryptroot with your LUKS mapping name
```


#### 6. Resize the Filesystem:

Finally, resize the filesystem inside the LUKS container. For a `btrfs` filesystem, you would use:

```sh
sudo mount /dev/mapper/cryptroot /mnt
sudo btrfs filesystem resize max /mnt
df -h /mnt # to check it worked
sudo umount /mnt
```



For an `ext4` filesystem, you would use:

```sh
sudo resize2fs /dev/mapper/cryptroot  # Replace /dev/mapper/cryptroot with your mapped device
```


### Example Commands in Sequence

```sh
# Unmount the filesystem
sudo umount /mnt  # Replace /mnt with your mount point

# Close the LUKS container
sudo cryptsetup close /dev/mapper/cryptroot  # Replace cryptroot with your LUKS mapping name

# Resize the logical volume
sudo lvresize -L 40G /dev/VG/cryptroot  # Replace VG with your volume group name and cryptroot with your LV name

# Open the LUKS container
sudo cryptsetup open /dev/VG/cryptroot cryptroot  # Replace VG with your volume group name and cryptroot with your LV name

# Resize the LUKS container
sudo cryptsetup resize cryptroot  # Replace cryptroot with your LUKS mapping name

# Resize the filesystem (example for btrfs)
sudo btrfs filesystem resize max /dev/mapper/cryptroot  # Replace /dev/mapper/cryptroot with your mapped device

# Mount the filesystem again
sudo mount /dev/mapper/cryptroot /mnt  # Replace /dev/mapper/cryptroot and /mnt with your actual device and mount point
```


### Important Notes
- Always ensure you have a complete backup of your data before performing resize operations.
- Be careful with each command, especially when dealing with partitions and filesystems, to avoid data loss.
- If you are decreasing the size of the logical volume, make sure to shrink the filesystem first, then the LUKS container, and finally the logical volume.
