1. **Boot from the USB:** 
Insert the NixOS live USB and boot from it. Select the option to start NixOS from the live environment.
 
2. **Activate LVM and LUKS:** 
Load the necessary kernel modules and activate the LVM and LUKS devices.

```bash
sudo modprobe dm-cache
sudo vgchange -ay VG
sudo cryptsetup open /dev/VG/cryptroot cryptroot
sudo cryptsetup open /dev/VG/cryptswap cryptswap
```
 
3. **Mount BTRFS Subvolumes:** 
Mount the root BTRFS subvolume and create the necessary directories.

```bash
sudo mount -o subvol=root /dev/mapper/cryptroot /mnt
sudo mkdir -p /mnt/nix /mnt/persist /mnt/boot
sudo mount -o subvol=nix /dev/mapper/cryptroot /mnt/nix
sudo mount -o subvol=persist /dev/mapper/cryptroot /mnt/persist
sudo mount /dev/disk/by-uuid/84A9-3C95 /mnt/boot
```
 
4. **Generate config files** 
BEcause rebuilding from `nixos enter` gives errors, we will do a nixos-install, it will keep all the files and boot entries.

```bash
sudo nixos-enter
```
 
5. **Reinstall the Configuration with Bootloader:** 
Inside the chroot environment, run the following command to reinstall NixOS with the bootloader:

```bash
sudo nixos-generate-config --root /mnt
```
 
6. **Edit the hardware configuration with you boot and hardware configuration in your flake for the surface** 

```bash
sudo nano /mnt/etc/nixos/hardware-configuration.nix
```
 
7. **Install and reboot:** 

```bash
sudo nixos-install --root /mnt --no-root-password
reboot
```
 
