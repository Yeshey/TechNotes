# Windows Dual boot, LUKS on LVM with LVM cache: LV across SSD and HDD/MicroSD, btrfs, nixOS

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
sudo lvcreate -l 15GB -n cache VG /dev/nvme0n1p5
sudo lvcreate -l 100%FREE -n cryptroot VG # uses rest of VG space, you could add /dev/sdb1 to the end for it to use the space only in that PV
```
Where Y is 1000 times smaller than the cache data LV, with a minimum of 8MB. e.g. if you have a 32 GB SSD, `Y = 32MB`.

#### 6. Set Up Caching:
1. Create the cache pool LV:, you might need to run `sudo modprobe dm-cache` first.

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

You can decrease the size of the root LV by 10 extents for example with `sudo lvreduce -l -10 /dev/VG/cryptroot` and you can also increase it afterwards with `sudo lvextend -l +100%FREE /dev/VG/cryptroot`.  
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

#### 4. Set Up LUKS Encryption:

Not encrypting `meta` LV, maybe I should?

```sh
sudo cryptsetup luksFormat /dev/VG/cryptswap
sudo cryptsetup luksFormat /dev/VG/cryptroot

sudo cryptsetup open /dev/VG/cryptswap cryptswap
sudo cryptsetup open /dev/VG/cryptroot cryptroot
```

#### 5. Format the Logical Volumes:

```sh
sudo mkswap /dev/mapper/cryptswap
sudo mkfs.btrfs /dev/mapper/cryptroot
```


#### 7. Configure NixOS:

Add the following configurations to your NixOS configuration file (`/etc/nixos/configuration.nix`):

```nix
{ config, pkgs, ... }:

{
  boot.initrd.luks.devices = {
    cryptroot = {
      device = "/dev/VG/cryptroot";
      preLVM = true;
    };
    cryptswap = {
      device = "/dev/VG/cryptswap";
      preLVM = true;
    };
  };

  boot.initrd.lvm.enable = true;
  boot.kernelModules = [ "dm_mod" "dm_crypt" ];

  fileSystems."/" = {
    device = "/dev/mapper/cryptroot";
    fsType = "btrfs";
  };

  swapDevices = [
    {
      device = "/dev/mapper/cryptswap";
    }
  ];

  boot.supportedFilesystems = [ "btrfs" ];
}
```


### Explanation: 
1. **Physical Volumes and Volume Group** : 
- `pvcreate` initializes the physical volumes on `/dev/nvme0n1p5` and `/dev/sdb1`. 
- `vgcreate` creates a volume group `VG` combining these physical volumes. 
2. **Logical Volumes** : 
- `lvcreate` creates a 6GB logical volume for swap on the SSD (`/dev/nvme0n1p5`) and uses the remaining space for the root filesystem on the microSD (`/dev/sdb1`). 
3. **LUKS Encryption** : 
- `cryptsetup luksFormat` sets up LUKS encryption on both logical volumes. 
- `cryptsetup open` opens these encrypted volumes, making them available as `/dev/mapper/cryptswap` and `/dev/mapper/cryptroot`. 
4. **Formatting** : 
- `mkswap` initializes the swap area. 
- `mkfs.btrfs` formats the root logical volume with `btrfs`. 
5. **Caching** : 
- `lvcreate` commands create cache metadata and cache data logical volumes on the SSD. 
- `lvconvert` combines these into a cache pool and then converts the root logical volume to use this cache pool. 
6. **NixOS Configuration** : 
- Configurations are added to `/etc/nixos/configuration.nix` to ensure NixOS recognizes and properly mounts the encrypted and cached volumes at boot.

After making these changes, run `sudo nixos-rebuild switch` to apply the configurations.
### Final Notes:
- Make sure you replace any placeholder values with the actual UUIDs or device names as needed.
- You may need to adjust the sizes and configurations based on your specific setup and requirements.
- Ensure you have backups and have tested the setup in a safe environment to avoid data loss.