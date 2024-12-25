```sh
nix-shell -p bcachefs-tools
sudo mount -t bcachefs /dev/nvme0n1p5:/dev/sdb3 /mnt/
sudo mkdir -p /mnt/boot
sudo mount /dev/nvme0n1p1 /mnt/boot
sudo nixos-generate-config --root /mnt
NIXPKGS_ALLOW_UNFREE=1 nix-shell -p vscode --run "sudo code /mnt/etc/nixos --no-sandbox --user-data-dir /tmp"
sudo nixos-install --root /mnt
```
