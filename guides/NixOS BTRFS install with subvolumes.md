```nix
# in case you have a LUKS on LVM setup like mine
sudo modprobe dm-cache
sudo vgchange -ay VG
sudo cryptsetup open /dev/VG/cryptroot cryptroot
sudo cryptsetup open /dev/VG/cryptswap cryptswap

# mkfs.btrfs -L nixos -f /dev/mapper/cryptroot # reformats partition
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
