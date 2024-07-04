Guide to creating BTRFS with LUKS and LVM: [hadilq/NixOS-guide](https://gist.github.com/hadilq/a491ca53076f38201a8aa48a0c6afef5)

Note that the above guide doesn't use the convention of creating subvolumes with `@` to easliy distinguish them from folders.
I advise the creation of a `@swap` subvolume as well to put a swapfile:
- ```nix
    sudo btrfs subvolume create /mnt/@swap
    ```
- ```nix
    fileSystems."/swap" = {
        device = "/dev/disk/by-label/nixos";
        fsType = "btrfs";
        options = [ "subvol=@swap" ];
    };
    ```

Either use the above guide (better), or the below commands

```nix
# in case you have a LUKS on LVM setup like mine
sudo modprobe dm-cache
sudo vgchange -ay VG
sudo cryptsetup open /dev/VG/cryptroot cryptroot
sudo cryptsetup open /dev/VG/cryptswap cryptswap

# mkfs.btrfs -L nixos -f /dev/mapper/cryptroot # reformats partition with nixos label
# Mount and create subvolumes
sudo mount /dev/mapper/cryptroot /mnt
sudo btrfs subvolume create /mnt/@
sudo btrfs subvolume create /mnt/@nix
sudo btrfs subvolume create /mnt/@persistent
sudo btrfs subvolume list -p /mnt # to list
sudo umount /mnt # unmount to mount with subvolumes:
sudo mount -o subvol=@ /dev/mapper/cryptroot /mnt
sudo mkdir -p /mnt/nix /mnt/persistent
sudo mount -o subvol=@nix /dev/mapper/cryptroot /mnt/nix
sudo mount -o subvol=@persistent /dev/mapper/cryptroot /mnt/persistent
sudo nixos-generate-config --root /mnt
NIXPKGS_ALLOW_UNFREE=1 nix-shell -p vscode --run "sudo code /mnt/etc/nixos/ --no-sandbox --user-data-dir /tmp"
sudo nixos-install

```

## Impermanence

For setting up impermanance check out [this video](https://www.youtube.com/watch?v=YPKwkWtK7l0).
If using systemd to boot, instead of `boot.initrd.postDeviceCommands` you'll need to use a systemd service:

```nix
boot.initrd.systemd.services.clean-old-roots = {
requires = ["dev-mapper-cryptroot.device"];
after = ["dev-mapper-cryptroot.device"];
before = [
    "sysroot.mount"
];
wantedBy = ["initrd.target"];
script = ''
    mkdir /btrfs_tmp
    mount /dev/disk/by-label/nixos /btrfs_tmp
    if [[ -e /btrfs_tmp/root ]]; then
        mkdir -p /btrfs_tmp/old_roots
        timestamp=$(date --date="@$(stat -c %Y /btrfs_tmp/root)" "+%Y-%m-%-d_%H:%M:%S")
        mv /btrfs_tmp/root "/btrfs_tmp/old_roots/$timestamp"
    fi

    delete_subvolume_recursively() {
        IFS=$'\n'
        for i in $(btrfs subvolume list -o "$1" | cut -f 9- -d ' '); do
            delete_subvolume_recursively "/btrfs_tmp/$i"
        done
        btrfs subvolume delete "$1"
    }

    for i in $(find /btrfs_tmp/old_roots/ -maxdepth 1 -mtime +30); do
        delete_subvolume_recursively "$i"
        echo "deleted subvolume $i"
    done

    btrfs subvolume create /btrfs_tmp/root
    umount /btrfs_tmp
'';
};
```

Or devide it in two services:

```nix
boot.initrd.systemd.services.clean-old-roots = {
requires = ["dev-mapper-cryptroot.device"];
after = ["dev-mapper-cryptroot.device"];
before = [
    "sysroot.mount"
];
wantedBy = ["initrd.target"];
script = ''
    mkdir /btrfs_tmp
    mount /dev/disk/by-label/nixos /btrfs_tmp

    delete_subvolume_recursively() {
        IFS=$'\n'
        for i in $(btrfs subvolume list -o "$1" | cut -f 9- -d ' '); do
            delete_subvolume_recursively "/btrfs_tmp/$i"
        done
        btrfs subvolume delete "$1"
    }

    for i in $(find /btrfs_tmp/old_roots/ -maxdepth 1 -mtime +30); do
        delete_subvolume_recursively "$i"
        echo "deleted subvolume $i"
    done

    umount /btrfs_tmp
'';
};
```

```nix
boot.initrd.systemd.services.wipe-my-fs = {
requires = ["dev-mapper-cryptroot.device"];
after = ["dev-mapper-cryptroot.device" "clean-old-roots.service"];
before = [
    "sysroot.mount"
];
wantedBy = ["initrd.target"];
script = ''
    mkdir /btrfs_tmp
    mount /dev/disk/by-label/nixos /btrfs_tmp
    if [[ -e /btrfs_tmp/root ]]; then
        mkdir -p /btrfs_tmp/old_roots
        timestamp=$(date --date="@$(stat -c %Y /btrfs_tmp/root)" "+%Y-%m-%-d_%H:%M:%S")
        mv /btrfs_tmp/root "/btrfs_tmp/old_roots/$timestamp"
    fi

    btrfs subvolume create /btrfs_tmp/root
    umount /btrfs_tmp
'';
};
```

## Initial configuration to boot with subvolumes

### configuration.nix

```nix
# Edit this configuration file to define what should be installed on
# your system. Help is available in the configuration.nix(5) man page, on
# https://search.nixos.org/options and in the NixOS manual (`nixos-help`).

{ config, lib, pkgs, ... }:

{
  imports =
    [ # Include the results of the hardware scan.
      ./hardware-configuration.nix
    ];

  users.users.yeshey = {
	isNormalUser = true;
	extraGroups = ["wheel" "networkmanager"];
    password = "123456789";
    };

  boot.initrd.kernelModules = [ "dm-cache" "dm-cache-smq" "dm-cache-mq" "dm-cache-cleaner" ];
  boot.kernelModules = [ 
    "dm_mod" # For LVM
    "dm-cache" "dm-cache-smq" "dm-writecache" # for cache
    "dm_crypt" # for encryption
  ];

  # Use the systemd-boot EFI boot loader.
  boot.loader.systemd-boot = {
    enable = true;
    configurationLimit = 10; # You can leave it null for no limit, but it is not recommended, as it can fill your boot partition.
  };
  boot.loader.efi.canTouchEfiVariables = true;
  boot.loader.efi.efiSysMountPoint = "/boot";

  boot.initrd.systemd.enable = true;
  boot.initrd.systemd.enableTpm2 = true;
  boot.initrd.systemd.emergencyAccess = true;

  boot.kernelPackages = pkgs.linuxPackages_latest;
  boot.supportedFilesystems = [ "btrfs" ];
  hardware.enableAllFirmware = true;
  nixpkgs.config.allowUnfree = true;

  environment.systemPackages = with pkgs; [
    wget vim git mkpasswd
    firefox
  ];

  # networking.hostName = "nixos"; # Define your hostname.
  # Pick only one of the below networking options.
  # networking.wireless.enable = true;  # Enables wireless support via wpa_supplicant.
  # networking.networkmanager.enable = true;  # Easiest to use and most distros use this by default.

  # Set your time zone.
  # time.timeZone = "Europe/Amsterdam";

  # Configure network proxy if necessary
  # networking.proxy.default = "http://user:password@proxy:port/";
  # networking.proxy.noProxy = "127.0.0.1,localhost,internal.domain";

  # Select internationalisation properties.
  # i18n.defaultLocale = "en_US.UTF-8";
  # console = {
  #   font = "Lat2-Terminus16";
  #   keyMap = "us";
  #   useXkbConfig = true; # use xkb.options in tty.
  # };

  # Enable the X11 windowing system.
  services.xserver.enable = true;


  # Enable the GNOME Desktop Environment.
  services.xserver.displayManager.gdm.enable = true;
  services.xserver.desktopManager.gnome.enable = true;
  

  # Configure keymap in X11
  # services.xserver.xkb.layout = "us";
  # services.xserver.xkb.options = "eurosign:e,caps:escape";

  # Enable CUPS to print documents.
  # services.printing.enable = true;

  # Enable sound.
  # hardware.pulseaudio.enable = true;
  # OR
  # services.pipewire = {
  #   enable = true;
  #   pulse.enable = true;
  # };

  # Enable touchpad support (enabled default in most desktopManager).
  # services.libinput.enable = true;

  # Define a user account. Don't forget to set a password with ‘passwd’.
  # users.users.alice = {
  #   isNormalUser = true;
  #   extraGroups = [ "wheel" ]; # Enable ‘sudo’ for the user.
  #   packages = with pkgs; [
  #     firefox
  #     tree
  #   ];
  # };

  # List packages installed in system profile. To search, run:
  # $ nix search wget
  # environment.systemPackages = with pkgs; [
  #   vim # Do not forget to add an editor to edit configuration.nix! The Nano editor is also installed by default.
  #   wget
  # ];

  # Some programs need SUID wrappers, can be configured further or are
  # started in user sessions.
  # programs.mtr.enable = true;
  # programs.gnupg.agent = {
  #   enable = true;
  #   enableSSHSupport = true;
  # };

  # List services that you want to enable:

  # Enable the OpenSSH daemon.
  # services.openssh.enable = true;

  # Open ports in the firewall.
  # networking.firewall.allowedTCPPorts = [ ... ];
  # networking.firewall.allowedUDPPorts = [ ... ];
  # Or disable the firewall altogether.
  # networking.firewall.enable = false;

  # Copy the NixOS configuration file and link it from the resulting system
  # (/run/current-system/configuration.nix). This is useful in case you
  # accidentally delete configuration.nix.
  # system.copySystemConfiguration = true;

  # This option defines the first version of NixOS you have installed on this particular machine,
  # and is used to maintain compatibility with application data (e.g. databases) created on older NixOS versions.
  #
  # Most users should NEVER change this value after the initial install, for any reason,
  # even if you've upgraded your system to a new NixOS release.
  #
  # This value does NOT affect the Nixpkgs version your packages and OS are pulled from,
  # so changing it will NOT upgrade your system - see https://nixos.org/manual/nixos/stable/#sec-upgrading for how
  # to actually do that.
  #
  # This value being lower than the current NixOS release does NOT mean your system is
  # out of date, out of support, or vulnerable.
  #
  # Do NOT change this value unless you have manually inspected all the changes it would make to your configuration,
  # and migrated your data accordingly.
  #
  # For more information, see `man configuration.nix` or https://nixos.org/manual/nixos/stable/options#opt-system.stateVersion .
  system.stateVersion = "24.05"; # Did you read the comment?

}
```

### hardware-configuration.nix

```nix
# Do not modify this file!  It was generated by ‘nixos-generate-config’
# and may be overwritten by future invocations.  Please make changes
# to /etc/nixos/configuration.nix instead.
{ config, lib, pkgs, modulesPath, ... }:

{
  imports =
    [ (modulesPath + "/installer/scan/not-detected.nix")
    ];

  boot.initrd.availableKernelModules = [ "xhci_pci" "ahci" "nvme" "usbhid" "usb_storage" "sd_mod" "sr_mod" "rtsx_pci_sdmmc" "asus_wmi" "hid_asus" "nouveau" ];
  boot.initrd.kernelModules = [ "dm-snapshot" ];
  boot.kernelModules = [ "kvm-intel" ];
  boot.extraModulePackages = [ ];

  fileSystems."/" =
    { #device = "/dev/disk/by-uuid/6fcc0524-bd74-44b9-ac07-c91d2ffe6121";
      device = "/dev/disk/by-label/nixos";
      fsType = "btrfs";
      options = [ "subvol=root" "compress-force=zstd:3" ];
    };

  boot.initrd.luks.devices.cryptroot = {
    device = "/dev/VG/cryptroot";
  };
  boot.initrd.luks.devices.cryptswap = {
    device = "/dev/VG/cryptswap";
  };

  #boot.initrd.luks.devices."cryptroot".device = "/dev/disk/by-uuid/306b4e06-70e4-45ff-bdee-df87c5c5a405";

  fileSystems."/nix" =
    { #device = "/dev/disk/by-uuid/6fcc0524-bd74-44b9-ac07-c91d2ffe6121";
      device = "/dev/disk/by-label/nixos";
      fsType = "btrfs";
      options = [ "subvol=nix" "compress-force=zstd:3" ];
    };

  fileSystems."/persist" =
    { #device = "/dev/disk/by-uuid/6fcc0524-bd74-44b9-ac07-c91d2ffe6121";
      device = "/dev/disk/by-label/nixos";
      fsType = "btrfs";
      options = [ "subvol=persist" "compress-force=zstd:3" ];
    };

  fileSystems."/boot" =
    { device = "/dev/disk/by-uuid/84A9-3C95";
      fsType = "vfat";
      options = [ "fmask=0022" "dmask=0022" ];
    };

  swapDevices = [ ];

  # Enables DHCP on each ethernet and wireless interface. In case of scripted networking
  # (the default) this is the recommended approach. When using systemd-networkd it's
  # still possible to use this option, but it's recommended to use it in conjunction
  # with explicit per-interface declarations with `networking.interfaces.<interface>.useDHCP`.
  networking.useDHCP = lib.mkDefault true;
  # networking.interfaces.wlp0s20f3.useDHCP = lib.mkDefault true;

  nixpkgs.hostPlatform = lib.mkDefault "x86_64-linux";
  hardware.cpu.intel.updateMicrocode = lib.mkDefault config.hardware.enableRedistributableFirmware;
}
```