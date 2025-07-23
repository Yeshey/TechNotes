<h1> TechNotes

<h2> Table Of Contents

- [1. OSs](#1-oss)
  - [1.1. **Linux** (Manjaro)](#11-linux-manjaro)
    - [1.1.1. Autostart Tasks](#111-autostart-tasks)
    - [1.1.2. PDFs](#112-pdfs)
      - [1.1.2.1. Unite](#1121-unite)
      - [1.1.2.2. OCR](#1122-ocr)
      - [1.1.2.3. Compress](#1123-compress)
    - [1.1.3. Latte Dock](#113-latte-dock)
    - [1.1.4. Notifications](#114-notifications)
      - [1.1.4.1. Fix notifications error in latte dock](#1141-fix-notifications-error-in-latte-dock)
      - [1.1.4.2. Notification badges in electron apps (like discord)](#1142-notification-badges-in-electron-apps-like-discord)
      - [1.1.4.3. Send linux OS notifications through terminal/console/cli](#1143-send-linux-os-notifications-through-terminalconsolecli)
    - [1.1.5. Button To Boot into Windows in a dual boot](#115-button-to-boot-into-windows-in-a-dual-boot)
    - [1.1.6. Ohmy - zsh (instead of bash)](#116-ohmy---zsh-instead-of-bash)
    - [1.1.7. Use laptop as a second monitor](#117-use-laptop-as-a-second-monitor)
    - [1.1.8. CLI Tricks](#118-cli-tricks)
      - [1.1.8.1. Download a file in a flakey internet connection](#1181-download-a-file-in-a-flakey-internet-connection)
      - [1.1.8.2. Journalctl find logs](#1182-journalctl-find-logs)
      - [1.1.8.3. CLI Search / find words](#1183-cli-search--find-words)
    - [1.1.9. Hotspot](#119-hotspot)
      - [1.1.9.1. linux-wifi-hotspot](#1191-linux-wifi-hotspot)
    - [1.1.10. Image Manipulation](#1110-image-manipulation)
      - [1.1.10.1. Changing Metadata](#11101-changing-metadata)
        - [1.1.10.1.1. Changing DateTime](#111011-changing-datetime)
      - [1.1.10.2. Overlaying DateTime On top of image](#11102-overlaying-datetime-on-top-of-image)
    - [1.1.11. Video Manipulation (NixOS)](#1111-video-manipulation-nixos)
      - [1.1.11.1. FFmpeg](#11111-ffmpeg)
      - [1.1.11.2. Add Subtitles](#11112-add-subtitles)
    - [1.1.12. File Systems](#1112-file-systems)
      - [1.1.12.1. BTRFS](#11121-btrfs)
        - [compression:](#compression)
        - [ntfs2btrfs:](#ntfs2btrfs)
    - [1.1.13. Tested in Other Linuxs](#1113-tested-in-other-linuxs)
      - [1.1.13.1. Add more resolution options (Linux Mint)](#11131-add-more-resolution-options-linux-mint)
    - [1.1.14. rsync](#1114-rsync)
    - [1.1.15. Reconfiguring System from scratch](#1115-reconfiguring-system-from-scratch)
      - [1.1.15.1. KDE Plasma](#11151-kde-plasma)
      - [1.1.15.2. Grub](#11152-grub)
    - [1.1.16. Partitioning](#1116-partitioning)
      - [1.1.16.1. Multiple Directories on same partition](#11161-multiple-directories-on-same-partition)
    - [1.1.17. Desktop Shortcuts](#1117-desktop-shortcuts)
      - [1.1.17.1. Shortcuts to a website (webapps / web app)](#11171-shortcuts-to-a-website-webapps--web-app)
    - [1.1.18. NixOS](#1118-nixos)
      - [1.1.18.x. Making environment](#1118x-making-environment)
        - [1.1.18.x.1 Python](#1118x1-python)
      - [1.1.18.1. Simple configuration.nix to get you started](#11181-simple-configurationnix-to-get-you-started)
      - [1.1.18.2. Chroot into nixOS btrfs system](#11182-chroot-into-nixos-btrfs-system)
      - [1.1.18.3. LVM Setup](#11183-lvm-setup)
        - [1.1.18.3.1. LVM Cache](#111831-lvm-cache)
      - [1.1.18.4. Update Channels](#11184-update-channels)
      - [1.1.18.5. Remote Builds](#11185-remote-builds)
        - [For nixos-rebuild](#for-nixos-rebuild)
        - [For flakes and nix develop](#for-flakes-and-nix-develop)
      - [1.1.18.6. Partitioning in nixOS](#11186-partitioning-in-nixos)
        - [1.1.18.6.1. Multiple Directories on same partition in nixOS](#111861-multiple-directories-on-same-partition-in-nixos)
    - [1.1.19. Mount options in linux](#1119-mount-options-in-linux)
  - [1.2. **Windows**](#12-windows)
    - [1.2.1. Recover /efi/boot for Windows](#121-recover-efiboot-for-windows)
    - [1.2.2. Move the msr partition \& other partition problems](#122-move-the-msr-partition--other-partition-problems)
  - [1.3. **Android**](#13-android)
    - [1.3.1. Root with Magisk (A70)](#131-root-with-magisk-a70)
    - [1.3.2. Hide root from apps without MagiskHide](#132-hide-root-from-apps-without-magiskhide)
- [2. Programs](#2-programs)
  - [2.1. VSC (Visual Studio Code)](#21-vsc-visual-studio-code)
    - [2.1.1. VSC Extensions](#211-vsc-extensions)
    - [2.1.2. VSC debugger](#212-vsc-debugger)
    - [2.1.3. VSC - OSS (Open source Visual Studio `code`)](#213-vsc---oss-open-source-visual-studio-code)
    - [2.1.4. VSC - Remote Development (with ssh)](#214-vsc---remote-development-with-ssh)
    - [2.1.5. Fix Live share in Manjaro](#215-fix-live-share-in-manjaro)
  - [2.2. ssh (in lan)](#22-ssh-in-lan)
    - [2.2.1. Install in Manjaro](#221-install-in-manjaro)
    - [2.2.2. Access through another PC](#222-access-through-another-pc)
    - [2.2.3. Access through phone](#223-access-through-phone)
    - [2.2.4. ssh without password (public \& private keys)](#224-ssh-without-password-public--private-keys)
    - [2.2.5. ssh config file (`~/.ssh/config`)](#225-ssh-config-file-sshconfig)
    - [2.2.6. Forward GUI (X11 forwarding)](#226-forward-gui-x11-forwarding)
  - [2.3. VMs](#23-vms)
    - [2.3.1. VirtualBox](#231-virtualbox)
      - [2.3.1.1. Host Manjaro](#2311-host-manjaro)
    - [2.3.2. Virtual Machine Manager / virt-manager (comes with KDE)](#232-virtual-machine-manager--virt-manager-comes-with-kde)
    - [2.3.3. Guest Manjaro](#233-guest-manjaro)
    - [2.3.4. SSH into Guest Manjaro](#234-ssh-into-guest-manjaro)
    - [2.3.5. High Performance VMs](#235-high-performance-vms)
  - [2.4. Vivaldi](#24-vivaldi)
    - [2.4.1. Search Engines](#241-search-engines)
- [3. Coding Languages](#3-coding-languages)
  - [3.1. MarkDown](#31-markdown)
    - [3.1.1. MarkDown CheatSheet](#311-markdown-cheatsheet)
    - [3.1.2. Extensions for md](#312-extensions-for-md)
    - [3.1.3. Markdown title into an HTML anchor](#313-markdown-title-into-an-html-anchor)
  - [3.2. LaTeX](#32-latex)
  - [3.3. Python](#33-python)
    - [3.3.1. Dependencies](#331-dependencies)
- [4. Others](#4-others)
  - [4.1. Camera (EOS 1100D)](#41-camera-eos-1100d)
    - [4.1.1. Timelapse](#411-timelapse)
  - [4.2. Programs to Install](#42-programs-to-install)
    - [4.2.1. Android](#421-android)
    - [4.2.2. Surface (Windows)](#422-surface-windows)
      - [4.2.2.1. Installing only some apps of Office](#4221-installing-only-some-apps-of-office)
    - [4.2.3. Linux](#423-linux)

## 1. OSs

---

### 1.1. **Linux** (Manjaro)

#### 1.1.1. Autostart Tasks

- Anacron  
[More Anacron Info](https://serverfault.com/questions/52335/job-scheduling-using-crontab-what-will-happen-when-computer-is-shutdown-during)  
Its also a bitch
  - [Anacron jobs as a user](https://askubuntu.com/questions/235089/how-can-i-run-anacron-in-user-mode)
    - Change default editor when you run `crontab -e`:

  ```bash
    export EDITOR=/bin/nano
    export VISUAL=nano
  ```

#### 1.1.2. PDFs

##### 1.1.2.1. Unite

- Unite (simple):  

  1. `pdfunite *.pdf pdfsss.pdf`

- [Unite with Table of contents](https://unix.stackexchange.com/questions/368415/merge-pdf-files-and-automatically-create-a-table-of-contents-with-each-file-as-a):

  1. Dependencies:
      - `sudo pacman -Sy bcprov`
      - in the software center install the `java-commons-lang` package
  2. Put this script in an .sh executable file in the same folder as  all the pdfs and run it:

  ```bash
  #!/bin/bash

  out_file="combined.pdf"
  bookmarks_file="/tmp/bookmarks.txt"
  bookmarks_fmt="BookmarkBegin
  BookmarkTitle: %s
  BookmarkLevel: 1
  BookmarkPageNumber: %d
  "

  rm -f "$bookmarks_file" "$out_file"

  declare -a files=(*.pdf)
  page_counter=1

  # Generate bookmarks file.
  for f in "${files[@]}"; do
      title="${f%.*}"
      printf "$bookmarks_fmt" "$title" "$page_counter" >> "$bookmarks_file"
      num_pages="$(pdftk "$f" dump_data | grep NumberOfPages | awk '{print $2}')"
      page_counter=$((page_counter + num_pages))
  done

  # Combine PDFs and embed the generated bookmarks file.
  pdftk "${files[@]}" cat output - | \
      pdftk - update_info "$bookmarks_file" output "$out_file"
  ```

  3. in nixOS, you can run it with something like:  
     `chmod +x ./script.sh && nix-shell -p pdftk --command "sh ./script.sh"`

##### 1.1.2.2. OCR

[see the language acronyms](https://tesseract-ocr.github.io/tessdoc/Data-Files-in-different-versions.html)

- `pip install ocrmypdf`
- `sudo pacman -Sy tesseract`
- `sudo pacman -Sy tesseract-data-eng`
- `sudo pacman -Sy tesseract-data-por`
- `ocrmypdf -l eng+por input.pdf output.pdf`
- **NixOS:**
  - `nix-shell -p tesseract -p ocrmypdf --run "ocrmypdf -l eng+por input.pdf output.pdf"`

##### 1.1.2.3. [Compress](https://unix.stackexchange.com/questions/274428/how-do-i-reduce-the-size-of-a-pdf-file-that-contains-images)

- `gs -sDEVICE=pdfwrite -dPDFSETTINGS=/ebook -q -o output.pdf file.pdf`
- **NixOS:**
  - `nix-shell -p ghostscript --command "gs -sDEVICE=pdfwrite -dPDFSETTINGS=/ebook -q -o output.pdf file.pdf"`

#### 1.1.3. Latte Dock

- [Copy latte dock from main screen to the other monitor](https://www.reddit.com/r/kde/comments/gmgpz6/how_to_create_an_additional_latte_dock_on_second/):  
Right Click Dock in main screen > Edit Dock > Right Click it AGAIN > Edit/Add Panels > Duplicate Panel

#### 1.1.4. Notifications

##### 1.1.4.1. Fix notifications error in latte dock

  > Notifications are currently provided by 'KDE Plasma'  

  check [Latte-Dock: Notifications are currently provided by 'KDE Plasma' - Fix](https://www.youtube.com/watch?v=9d35CMxJkLM)
  
##### 1.1.4.2. Notification badges in electron apps (like discord)

  Don't work, we're [waiting](https://github.com/electron/electron/issues/30085).
  
##### 1.1.4.3. Send linux OS notifications through terminal/console/cli

  Try: `notify-send "$USER and $HOME"` go ahead!
  
#### 1.1.5. [Button To Boot into Windows in a dual boot](https://askubuntu.com/questions/42390/one-click-shutdown-ubuntu-and-load-into-alternative-bootup)

- My .desktop file:
  
  ```bash
  [Desktop Entry]
  Comment[en_GB]=
  Comment=
  Exec=gksu grub-reboot Windows && reboot
  GenericName[en_GB]=
  GenericName=
  Icon=/home/yeshey/.icons/Windows_logo_2021.png
  MimeType=
  Name[en_GB]=GoToWindows
  Name=GoToWindows
  Path=
  StartupNotify=true
  Terminal=false
  TerminalOptions=
  Type=Application
  X-DBUS-ServiceName=
  X-DBUS-StartupType=
  X-KDE-SubstituteUID=false
  X-KDE-Username=
  ```

#### 1.1.6. Ohmy - zsh (instead of bash)

[Installation Guide](https://gist.github.com/yovko/becf16eecd3a1f69a4e320a95689249e)

- Plugins:
  - zsh-autosuggestions
- Commands:
  - Change config: `nano .zshrc`
  - Apply the changes: `source ~/.zshrc`
- [my `.zshrc` configuration](https://github.com/Yeshey/Linux_config/blob/main/.zshrc)

#### 1.1.7. Use laptop as a second monitor

- How I made it work:
  1. Install [deskreen](https://deskreen.com/lang-en) in the main machine
  2. [Make a dummy second screen from your linux machine](https://github.com/pavlobu/deskreen/issues/42)
     1. Depends on the graphical drivers ou're using. Check comments for other solutions. This solution works for the open source drivers.
     2. [For nvidia drivers](https://github.com/pavlobu/deskreen/issues/42#issuecomment-770766553) use [this method](https://unix.stackexchange.com/questions/559918/how-to-add-virtual-monitor-with-nvidia-proprietary-driver), but attention, when adding that config file, add a comma and the screen (or your main screen will be black, can fix by going with CTRL + ALT + 2-9 to another terminal). For example:

        1. ```txt
           (base)  yeshey@Manjaro-Laptop  ~  xrandr 
           DP-0 disconnected (normal left inverted right x axis y axis)
           DP-1 disconnected (normal left inverted right x axis y axis)
           HDMI-0 disconnected (normal left inverted right x axis y axis)
           DP-2 connected primary 1920x1080+0+0 (normal left inverted right x axis y axis) 344mm x 194mm
             1920x1080     60.03*+
           DP-3 disconnected (normal left inverted right x axis y axis)
           DP-4 disconnected (normal left inverted right x axis y axis)
           ```

        2. so, in the file `nano /etc/X11/xorg.conf.d/30-virtscreen.conf` I'd put:

        3. ```txt
            Section "Device"
                Identifier  "nvidiagpu"
                Driver      "nvidia"
            EndSection

            Section "Screen"
                Identifier  "nvidiascreen"
                Device      "nvidiagpu"
                Option      "ConnectedMonitor" "LVDS-0,DP-1,DP-2"
            EndSection
            ```

  3. Now you have a new screen, can control with `Win + P`, and see it in settings, so broadcast it
     1. open deskreen > share desktop screen > share the new screen you created
  4. You can change the resolution of the new screen, but you're bounded by presets, as explained in [the post](https://unix.stackexchange.com/questions/559918/how-to-add-virtual-monitor-with-nvidia-proprietary-driver). The best we have is `xrandr --output DP-1 --mode 1600x900`

> - Other posts that helped me get here:
>   - [r/linux questions - How can I use my old laptop as second monitor](https://www.reddit.com/r/linuxquestions/comments/qp3p7a/how_can_i_use_my_old_laptop_as_second_monitor/)
>   - [r/linuxquestions - Using VNC to extend the display of desktop into laptop screen.](https://www.reddit.com/r/linuxquestions/comments/gh1307/using_vnc_to_extend_the_display_of_desktop_into/)

#### 1.1.8. CLI Tricks

##### 1.1.8.1. Download a file in a flakey internet connection

- Downloads to current directory, tries infinite times, and resumes from where it left off:
- `wget --tries=inf --continue http://speedtest-sgp1.digitalocean.com/5gb.test`
`

##### 1.1.8.2. Journalctl find logs

- `journalctl --since "1 hour ago" > /home/yeshey/journal.txt`

##### 1.1.8.3. CLI Search / find words

- [Find a files location through its name recursively](https://stackoverflow.com/questions/5905054/how-can-i-recursively-find-all-files-in-current-and-subfolders-based-on-wildcard):
  - `find . 2>/dev/null -print | grep -i 'product.json' 2>/dev/null` (the *2>/dev/null* [hides premission errors](https://stackoverflow.com/questions/762348/))
  - `tree -P 'product.json' --prune`
- [Find all files containing specific text on Linux](https://stackoverflow.com/questions/16956810/how-do-i-find-all-files-containing-specific-text-on-linux):
  - `grep -Ril "text-to-find-here" /`

#### 1.1.9. Hotspot

For reliable hotspot in arch install:  

##### 1.1.9.1. [linux-wifi-hotspot](https://github.com/lakinduakash/linux-wifi-hotspot)

- Launch gui with `wihotspot`
- Run on startup with `systemctl enable create_ap`
- Disable Running on startup with `systemctl disable create_ap`

#### 1.1.10. Image Manipulation

##### 1.1.10.1. Changing Metadata

###### 1.1.10.1.1. [Changing DateTime](https://unix.stackexchange.com/questions/140427/change-time-date-in-or-from-exif-data)

- You can check an image metadata with `file IMG.jpg`
- Change datetime property to add 44min and 34 seconds to all images: `jhead -ta+0:44:34 *.JPG`

##### 1.1.10.2. Overlaying DateTime On top of image

- Check comments for more references
- Note: you can also use `mogrify` included in the package instead of `convert` to replace the images in place, example:

  - ```bash
      mogrify -resize 390 *.jpeg # resizes so the width is 390
      mogrify -gravity South -chop 0x267 *.jpeg # crops bottom 267 rows of pixels
      mogrify -gravity North -chop 0x206 *.jpeg # crops top 267 rows of pixels
    ```

- Change one character of all files in folder `find ./ -depth -name '*' -execdir bash -c 'mv -- "$1" "${1/f/w}"' bash {} \;` changes `f` to `w`
- [Code mostly taken from here](https://superuser.com/questions/649033/add-timestamp-to-image-from-linux-command-line)
- [See this for documentation on how to Overlay info on images with imagemagick](https://legacy.imagemagick.org/Usage/annotating/)

```bash
#!/usr/bin/env bash

terminater(){
    echo
    echo " Exiting normally"
    exit  # Exits normally
}

# How to use imagemagick annotate:
#https://legacy.imagemagick.org/Usage/annotating/

# Taken from https://superuser.com/questions/649033/add-timestamp-to-image-from-linux-command-line

## This command will find all image files, if you are using other
## extensions, you can add them: -o "*.foo"
find . -iname "*.jpg" -o -iname "*.jpeg" -o -iname "*.tif" -o \
 -iname "*.tiff" -o -iname "*.png" | 

while IFS= read -r img; do
    name=$(basename "$img")
    path=$(dirname "$img")
    ext="${name/#*./}"; 

    ## Check whether this file has exif data
    if exiv2 "$img" 2>&1 | grep timestamp >/dev/null 
    ## If it does, read it and add the water mark   
    then
    echo "Processing $img...";
    convert "$img" \
            -rotate -90 `# we have to rotate and back bc magick is drink` \
            -stroke '#000C' -strokewidth 20 `# Increases the font to the outside and inside, to have the black outline` \
            -gravity NorthWest -pointsize 250 `# pointsize is the font size` \
            -annotate +70+70 %[exif:DateTimeOriginal] `# +70+70 is the pixels distance from the corner` \
            `# Then we draw everything again so we have the black outline` \
            -stroke  none   -fill white    -gravity NorthWest -pointsize 250 -annotate +70+70 %[exif:DateTimeOriginal] \
            -rotate 90 `# drunk magick` \
            "$path/${name/%.*/_time.$ext}" || terminater;
    fi 
done
```

#### 1.1.11. Video Manipulation (NixOS)

##### 1.1.11.1. FFmpeg

- Trim Video:
  - `nix-shell -p ffmpeg --run "ffmpeg -i input.mp4 -ss 00:01:00 -to 00:02:10 -c:v copy -c:a copy output2.mp4"`

##### 1.1.11.2. Add Subtitles

Using [openai's whisper](https://github.com/openai/whisper):

- `nix-shell -p openai-whisper --run "whisper ./input.mp4 --language Portuguese"`

#### 1.1.12. File Systems

##### 1.1.12.1. BTRFS

- Supports spanning multiple drives with one file system without LVM!!

- Mount options:
```bash
    "defaults"
    "nofail" # boots anyways if can't find the disk 
    "users" # any user can mount
    "x-gvfs-show" # show in gnome disks
    "noatime" # doesn't write access time to files
    "compress-force=zstd:5" # compression level 5, good for slow drives. forces compression of every file even if fails to compress first segment of the file
    "ssd" # optimize for an ssd
    "nosuid" "nodev" # for security (https://serverfault.com/questions/547237/explanation-of-nodev-and-nosuid-in-fstab)
```
- check mount options of mounted btrfs file systems:
  ```bash
    sudo findmnt -t btrfs
  ```
###### compression:

- `"compress-force=zstd:5"`: default is level 3, higher is more compression, i use 5 in slower drives, because in those the bottleneck is IO
- check how much is being saved by compression: `nix-shell -p compsize --run "sudo compsize /mnt/btrfsMicroSD-DataDisk"`
- tell btrfs to compress everything according to current flags: `sudo btrfs filesystem defragment -v -r -czstd /mnt/btrfsMicroSD-DataDisk`

###### ntfs2btrfs:

- it will have `space_cache=v1`, you can check what you're using with `sudo findmnt -t btrfs` change it to v2 by:
1. Unmounting the partition 
2. Removing the v1 cache: `sudo btrfs rescue clear-space-cache v1 /dev/sda2`
3. Remounting with `"space_cache=v2"`, or at least `defaults` (not sure if needed)


#### 1.1.13. Tested in Other Linuxs

##### 1.1.13.1. Add more resolution options (Linux Mint)  

(this might not work if you have a NVIDIA card with propriatery drivers)

- [In linux Minit you have the `~/.profile` file](https://forums.linuxmint.com/viewtopic.php?t=291078), where you can run `xrandr` commands for each user  
  [But here's how to do it for the whole system:](https://forums.linuxmint.com/viewtopic.php?p=1709995#p1709995)
  - Mint reads everything inside `/etc/lightdm/lightdm.conf.d` on boot, you can add a file there that points to a script of yours to execute the `xrandr` commands.  
  1. Create a new file like `sudo nano /etc/lightdm/lightdm.conf.d/71-linuxmint.conf` and add the following:

      ```bash
      [SeatDefaults]
      user-session=cinnamon
      display-setup-script=/usr/bin/LGmonitor.bsh
      ```

  2. Create the script at `sudo nano /usr/bin/LGmonitor.bsh`  
     And add the `xrandr` commands:

      ```bash
      xrandr --newmode "1440x900_60.00"  106.50  1440 1528 1672 1904  900 903 909 934 -hsync +vsync
      xrandr --addmode VGA-1 1440x900_60.00 

      xrandr --newmode "1280x800_60.00"   83.50  1280 1352 1480 1680  800 803 809 831 -hsync +vsync
      xrandr --addmode VGA-1 1280x800_60.00

      xrandr --newmode "1920x1080_60.00"  172.80  1920 2040 2248 2576  1080 1081 1084 1118  -HSync +Vsync
      xrandr --addmode VGA-1 "1920x1080_60.00"
      ```

      (note that instead of VGA-1 you might have to put something else like DP-2, you should be able to check it in your display application where you change the resolution)
  3. Make the script executable:  
     `sudo chmod +x /usr/bin/LGmonitor.bsh`
  4. You are now able to change the resolution in all users from your display application.

#### 1.1.14. rsync

- [Command to copy ***Everything***](https://askubuntu.com/questions/117014/what-is-the-easiest-way-to-merge-and-home):
  - `sudo rsync -avz --hard-links --info=progress2 --numeric-ids /mnt/oldhome/ /mnt/root/home`

#### 1.1.15. Reconfiguring System from scratch

##### 1.1.15.1. KDE Plasma

- Shortcuts:
  - ALT-Space opens the search box for plasma, very handy
  - `spectacle -brc`  |  Takes screenshot of part of screen and saves to clipboard
- Desktop Configuration:
  - Try to load most of it from the PlasmaConfigSaverBkup.tar.gz file in this repo, install the dependencies `scrot` & `kdialog` for the Plasma Config Saver widget to work.
- [Make the Windows_Key/Meta open the Application launcher](https://askubuntu.com/questions/246886/how-do-i-open-the-application-launcher-on-kde-with-just-the-meta-windows-key)
- If Apps are to big, like vivaldi taking too much space, go to Settings > Fonts > Force font DPI, I have it at `96`

##### 1.1.15.2. Grub

- [Adding reboot and poweroff grub entries](https://daulton.ca/2018/08/reboot-and-shutdown-options-grub/)
  - Edit `nano /etc/grub.d/40_custom`
  - Add:

    ```conf
    menuentry "Reboot" {
        reboot
    }

    menuentry "Shut Down" {
        halt
    }

    # menuentry 'Windows' {
    #    savedefault
    #    load_video
    #    insmod part_gpt
    #    insmod fat
    #    search --no-floppy --fs-uuid --set=root FA05-EB82
    #    chainloader /EFI/Microsoft/Boot/bootmgfw.efi
    # }
    ```

  - `update-grub`
- Adding Grub entry to boot into CLI
  - [Source 1 (Ubuntu)](https://askubuntu.com/questions/1029339/add-grub-menu-item-to-boot-into-terminal)
  - [Source 2 (Manjaro)](https://archived.forum.manjaro.org/t/how-to-boot-linux-to-command-line-mode-instead-of-gui-solved/30854)
  - Relevant file system places are :`/etc/grub.d/`(save your configuration in 40_custom), `/boot/grub/` grub.cfg is where your configuration gets generated to.
    - If you have no more entries, to show grub anyways, edit `sudo nano /etc/default/grub`:
      - Edit `TIMEOUT=10`
      - Edit `GRUB_TIMEOUT_STYLE=menu`
      - Run `update-grub`
    - To set a certain grub entry as default you can change the line `GRUB_DEFAULT=saved` to a number

#### 1.1.16. Partitioning

- When limited space in ssd, and a devide is needed between ssd and hdd, [read this](https://nickbair.net/2010/10/30/a-good-ssdhdd-partitioning-scheme/).
- Swap can be also divided, you can have 5Gb in one partition and 5 in another and set their priorities.

##### 1.1.16.1. Multiple Directories on same partition

[You can achieve this in one of 2 ways:](https://unix.stackexchange.com/questions/47222/how-to-mount-multiple-directories-on-the-same-partition)

- Use symlinks. Then create symlinks from `/home` to `/hd/home`, etc.
  - Make sure you use [relative symlink paths](https://unix.stackexchange.com/questions/10370/make-a-symbolic-link-to-a-relative-pathname) if you go this way
- Instead of symlinks, use bind mounts. Syntax is `mount --bind /hd/home /home`. You can (should) also put that in fstab, using 'bind' as the fstype.

Symlinks seem to be better according to [this](https://unix.stackexchange.com/questions/49623/are-there-any-drawbacks-from-using-mount-bind-as-a-substitute-for-symbolic-lin) answer.

#### 1.1.17. Desktop Shortcuts

Local Shortcuts are here:
- `/home/yeshey/.local/share/applications`

##### 1.1.17.1. Shortcuts to a website (webapps / web app)

- You can use a web app manager, there is [ice](https://github.com/peppermintos/ice) by the peppermint team, and [Webapp Manager](https://github.com/linuxmint/webapp-manager) based on ice by mint (none available in nixOS rn)
- Manually:
  - Any Chromium Based Browser: Options > More Tools > Create Shortcut... (note that this will make an app in the browser that will be launched, if you want to use it with nixOS and home-manager you can't create that app, see the code below)
  - In Vivaldi its different, [see this](https://www.reddit.com/r/vivaldibrowser/comments/fuspx5/how_do_i_create_web_app_shortcuts/)
  - For firefox use one of the Web App Managers... You need a special firefox profile

- In NixOS:  
  You can use Home-manager to automatically make a shortcut like so:   

  ```nix
    # Syncthing shortcut, based on webapp manager created shortcut (https://github.com/linuxmint/webapp-manager)
    home.file.".local/share/applications/vivaldi-syncthing.desktop".source = builtins.toFile "vivaldi-syncthing.desktop" ''
  [Desktop Entry]
  Version=1.0
  Name=Syncthing
  Comment=Web App
  Exec=vivaldi --app="http://127.0.0.1:8384#" --class=WebApp-Syncthingvivaldi5519 --user-data-dir=/home/yeshey/.local/share/ice/profiles/Syncthingvivaldi5519
  Terminal=false
  X-MultipleArgs=false
  Type=Application
  Icon=webapp-manager
  Categories=GTK;WebApps;
  MimeType=text/html;text/xml;application/xhtml_xml;
  StartupWMClass=WebApp-Syncthingvivaldi5519
  StartupNotify=true
  X-WebApp-Browser=Vivaldi
  X-WebApp-URL=http://127.0.0.1:8384#
  X-WebApp-CustomParameters=
  X-WebApp-Navbar=false
  X-WebApp-PrivateWindow=false
  X-WebApp-Isolated=true
    '';
  ```

#### 1.1.18. NixOS

- [Installing directly KDE desktop didn't work for me](https://discourse.nixos.org/t/gui-not-starting-after-upgrade-to-22-05/19534)
- [Mount Internal drive automattically](https://unix.stackexchange.com/questions/533265/how-to-mount-internal-drives-as-a-normal-user-in-nixos)
- Give up on plasma configuration
- [Can't control the brightness of external monitors because of NVIDIA driver](https://discourse.nixos.org/t/brightness-control-of-external-monitors-with-ddcci-backlight/8639/9?u=yeshey), using and `xrandr -q | grep " connected"` for it now `xrandr --output HDMI-0 --brightness 0.5`
- The Stuck on reboot or poweroff problem? [This solves](https://unix.stackexchange.com/questions/577987/graceful-shutdown-with-suspend-job-hanging-in-syscall)

##### 1.1.18.x. Making environment 

###### 1.1.18.x.1 Python

**Virtual Env**:

See [this project](https://github.com/RICADINHO/ProjetoIAA). But you can use these files:

- In NixOS, you should have flakes, activate the environment (nix develop or direnv allow) and run sh venvnix.sh. Using venv from inside python can and does yeild problems with some packages!


```nix
# https://github.com/nix-community/dream2nix/tree/main

{
  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixpkgs-unstable";
    systems.url = "github:nix-systems/default";
  };

  outputs = { systems, nixpkgs, ... } @ inputs:
  let
    eachSystem = f:
      nixpkgs.lib.genAttrs (import systems) (
        system:
          f nixpkgs.legacyPackages.${system}
      );
  in {
    devShells = eachSystem (pkgs: 
    let
      #lt = pkgs.python311Packages.buildPythonPackage {
      #  pname = "lt_core_news_sm";
      #  version = "3.7.0";
      #  src = pkgs.fetchurl {
      #    url = "https://github.com/explosion/spacy-models/releases/download/pt_core_news_sm-3.7.0/pt_core_news_sm-3.7.0.tar.gz";
      #    hash = "sha256-uG0vywIrvh3/qGkoUskJRZHpPQKZtlxb35L3lArixHw=";
      #  };
      #  buildInputs = with pkgs.python311Packages; [ pipBuildHook ];
      #  dependencies = with pkgs.python311Packages; [ spacy ];
      #};
      #dontCheckPython = drv: drv.overridePythonAttrs (old: { doCheck = false; });
    in {
      default = pkgs.mkShell {
        packages = [
          #pkgs.jupyter-all
          (pkgs.python312.withPackages (python-pkgs: with python-pkgs; [
            tensorflow
            pytorch
            keras
            pandas
            numpy
            jupyter
            matplotlib
            nltk # (NLP processing)
            spacy # (NLP processing)
            # lt
            progressbar
            transformers
            datasets

            #torch

            # Add version overrides for conflicting dependencies
            #(protobuf.overridePythonAttrs (old: { version = "4.25.3"; }))
            #(typing-extensions.overridePythonAttrs (old: { version = "4.9.0"; }))
            #(numpy.override { blas = pkgs.openblasCompat; })
          ]))
          pkgs.virtualenv
        ];

        shellHook = ''
          echo "Development shell ready!"
          echo "Run with > jupyter notebook"

          echo "when running if you see this on the browser: http://127.0.0.1:8890/tree?token=6c86ed65bba3efd8ebd779bb4263094bbaaa4d9c28a648f4, that means that if you want to use the jupyternotebook server as a kernel for VSC, you need to use 6c86ed65bba3efd8ebd779bb4263094bbaaa4d9c28a648f4 as the password"

          # jupyter notebook
        '';
      };
    });
  };
}
```

```bash
# venvnix.sh
# https://acalustra.com/optimizing-python-development-virtualenv-kernels-with-nix-and-jupyter.html
echo "Creating venv $1"
# VENV_FOLDER="$HOME/venvs/$1"
VENV_FOLDER=".venv"

if test -d "$VENV_FOLDER"; then
    echo "${VENV_FOLDER} is already created"
    nix shell github:GuillaumeDesforges/fix-python --command fix-python --venv "$VENV_FOLDER"
    exit 0
fi

echo "creating venv $1 on folder $VENV_FOLDER"
virtualenv "$VENV_FOLDER"

# Upgrade pip and install requirements in the new venv
"$VENV_FOLDER/bin/pip" install --upgrade pip
"$VENV_FOLDER/bin/pip" install -r requirements.txt

"$VENV_FOLDER/bin/pip" install ipykernel

nix shell github:GuillaumeDesforges/fix-python --command fix-python --venv "$VENV_FOLDER"
"$VENV_FOLDER/bin/python" -m ipykernel install --prefix="$HOME/.local/share" --name "venv-$1"
jupyter kernelspec install --user "$HOME/.local/share/share/jupyter/kernels/venv-$1"
```

**With poetry and poetry2nix and nix run**

You can see [this project](https://github.com/Yeshey/chat_analyzer).

Here is a rundown:

**Make a poetry2nix project**

1. Start with `nix-shell -p poetry`
2. `poetry init`
3. Add packages with for example `poetry add matplotlib pandas python-dateutil`
4. structure:
    ```
    ├── chatanalyzer # same as project name `[tool.poetry]` `name = "chatanalyzer"`
    │   ├── __init__.py
    │   └── main.py 
    ```
5. script defined in poetry's toml
   ```toml
    [tool.poetry.scripts]
    start = "chatanalyzer.main:main" # file main, runs function main
   ```
6. As mencioned in the script above `main.py` needs to have a `def main()` function, that is what will be ran.
7. the `start` here: ` start = "chatanalyzer.main:main" # file main, runs function main` is the same in the flake.nix here: `program = "${self.packages.${system}.default}/bin/start";`

**Update:**
1. `nix develop`
2. `poetry update`
3. `nix flake update`

##### 1.1.18.1. Simple configuration.nix to get you started

Activate with `sudo nixos-rebuild --flake ~/.setup#hyrulecastle --option cores 6 --option max-jobs 3 boot && reboot` after changing the partitions properly, and adding swap to not run out of swap

```nix
# Edit this configuration file to define what should be installed on
# your system.  Help is available in the configuration.nix(5) man page
# and in the NixOS manual (accessible by running ‘nixos-help’).

{ config, pkgs, lib, ... }:

{
  imports =
    [ # Include the results of the hardware scan.
      ./hardware-configuration.nix
    ];

  # Use the systemd-boot EFI boot loader.
  boot.loader.efi.canTouchEfiVariables = true;
  boot.loader.efi.efiSysMountPoint = "/boot";
  boot.loader.systemd-boot = {
    enable = true;
    configurationLimit = 10; # You can leave it null for no limit, but it is not recommended, as it can fill your boot partition.
  };

  # Bootloader (For BIOS VMs)
  /*
  boot.loader.grub.enable = true;
  boot.loader.grub.device = "/dev/vda";
  boot.loader.grub.useOSProber = true;
  */

  # Bootloader (For UEFI VMs)
  /*
  boot.loader = {

    timeout = 2;
    efi = {
      canTouchEfiVariables = true;
      efiSysMountPoint = "/boot/efi";
    };
    grub = {
      enable = true;
      version = 2;
      efiSupport = true;
      devices = [ "nodev" ];
      device = "nodev";
      useOSProber = true;
      # default = "saved"; # doesn't work with btrfs :(
      extraEntries = ''
        menuentry "Reboot" {
            reboot
        }

        menuentry "Shut Down" {
            halt
        }

        # Option info from /boot/grub/grub.cfg, technotes "Grub" section for more details
        menuentry "NixOS - Console" --class nixos --unrestricted {
        search --set=drive1 --fs-uuid 69e9ba80-fb1f-4c2d-981d-d44e59ff9e21
        search --set=drive2 --fs-uuid 69e9ba80-fb1f-4c2d-981d-d44e59ff9e21
          linux ($drive2)/@/nix/store/ll70jpkp1wgh6qdp3spxl684m0rj9ws4-linux-5.15.68/bzImage init=/nix/store/c2mg9sck85ydls81xrn8phh3i1rn8bph-nixos-system-nixos-22.11pre410602.ae1dc133ea5/init loglevel=4 3
          initrd ($drive2)/@/nix/store/s38fgk7axcjryrp5abkvzqmyhc3m4pd1-initrd-linux-5.15.68/initrd
        }

      '';
    };
  };
  */

  boot.tmp.cleanOnBoot = true;
  boot.supportedFilesystems = [ "ntfs" "bcachefs" ];

  boot.kernelPackages = pkgs.linuxPackages_latest;

  # Enable CUPS to print documents.
  services.printing.enable = true;

  networking.hostName = "nixos"; # Define your hostname.
  # networking.wireless.enable = true;  # Enables wireless support via wpa_supplicant.

  # Enable networking
  networking.networkmanager.enable = true;
  networking.resolvconf.dnsExtensionMechanism = false; # fixes internet connectivity problems with some sites (https://discourse.nixos.org/t/domain-name-resolve-problem/885/2)

  # Set your time zone.
  time.timeZone = "Europe/Lisbon";

  # Select internationalisation properties.
  i18n.defaultLocale = "en_US.UTF-8";

  i18n.extraLocaleSettings = {
    LC_ADDRESS = "pt_PT.UTF-8";
    LC_IDENTIFICATION = "pt_PT.UTF-8";
    LC_MEASUREMENT = "pt_PT.UTF-8";
    LC_MONETARY = "pt_PT.UTF-8";
    LC_NAME = "pt_PT.UTF-8";
    LC_NUMERIC = "pt_PT.UTF-8";
    LC_PAPER = "pt_PT.UTF-8";
    LC_TELEPHONE = "pt_PT.UTF-8";
    LC_TIME = "pt_PT.UTF-8";
  };

  # Enable the X11 windowing system.
  services.xserver.enable = true;

  # Enable the GNOME Desktop Environment.
  services.xserver.displayManager.gdm.enable = true;
  services.xserver.desktopManager.gnome.enable = true;

  # Configure keymap in X11
  services.xserver = {
    xkb.layout = "pt";
    xkb.variant = "";
  };

  services.spice-vdagentd.enable=true; # to enable clipboard sharing in VM

  # Enable the OpenSSH daemon.
  services.openssh = {
    enable = true;
    settings.X11Forwarding = true; # forward graphical interfaces through SSH
    #settings = { # wasn't even working..?
    settings.PermitRootLogin = "yes"; # to let surface and Laptop connect to builds for the surface (https://github.com/NixOS/nixpkgs/issues/20718)
    #};
  };
  programs = {
    ssh = {
      startAgent = true;
      forwardX11 = true;
    };

    # general terminal shell config for all users
    zsh = {
      enable = true;
      shellAliases = {
        vim = "nvim";
        # ls = "lsd -l --group-dirs first";
        #update = "sudo nixos-rebuild switch --flake ${location}#${host}"; # old: "sudo nixos-rebuild switch";
        #upgrade = "trap \"cd ${location} && git checkout -- flake.lock\" INT ; sudo nixos-rebuild switch --flake ${location}#${host} --upgrade --update-input nixos-hardware --update-input home-manager --update-input nixpkgs || (cd ${location} && git checkout -- flake.lock)"; /*--commit-lock-file*/ #upgrade: upgrade NixOS to the latest version in your chosen channel";
        update = "sudo nixos-rebuild switch";
        upgrade = "sudo nixos-rebuild switch --upgrade";
        clean = "echo \"This will clean all generations, and optimise the store\" ; sudo sh -c 'nix-collect-garbage -d ; nix-store --optimise'";
        cp = "cp -i";                                   # Confirm before overwriting something
        df = "df -h";                                   # Human-readable sizes
        free = "free -m";                               # Show sizes in MB
        gitu = "git add . && git commit && git push";
        zshreload = "clear && zsh";
        zshconfig = "nano ~/.zshrc";
        # killall latte-dock && latte-dock & && kquitapp5 plasmashell || killall plasmashell && kstart5 plasmashell"
        re-kde = "nix-shell -p killall --command \"kquitapp5 plasmashell || killall plasmashell && kstart5 plasmashell\""; # Restart gui in KDE
        mount = "mount|column -t";                      # Pretty mount
        speedtest = "nix-shell -p python3 --command \"curl -s https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py | python3 -\"";
        temperature = "watch \"nix-shell -p lm_sensors --command sensors | grep temp1 | awk '{print $2}' | sed 's/+//'\"";
        rvt = "nix-shell -p ffmpeg --command \"bash <(curl -s https://raw.githubusercontent.com/Yeshey/RecursiveVideoTranscoder/main/RecursiveVideoTranscoder.sh)\"";
        ping = "ping -c 5";                             # Control output of ping
        fastping = "ping -c 100 -s 1";
        ports = "netstat -tulanp";                      # Show Open ports
        l="ls -l";
        la="ls -a";
        lla="ls -la";
        lt="ls --tree";
        grep="grep --color=auto";
        egrep="egrep --color=auto";
        fgrep="fgrep --color=auto";
        diff="colordiff";
        dir="dir --color=auto";
        vdir="vdir --color=auto";
        week = "
          now=$(date '+%V %B %Y');
          echo \"Week Date:\" $now
        ";
        myip = "  
          echo \"Your external IP address is:\"
          curl -w '\n' https://ipinfo.io/ip
        ";
        chtp = " curl cht.sh/python/\"$1\" ";           # alias to use cht.sh for python help
        chtc = " curl cht.sh/c/\"$1\" ";                # alias to use cht.sh for c help
        chtsharp = " curl cht.sh/csharp/\"$1\" ";           # alias to use cht.sh for c# help
        cht = " curl cht.sh/\"$1\" ";                   # alias to use cht.sh in general
      };
      autosuggestions.enable = true;
      syntaxHighlighting.enable = true;
      enableCompletion = true;
      histSize = 100000;
      ohMyZsh = {
        enable = true;
        plugins = [ "git" 
                    "colored-man-pages" 
                    "alias-finder" 
                    "command-not-found" 
                    #"autojump" 
                    "urltools" 
                    "bgnotify"];
        theme = "agnoster"; # robbyrussell # agnoster # frisk
      };
    };
  };

  # Configure console keymap
  console.keyMap = "pt-latin1";

  # Enable sound with pipewire.
  hardware.pulseaudio.enable = false;
  security.rtkit.enable = true;
  services.pipewire = {
    enable = true;
    alsa.enable = true;
    alsa.support32Bit = true;
    pulse.enable = true;
  };

  services.libinput.enable = true;

  # Define a user account. Don't forget to set a password with ‘passwd’.
  users.users.yeshey = {
    isNormalUser = true;
    description = "Yeshey";
    extraGroups = [ "networkmanager" "wheel" ];
    packages = with pkgs; [
      firefox
    ];
    
    # needed to make home-manager zsh work with gdm
    shell = pkgs.zsh;
    useDefaultShell = false;
  };
  users.defaultUserShell = pkgs.zsh;

  # Enable automatic login for the user.
  services.displayManager.autoLogin.enable = true;
  services.displayManager.autoLogin.user = "yeshey";

  # Workaround for GNOME autologin: https://github.com/NixOS/nixpkgs/issues/103746#issuecomment-945091229
  systemd.services."getty@tty1".enable = false;
  systemd.services."autovt@tty1".enable = false;

  # Allow unfree packages
  nixpkgs.config.allowUnfree = true;

  nix = let
    substitutersList = [
      "cachenixosorg"
      "numtidecachixorg"
      "nrdxpcachixorg"
      "nixcommunitycachixorg"
    ];

    substitutersMap = {
      cachenixosorg = {
        url = "https://cache.nixos.org";
        key = "cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY=";
      };
      numtidecachixorg = {
        url = "https://numtide.cachix.org";
        key = "numtide.cachix.org-1:2ps1kLBUWjxIneOy1Ik6cQjb41X0iXVXeHigGmycPPE=";
      };
      nrdxpcachixorg = {
        url = "https://nrdxp.cachix.org";
        key = "nrdxp.cachix.org-1:Fc5PSqY2Jm1TrWfm88l6cvGWwz3s93c6IOifQWnhNW4=";
      };
      nixcommunitycachixorg = {
        url = "https://nix-community.cachix.org";
        key = "nix-community.cachix.org-1:mB9FSh9qf2dCimDSUo8Zy7bkq5CX+/rkCWyvRCYg3Fs=";
      };
    };
  in {
    enable = true;
    package = pkgs.nix;
    extraOptions = ''
      !include ./extra.conf
    '';
    settings = lib.mkMerge [
      {
        experimental-features = [ "nix-command" "flakes" "pipe-operators" ];
        nix-path = lib.mapAttrsToList (key: value: "${key}=${value.to.path}") config.nix.registry;
        substituters = map (x: substitutersMap.${x}.url) substitutersList;
        trusted-public-keys = map (x: substitutersMap.${x}.key) substitutersList;
      }
      {
        trusted-public-keys = [ "cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY=" ];
        substituters = lib.mkAfter [ "https://cache.nixos.org/" ];
      }
    ];
  };


  # List packages installed in system profile. To search, run:
  # $ nix search wget
  environment.systemPackages = with pkgs; [
    vim # Do not forget to add an editor to edit configuration.nix! The Nano editor is also installed by default.
    wget
    htop
    git
    gparted
    vscode
    bcachefs-tools
    tmux
  ];

  system.stateVersion = "25.05"; # Did you read the comment?
}
```

- And then copy the ssh keys into the ssh folder
- git clone the repository into ~/.setup/
- and run `sudo nixos-rebuild switch --flake ~/.setup/#vm;` in a terminal window(so it doesn't turn off), in fullscreen in the up part you have a button to send key stroke combinations

##### 1.1.18.2. [Chroot into nixOS btrfs system](https://nixos.wiki/wiki/Change_root)

```bash
sudo mount /dev/nvme0n1p6 /mnt -o subvol=@
sudo mount -o umask=0077,shortname=winnt /dev/nvme0n1p1 /mnt/boot 
sudo nixos-enter --root /mnt

# Remember you can also:
sudo nixos-generate-config --root /mnt # regenerate config
sudo nixos-install --root /mnt # see below
```

- When running `sudo nixos-install --root /mnt`, it will leave everything as is in the `/mnt` and use the `/mnt/etc/nixos/...` configuration. You can do this as an alternative to `nixos-rebuild` inside the chroot environment if it doesn't work.   
You will also have to set the user password again when you boot into the system:
  - `passwd yeshey`

##### 1.1.18.3. LVM Setup

- [Understand](https://askubuntu.com/questions/219881/how-can-i-create-one-logical-volume-over-two-disks-using-lvm) the hierarchy.
- Create the Physical Volumes with Gparted! Then combining them in a Volume Group and making logical volumes has to be with CLI
- My guide on [**Windows Dual boot, LUKS on LVM with LVM cache, btrfs, nixOS**](guides/LUKS%20on%20LVM%20with%20cache%20on%20nixOS.md)

###### 1.1.18.3.1. LVM Cache

Serves to have both fast and slow drives and have performance like the fast drive.

- [Note that in nixOS](https://github.com/NixOS/nixpkgs/issues/15516), to boot into a system with cache you need to add something like

  ```nix
  # get rid of scary warning about missing cache_check
  services.lvm.boot.thin.enable = true;

  # if you don't have enough kernel modules, you'll get this error message:
  # cache: Error creating cache's policy
  boot.initrd.kernelModules = [ "dm-cache" "dm-cache-smq" "dm-cache-mq" "dm-cache-cleaner" ];
  boot.kernelModules = [ "kvm-amd" "dm-cache" "dm-cache-smq" "dm-persistent-data" "dm-bio-prison" "dm-clone" "dm-crypt" "dm-writecache" "dm-mirror" "dm-snapshot"];

  networking.resolvconf.dnsExtensionMechanism = false; # fixes internet connectivity problems with some sites (https://discourse.nixos.org/t/domain-name-resolve-problem/885/2)
  ```

  to the nixOS configuration and run `sudo nixos-rebuild switch`.

- [Best tutorial](https://gist.github.com/gabrieljcs/805c183753046dcc6131) from Github.
- [Red Hat more in depth tutorial](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/logical_volume_manager_administration/lvm_cache_volume_creation)
- \+ Some usefull commands:

  ```bash
  lvremove /dev/VG/root # deletes a Logical volume
  vgcreate VG /dev/sde1 /dev/sdf1 # creates a Volume Group named VG from the 2 Physical Volumes
  lvcreate -n root -l 100%FREE VG /dev/sdb1 # Creates a LV called root with all remaining space of PV
  mkfs.ext4 /dev/VG/root # Makes the the LV created into a ext4 filesystem
  # For viewing:
  lsblk 
  pvs 
  vgs
  lvs

  ```

- After creating LV, you need to also format them to what you need:  
  `mkfs.ext4 /dev/VG/root` ([nixOS wiki](https://nixos.wiki/wiki/LVM))  
  `mkswap /dev/VolGroup00/LogVol02` ([Red Hat Swap in LVM](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/4/html/system_administration_guide/adding_swap_space-creating_an_lvm2_logical_volume_for_swap))

- Then if you want to install nixOS through the GUI in LVM (Calamares installer), you need the efi partition outside of the VG and to have the partitions inside the volume group already formatted.  
You need to select them [without formatting](https://youtu.be/PJilemDeYdo?t=587)  

- I actually had to create all the meta swap cache and root LVs and mkfs.ext4 and mkswap and install, go to the installed nixOS, add the kernel modules in the configuration, run sudo nixos-rebuild switch, and only after go back to the LiveCD and make the cache.

##### 1.1.18.4. Update Channels

- `nix-channel --update`
- To update for a flake, [check this](https://discourse.nixos.org/t/why-nixos-rebuild-wont-use-my-updated-nixpkgs-flake/9578/5) `sudo nix flake update --commit-lock-file`

##### 1.1.18.5. [Remote Builds](https://eno.space/blog/2021/08/nixos-on-underpowered-devices)

###### For nixos-rebuild

This might not apply between PCs of different architectures.
You might need to add `services.openssh.permitRootLogin = "yes";` in both cases

- From weak PC: `sudo nixos-rebuild --flake ~/.setup#kakariko --build-host root@192.168.1.102 switch --verbose`
- From powerful PC: `sudo nixos-rebuild --flake ~/.setup#kakariko --target-host root@192.168.1.103 switch --verbose`

[Here is the official documentation](https://nixos.wiki/wiki/Nixos-rebuild).  
You [should be able to use](https://github.com/NixOS/nixpkgs/issues/80142) `NIX_SSHOPTS="..."` to pass arguments to the ssh running inside the `nixos-rebuild` command.  
Use the `--use-remote-sudo` when you're the building machine, and specifying the `--target-host`, and you don't have sudo, so you want to use the sudo of the target machine.

###### For flakes and nix develop

From the weaker PC: 
```sh
IP="10.19.12.17"; NIX_CONFIG="builders = ssh://root@${IP} x86_64-linux - 1 1 big-parallel"; nix develop --option builders "ssh://root@${IP} x86_64-linux - 1 1 big-parallel" --max-jobs 0 -v
```

##### 1.1.18.6. Partitioning in nixOS

- Note that in nixOS it's a good idea to have the /nix/store in a partition like btrfs due to the large number of inodes used by symlinks, to make sure it doesn't run out of inodes before it runs out of space.
- You can add multiple swap files in nixOS and set their priority in a ext4 partition [like this](https://rycwo.dev/archive/nixos-series-002-swapfiles/)

###### 1.1.18.6.1. Multiple Directories on same partition in nixOS

- nixOS `/nix/store` [can't be symlinked](https://discourse.nixos.org/t/getting-around-no-symlink-policy/19712/3), instead, mount with --binds

  1. Edit `/etc/nixos/configuration.nix` to mount the partition in the extra disk on boot, make sure to add `neededForBoot` as the bind mounts will need this mount to be executed first.

    ```nix
    fileSystems."/mnt/btrfsMicroSD" =
      { device = "/dev/disk/by-label/btrfsMicroSD";
        fsType = "btrfs";
        neededForBoot = true;
      };
    ```

  2. `sudo nixos-rebuild switch`
  3. Add the configuration to mount the selected folders from the mounted drive into their places:

  ```nix
  fileSystems."/nix" =
    { device = "/mnt/btrfsMicroSD/nix"; 
      fsType = "none";
      options = [ "bind" ];
    };
  ```

  4. `sudo nixos-rebuild boot` to make sure the configuration doesn't break your system right away.
  5. `sudo mv -f` the folder into the new drive, (you could also reboot and do this from a live USB)  
  `sudo mv -f /nix /mnt/ext4MicroSD/`  
  ( or [copy it](https://cs-syd.eu/posts/2019-09-14-nix-on-seperate-device), but doesn't seem to quite work `sudo rsync --recursive --links --info=progress2 /nix /mnt/ext4MicroSD/`)
      - Note that doing this for `/var` might give `Operation not permitted` even with root. Run `sudo chattr -i var/empty/` and remove now for it to work `studo rm -vrf var`
  6. Now Reboot and you should be good to go.

- Another way to takle this would be with LVM or btrfs subvolumes or multiple disks support...

#### 1.1.19. Mount options in linux

- **NTFS**
  ```nix
  # MY MOUNTS (works for wine gaming)
  fileSystems."/mnt/DataDisk" = {
    device = "/dev/disk/by-label/DataDisk";
    fsType = "lowntfs-3g";
    options = [
      "uid=1000" "gid=1000" "rw" "exec" "umask=000" # "user"
      # gaming options as per valve: https://github.com/ValveSoftware/Proton/wiki/Using-a-NTFS-disk-with-Linux-and-Windows
      # "ignore_case" # prevents you from making any file or directory with any upper case letter... only lowntfs-3g 
      #"windows_names" # makes games not work
      "nofail"
      /*
      "defaults"
      # "nosuid" "nodev" # security, probably should
      "nofail"
      "x-gvfs-show"
      "windows_names"
      "big_writes"
      "streams_interface=windows" # only ntfs-3g 
      "nls=utf8" */
    ];
  };
  ```
- **BTRFS**
  ```nix
  fileSystems."${config.mySystem.dataStoragePath}" = {
    device = "/dev/disk/by-label/btrfsMicroSD-DataDisk";
    fsType = "btrfs";
    options = [ # check mount options of mounted btrfs fs: sudo findmnt -t btrfs
      "defaults"
      "nofail" # boots anyways if can't find the disk 
      # "users" # don't use, drive became invisible in steam because of this! (any user can mount)
      "x-gvfs-show" # show in gnome disks
      "noatime" # doesn't write access time to files
      "compress-force=zstd:5" # compression level 5, good for slow drives. forces compression of every file even if fails to compress first segment of the file
      # "ssd" # optimize for an ssd
      # security "nosuid" "nodev" (https://serverfault.com/questions/547237/explanation-of-nodev-and-nosuid-in-fstab)
    ];
  };
  ```

---

### 1.2. **Windows**

#### 1.2.1. Recover /efi/boot for Windows

On a dual boot system if you can't boot into windows anymore, do this:

- [Follow this](https://www.youtube.com/watch?v=l_I4K2-Rr_Y) to be able to boot back into Windows
- now grub must have disappeared, so, chroot or boot through bios into [manjaro with `manjaro-chroot -a`](https://wiki.manjaro.org/index.php/GRUB/Restore_the_GRUB_Bootloader) and fix grub
  - \# `grub-install`
  - \# `update-grub`
- Now grub should appear again
- [if it doesn't detect windows, try this](https://askubuntu.com/questions/197868/grub-does-not-detect-windows)
- In Windows you might have now a choose operating system question on boot, if so, [follow these instructions from here](https://www.windowsdigitals.com/how-to-remove-choose-an-operating-system-screen-windows-10/)
  - If it doesn't let you, try to run `chkdsk /f /r` [as explained here](https://www.youtube.com/watch?v=FejmrhtxauU)

#### 1.2.2. Move the msr partition & other partition problems

- You can move the msr (reported as the Microsoft reserved partition in gparted) without breaking your PCs boot capacity [by following this](https://superuser.com/questions/1532044/e2fsck-error-when-trying-to-move-windows-msr-partition-with-gparted)
- All other windows partitions you can move and resize with the AOMEI Partition Assistent (only untested scenario is to move the EFI paprtition, witch I don't advise especially in dual boot, but growing it is fine)
- If you have multiple recovery partitions [check this](https://superuser.com/questions/1210470/multiple-recovery-partitions-in-windows-10) to see witch one your system is using and delete the other

---

### 1.3. **Android**

#### 1.3.1. Root with Magisk (A70)

- [This guy knows his shit](https://forum.xda-developers.com/t/recovery-unofficial-root-twrp-for-galaxy-a70.3955984/)
- [With some help from this guide](https://magiskapp.com/root-samsung-galaxy-a70s-using-magisk/)

#### 1.3.2. Hide root from apps without MagiskHide

- YOu need to pass safety net, wich is google's method to detect root on android devices. [Follow this guide](https://www.droidwin.com/how-to-pass-safetynet-on-rooted-android-12/)

## 2. Programs

### 2.1. VSC (Visual Studio Code)

#### 2.1.1. VSC Extensions

- [Auto install them](https://github.com/microsoft/vscode/issues/42994) (post for windows, see comments for linux)
- [Get VSC extensions list](https://stackoverflow.com/questions/35773299/how-can-you-export-the-visual-studio-code-extension-list)
- my VSC extensions

  - ```txt
    13xforever.language-x86-64-assembly
    aaron-bond.better-comments
    akashrajkn.language-netlogo-code
    bungcip.better-toml
    DavidAnson.vscode-markdownlint
    formulahendry.code-runner
    GitHub.remotehub
    icrawl.discord-vscode
    llvm-vs-code-extensions.vscode-clangd
    matklad.rust-analyzer
    mitaki28.vscode-clang
    ms-dotnettools.csharp
    ms-python.python
    ms-python.vscode-pylance
    ms-toolsai.jupyter
    ms-toolsai.jupyter-keymap
    ms-toolsai.jupyter-renderers
    ms-vscode-remote.remote-ssh
    ms-vscode-remote.remote-ssh-edit
    ms-vscode.cmake-tools
    ms-vscode.cpptools
    ms-vscode.remote-repositories
    ms-vsliveshare.vsliveshare
    ritwickdey.live-sass
    ritwickdey.LiveServer
    serayuzgur.crates
    stevencl.addDocComments
    thekalinga.bootstrap4-vscode
    tomoki1207.pdf
    twxs.cmake
    vadimcn.vscode-lldb
    WallabyJs.quokka-vscode
    yzhang.markdown-all-in-one
    ```

#### 2.1.2. VSC debugger

1. First make a task work (just compiles the code): Terminal > Configure Default Build Task
   1. (gcc-10 works well)  
2. Make necessary changes in tasks.json, then try to run it to test it: Terminal > Run Task…
   1. (Choose the task you just created)  
3. Then make the debugger configuration, by going to the debugger panel and selecting “run and debug”  
   1. (gcc-10)  
4. And make necessary changes in launcher.json now  
5. These files are inside a .vscode folder  

#### 2.1.3. VSC - OSS (Open source Visual Studio `code`)

- Make Live share work in Open source VSC (OSS)(in manjaro get from `pamac-manager` (add/remove software)):  
- Install `code-marketplace` from the AUR.
- [To share terminals add lines to product.json](https://github.com/MicrosoftDocs/live-share/issues/262)
  - ([find files location](https://stackoverflow.com/questions/5905054/how-can-i-recursively-find-all-files-in-current-and-subfolders-based-on-wildcard) with `find . 2>/dev/null -print | grep -i 'product.json'`) (`2>/dev/null` [hides premission errors](https://stackoverflow.com/questions/762348/how-can-i-exclude-all-permission-denied-messages-from-find))
  - (or `tree -P 'product.json' --prune`)
  - If the share button isn't doing anything you might have to `yay -S icu69` saw in [here](https://github.com/MicrosoftDocs/live-share/issues/4650)

#### 2.1.4. VSC - Remote Development (with ssh)

- Install the `Remote Development` extension pack
- Refer to [ssh without password section](#224-ssh-without-password-public--private-keys) for ssh configuration
- If you want X11 forwarding to your client PC you seemingly need, not one, but booth following options(see [forward gui X11 ssh section](#226-forward-gui-x11-forwarding) for more details):

  ```bash
  ForwardX11          yes
  ForwardX11Trusted   yes
  ```

#### 2.1.5. [Fix Live share in Manjaro](https://github.com/MicrosoftDocs/live-share/issues/4650)

### 2.2. ssh (in lan)

#### 2.2.1. Install in Manjaro

Will already be able to access after a reboot from any computer.

1. `sudo pacman -S openssh`
2. `sudo systemctl enable sshd`
3. `sudo systemctl start sshd`

#### 2.2.2. Access through another PC

1. in your host see the local IP with `ifconfig`
2. in your other PC in the same LAN do `ssh <UserName>@<Ipv4>` like `ssh yeshey@192.168.0.101`

#### 2.2.3. Access through phone

1. You can try installing *Termius* from the *F-Droid* store

#### 2.2.4. ssh without password (public & private keys)

1. [Best video on setting it up](https://youtu.be/lKXMyln_5q4)
2. After that you can Ex: `ssh -i ~/.ssh/my_identity pi@192.168.12.230` without a pass
3. This way you can also connect to the server with VSC

#### 2.2.5. ssh config file (`~/.ssh/config`)

1. Access the file `~/.ssh/config`
2. Here is an example of config file:

   ```bash
    IdentityFile  ~/.ssh/my_identity

    Host raspberry
        HostName      192.168.12.230
        User          pi
        ForwardX11    yes
        ForwardX11Trusted    yes
   ```

   You usually only have one IdentityFile and add it to the beginning of the config file like so  
   You can have multiple of these blocks for several configurations
3. Now you can `ssh raspberry` and it will apply all the configurations, manually you'd have to run `ssh -X -Y -i ~/.ssh/my_identity pi@192.168.12.230`

- You can also do this with ssh agents (might be a way to bypass password when your keys have pass)
  - The agent is run with `eval $(ssh-agent)` & key added with `ssh-add ~/.ssh/my_identity`
   1. But this isn't persistent after reboots, better is too
      1. Add this to `~/.bashrc` (or `~/.zshrc` if using zsh)

      ```bash
      #Starting SSH authentication agent, so we don't need to run < eval $(ssh-agent) >, run ssh-add before starting to work
      SSH_ENV="$HOME/.ssh/agent-environment"

      function start_agent {
          echo "Initialising new SSH agent..."
          /usr/bin/ssh-agent | sed 's/^echo/#echo/' > "${SSH_ENV}"
          echo succeeded
          chmod 600 "${SSH_ENV}"
          . "${SSH_ENV}" > /dev/null
          #/usr/bin/ssh-add;
      }
      # Source SSH settings, if applicable
      if [ -f "${SSH_ENV}" ]; then
          . "${SSH_ENV}" > /dev/null
          #ps ${SSH_AGENT_PID} doesn't work under cywgin
          ps -ef | grep ${SSH_AGENT_PID} | grep ssh-agent$ > /dev/null || {
              start_agent;
          }
      else
          start_agent;
      fi
      ```

      2. Add `IdentityFile ~/.ssh/my_identity` to the top of `~/.ssh/config` to tell what your key is.

#### 2.2.6. Forward GUI (X11 forwarding)

1. Note that on the **server-side** you might have to set `X11Forwarding yes` in `/etc/ssh/sshd_config` as explained [here](https://unix.stackexchange.com/questions/12755/how-to-forward-x-over-ssh-to-run-graphics-applications-remotely)
2. you can add the `-X` or `-Y` options when connecting  
   `-Y` corresponds to `ForwardX11Trusted yes` in the config file, and is secure forwarding (several features might not work in the gui application)  
   `-X` corresponds to `ForwardX11 yes` in the config file, and is full forwarding  

### 2.3. VMs  

#### 2.3.1. VirtualBox 

##### 2.3.1.1. Host Manjaro

- [Make Virtual Box work in arch with USB devices](https://forum.manjaro.org/t/virtualbox-usb-devices-arent-recognized/57361/2):
  1. Install it normally through `pamac-manager` (Add/Remove software)
  2. Install `virtualbox-ext-oracle` package
  3. Add user to vboxusers: `sudo gpasswd -a $USER vboxusers`

#### 2.3.2. Virtual Machine Manager / virt-manager (comes with KDE)

- [When you install a new VM, it will install with legacy BIOS boot per default, I recomend setting UEFI, specially if you're going to be messing with partitions](https://ostechnix.com/enable-uefi-support-for-kvm-virtual-machines-in-linux/)
- To [enable USB redirection](https://github.com/NixOS/nixpkgs/issues/106594) you need to add `virtualisation.spiceUSBRedirection.enable = true;` to the host machine in nixOS
- [For Clipboard sharing & Auto-resize the VM machine](https://www.youtube.com/watch?v=h5IJMJYEj8I), install in the guest system `spice-vdagent`. Or add `services.spice-vdagentd.enable = true;` in nixOS. WIth this you can in virt-manager go to View > Scale-Display > tick Auto resize VM with window to do exactly that.
- About the error <font color="red"><i>Network "Default" not active in virt-manager</i></font>, you need to start the "Default" network, [do that](https://www.youtube.com/watch?v=dF32UgEPGKE&t=2s) with this command: `sudo virsh net-start default`, you can try to [make it autostart](https://serverfault.com/questions/577209/how-to-automatically-start-virtual-networks-using-virsh) with this: `sudo virsh net-autostart default`(untested) 
- [Check this](https://unix.stackexchange.com/questions/669536/unable-to-get-live-usb-to-boot) to start a virtual machine from virt-manager from a USB device.
  
#### 2.3.3. [Guest Manjaro](https://forum.manjaro.org/t/root-tip-virtualbox-installation-usb-shared-folder/1178)

1. `sudo pacman -Syu virtualbox-guest-utils`  
2. `sudo gpasswd -a $USER vboxsf`  
3. `sudo systemctl enable --now vboxservice`
4. `reboot`

#### 2.3.4. [SSH into Guest Manjaro](https://averagelinuxuser.com/ssh-into-virtualbox/)

1. [Install OpenSSH:](https://tuxfixer.com/configure-ssh-service-in-manjaro-linux/)
    1. `sudo pacman -S openssh`
    2. `sudo systemctl enable sshd.service`
    3. `sudo systemctl start sshd.service`
2. Go to VM settings > Network > Adapter 1 > Advanced > Port Forwarding and set:
    1. Name: ssh (or whatever you like)
    2. Protocol: TCP
    3. Host Port: 2222 (or any other port you like)
    4. Guest port: 22
3. Then connect from the host OS with `ssh -p 2222 yeshey@localhost`
   Or add to `C:\Users\yeshe\.ssh\config`: (or by pressing F1 and selecting `Remote-SSH: Open SSH configuration File...`)

   ```txt
   Host vm
    HostName localhost
    User yeshey
    Port 2222
   ```
#### 2.3.5. High Performance VMs

- Here is your current xml configuration for youw Windows PC with nvidia Vgpu according to [your module](https://github.com/Yeshey/nixos-nvidia-vgpu_nixOS): 
  ```xml
  <domain xmlns:qemu="http://libvirt.org/schemas/domain/qemu/1.0" type="kvm">
  <name>win10</name>
  <uuid>7412b302-dae5-46a7-a9d3-c849658e4897</uuid>
  <metadata>
    <libosinfo:libosinfo xmlns:libosinfo="http://libosinfo.org/xmlns/libvirt/domain/1.0">
      <libosinfo:os id="http://microsoft.com/win/10"/>
    </libosinfo:libosinfo>
  </metadata>
  <memory unit="KiB">11776000</memory>
  <currentMemory unit="KiB">11776000</currentMemory>
  <vcpu placement="static">8</vcpu>
  <cputune>
    <vcpupin vcpu="0" cpuset="4"/>
    <vcpupin vcpu="1" cpuset="5"/>
    <vcpupin vcpu="2" cpuset="6"/>
    <vcpupin vcpu="3" cpuset="7"/>
    <vcpupin vcpu="4" cpuset="8"/>
    <vcpupin vcpu="5" cpuset="9"/>
    <vcpupin vcpu="6" cpuset="10"/>
    <vcpupin vcpu="7" cpuset="11"/>
  </cputune>
  <os>
    <type arch="x86_64" machine="pc-q35-7.1">hvm</type>
    <loader readonly="yes" type="pflash">/run/libvirt/nix-ovmf/OVMF_CODE.fd</loader>
    <nvram template="/run/libvirt/nix-ovmf/OVMF_VARS.fd">/var/lib/libvirt/qemu/nvram/win10_VARS.fd</nvram>
  </os>
  <features>
    <acpi/>
    <apic/>
    <hyperv mode="custom">
      <relaxed state="on"/>
      <vapic state="on"/>
      <spinlocks state="on" retries="8191"/>
    </hyperv>
    <vmport state="off"/>
  </features>
  <cpu mode="host-passthrough" check="none" migratable="on">
    <topology sockets="1" dies="1" cores="4" threads="2"/>
  </cpu>
  <clock offset="localtime">
    <timer name="hpet" present="yes"/>
    <timer name="hypervclock" present="yes"/>
  </clock>
  <on_poweroff>destroy</on_poweroff>
  <on_reboot>restart</on_reboot>
  <on_crash>destroy</on_crash>
  <pm>
    <suspend-to-mem enabled="no"/>
    <suspend-to-disk enabled="no"/>
  </pm>
  <devices>
    <emulator>/run/libvirt/nix-emulators/qemu-system-x86_64</emulator>
    <disk type="file" device="disk">
      <driver name="qemu" type="qcow2"/>
      <source file="/mnt/DataDisk/AppFiles/interchangeable/VMs/Windows/win10.qcow2"/>
      <target dev="vda" bus="virtio"/>
      <boot order="1"/>
      <address type="pci" domain="0x0000" bus="0x04" slot="0x00" function="0x0"/>
    </disk>
    <disk type="file" device="cdrom">
      <driver name="qemu" type="raw"/>
      <source file="/mnt/DataDisk/AppFiles/interchangeable/VMs/Windows/Win11_22H2_EnglishInternational_x64v1.iso"/>
      <target dev="sdb" bus="sata"/>
      <readonly/>
      <address type="drive" controller="0" bus="0" target="0" unit="1"/>
    </disk>
    <disk type="file" device="cdrom">
      <driver name="qemu" type="raw"/>
      <source file="/mnt/DataDisk/AppFiles/interchangeable/VMs/Windows/virtio-win-0.1.215.iso"/>
      <target dev="sdc" bus="sata"/>
      <readonly/>
      <address type="drive" controller="0" bus="0" target="0" unit="2"/>
    </disk>
    <controller type="usb" index="0" model="qemu-xhci" ports="15">
      <address type="pci" domain="0x0000" bus="0x02" slot="0x00" function="0x0"/>
    </controller>
    <controller type="pci" index="0" model="pcie-root"/>
    <controller type="pci" index="1" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="1" port="0x10"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x02" function="0x0" multifunction="on"/>
    </controller>
    <controller type="pci" index="2" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="2" port="0x11"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x02" function="0x1"/>
    </controller>
    <controller type="pci" index="3" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="3" port="0x12"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x02" function="0x2"/>
    </controller>
    <controller type="pci" index="4" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="4" port="0x13"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x02" function="0x3"/>
    </controller>
    <controller type="pci" index="5" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="5" port="0x14"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x02" function="0x4"/>
    </controller>
    <controller type="pci" index="6" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="6" port="0x15"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x02" function="0x5"/>
    </controller>
    <controller type="pci" index="7" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="7" port="0x16"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x02" function="0x6"/>
    </controller>
    <controller type="pci" index="8" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="8" port="0x17"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x02" function="0x7"/>
    </controller>
    <controller type="pci" index="9" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="9" port="0x18"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x03" function="0x0" multifunction="on"/>
    </controller>
    <controller type="pci" index="10" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="10" port="0x19"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x03" function="0x1"/>
    </controller>
    <controller type="pci" index="11" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="11" port="0x1a"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x03" function="0x2"/>
    </controller>
    <controller type="pci" index="12" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="12" port="0x1b"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x03" function="0x3"/>
    </controller>
    <controller type="pci" index="13" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="13" port="0x1c"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x03" function="0x4"/>
    </controller>
    <controller type="pci" index="14" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="14" port="0x1d"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x03" function="0x5"/>
    </controller>
    <controller type="pci" index="15" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="15" port="0x1e"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x03" function="0x6"/>
    </controller>
    <controller type="pci" index="16" model="pcie-to-pci-bridge">
      <model name="pcie-pci-bridge"/>
      <address type="pci" domain="0x0000" bus="0x0a" slot="0x00" function="0x0"/>
    </controller>
    <controller type="sata" index="0">
      <address type="pci" domain="0x0000" bus="0x00" slot="0x1f" function="0x2"/>
    </controller>
    <controller type="virtio-serial" index="0">
      <address type="pci" domain="0x0000" bus="0x03" slot="0x00" function="0x0"/>
    </controller>
    <interface type="network">
      <mac address="52:54:00:00:06:6c"/>
      <source network="default"/>
      <model type="virtio"/>
      <address type="pci" domain="0x0000" bus="0x01" slot="0x00" function="0x0"/>
    </interface>
    <serial type="pty">
      <target type="isa-serial" port="0">
        <model name="isa-serial"/>
      </target>
    </serial>
    <console type="pty">
      <target type="serial" port="0"/>
    </console>
    <channel type="spicevmc">
      <target type="virtio" name="com.redhat.spice.0"/>
      <address type="virtio-serial" controller="0" bus="0" port="1"/>
    </channel>
    <channel type="spiceport">
      <source channel="org.spice-space.webdav.0"/>
      <target type="virtio" name="org.spice-space.webdav.0"/>
      <address type="virtio-serial" controller="0" bus="0" port="2"/>
    </channel>
    <input type="mouse" bus="ps2"/>
    <input type="keyboard" bus="ps2"/>
    <graphics type="spice" autoport="yes">
      <listen type="address"/>
      <image compression="off"/>
    </graphics>
    <sound model="ich9">
      <address type="pci" domain="0x0000" bus="0x00" slot="0x1b" function="0x0"/>
    </sound>
    <audio id="1" type="spice"/>
    <video>
      <model type="none"/>
    </video>
    <hostdev mode="subsystem" type="mdev" managed="no" model="vfio-pci" display="on">
      <source>
        <address uuid="ce851576-7e81-46f1-96e1-718da691e53e"/>
      </source>
      <address type="pci" domain="0x0000" bus="0x05" slot="0x00" function="0x0"/>
    </hostdev>
    <hostdev mode="subsystem" type="usb" managed="yes">
      <source>
        <vendor id="0x8087"/>
        <product id="0x0aaa"/>
      </source>
      <address type="usb" bus="0" port="5"/>
    </hostdev>
    <redirdev bus="usb" type="spicevmc">
      <address type="usb" bus="0" port="2"/>
    </redirdev>
    <redirdev bus="usb" type="spicevmc">
      <address type="usb" bus="0" port="4"/>
    </redirdev>
    <redirdev bus="usb" type="spicevmc">
      <address type="usb" bus="0" port="1"/>
    </redirdev>
    <redirdev bus="usb" type="spicevmc">
      <address type="usb" bus="0" port="3"/>
    </redirdev>
    <watchdog model="itco" action="reset"/>
    <memballoon model="none"/>
    <shmem name="looking-glass">
      <model type="ivshmem-plain"/>
      <size unit="M">64</size>
      <address type="pci" domain="0x0000" bus="0x10" slot="0x01" function="0x0"/>
    </shmem>
  </devices>
  <qemu:capabilities>
    <qemu:del capability="usb-host.hostdevice"/>
  </qemu:capabilities>
</domain>
  ```

### 2.4. Vivaldi

#### 2.4.1. Search Engines

- Url for searching Google maps with shortcut: `{google:baseURL}maps/place/search?q=%s&{google:originalQueryForSuggestion}{google:prefetchSource}{google:sourceId}{google:contextualSearchVersion}ie={inputEncoding}`

---

## 3. Coding Languages

---

### 3.1. MarkDown

#### 3.1.1. [MarkDown CheatSheet](https://www.markdownguide.org/cheat-sheet/)  

#### 3.1.2. Extensions for md

- [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint) for warnings & sugestions
- [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) for more features

#### 3.1.3. Markdown title into an HTML anchor

- Refer to [these](https://stackoverflow.com/questions/43273842/what-are-the-rules-of-converting-one-markdown-title-into-an-html-anchor) rules
- For example, the title `#### 2.2.4. ssh without password (public & private keys)` gets turned to `#224-ssh-without-password-public--private-keys`.  
So, [this link to section 2.2.4](#224-ssh-without-password-public--private-keys) is formated like so:  
`[section 2.2.4](#224-ssh-without-password-public--private-keys)`

---

### 3.2. LaTeX

- [Learn LaTeX in overleaf](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes)
- Use [overleaf](https://www.overleaf.com) for simultanious work
- [Discord Server link about latex](https://discord.com/channels/584139918822080543/994917160709275738)
- [OverLeaf's IEEE official IEEE templates](https://www.overleaf.com/gallery/tagged/ieee-official)
- Also have [LatexTemplates.com](https://latextemplates.com)
- OverLeaf's template:

  ```tex
  \documentclass{article}
  \usepackage[utf8]{inputenc}

  \title{Embedded Machine Learning Report}
  \author{yesheysangpo}
  \date{August 2022}

  \begin{document}

  \maketitle

  \section{Introduction}

  \end{document}
  ```

- My main.tex Template Report:
  
  ```tex
  \documentclass[10pt]{article}
  % -------------------------------------------------------------------
  % Pacotes básicos
  \usepackage[english]{babel}										% Idioma a ser usado
                                                                  % Trocar "english" para "brazil" para artigos escritos em língua portuguesa 
  \usepackage[utf8]{inputenc}										% Escrita de caracteres acentuados e cedilhas - 1
  \usepackage[T1]{fontenc}										% Escrita de caracteres acentuados + outros detalhes técnicos fundamentais
  % -------------------------------------------------------------------
  % Pacotes matemáticos
  \usepackage{amsmath,amsfonts,amssymb,amsthm,cancel,siunitx,
  calculator,calc,mathtools,empheq,latexsym}
  % -------------------------------------------------------------------
  % Pacotes para inserção de figuras e subfiguras
  \usepackage{subfig,epsfig,tikz,float}		            % Packages de figuras. 
  % -------------------------------------------------------------------
  % Pacotes para inserção de tabelas
  \usepackage{booktabs,multicol,multirow,tabularx,array}          % Packages para tabela
  % -------------------------------------------------------------------
  \usepackage{float}
  \usepackage{biblatex}
  \usepackage[colorlinks=true, allcolors=blue]{hyperref}
  \usepackage{lipsum}

  % trying to How can one keep a \section from being at the end of a page?
  % \usepackage[nobottomtitles*]{titlesec}

  % -------------------------------------------------------------------
  % Definition of lengths
  \setlength{\parskip}{5pt}
  \textwidth 13.5cm
  \textheight 19.5cm
  \columnsep .5cm
  % -------------------------------------------------------------------
  % Title of the Article
  \title{\renewcommand{\baselinestretch}{1.17}\normalsize\bf%
  \uppercase{Embedded American Sign Letters Recognition in  Raspberry Pi}
  }
  % -------------------------------------------------------------------
  % Authors
  \author{%
  João Almeida\\
  Joao.SilvadeAlmeida@haw-hamburg.de
  }
  % -------------------------------------------------------------------

  % Begin Document

  \begin{document}

  \date{}

  \maketitle

  \vspace{-0.5cm}

  \begin{center}
  {\footnotesize 
  HAW Hamburg, Dept. for Computer Science \\
  }
  \end{center}

  % -------------------------------------------------------------------
  % Abstract
  \bigskip
  \noindent
  \begin{abstract}
    Training of a object detection model with TensorFlow for deployment on an Embedded Raspberry Pi system for recognition of American sign language letters from the camera's image.
  %	\lipsum[2-4]
  \end{abstract}

  \medskip
  \noindent
  {\small{\bf Keywords}{:} 
  computer vision, tensorflow, classification, raspberry pi, python, object detection, machine learning, opencv
  }

  \baselineskip=\normalbaselineskip

  \pagebreak
  \tableofcontents
  \pagebreak
  % -------------------------------------------------------------------

  \section{Introduction}\label{sec:1}

    \lipsum[1-1]

    \pagebreak

  \section{Approach and Architecture}\label{sec:2}

    \lipsum[65-66]

  \section{Training and Test Data-set}\label{sec:3}

    \lipsum[65-66]

    \begin{figure}[H]
      \centering
      \includegraphics[scale=0.4]{example-image-c}
      \caption{Goal of the image preprocessing.}\label{fig:preprocessing-goal}
    \end{figure}

    \subsection{Color Space Conversion}

      \lipsum[65]

    \subsection{Gaussian Blur}

      \lipsum[65] $\frac{1}{25}$

      \begin{figure}[H]
        \centering
        \includegraphics[scale=0.6]{example-image-b}
        \caption{Application of the Gaussian blur.}\label{fig:gaussian-blur}
      \end{figure}

    \subsection{Canny Edge Detection}

      \lipsum[65] $\frac{\pi}{180}$

      \begin{figure}[H]
        \centering
        \includegraphics[scale=0.15]{example-image-a}
        \caption{Example application of the Canny Edge detection technique.}\label{fig:canny-edge}
      \end{figure}

    \subsection{Clustering}

      \lipsum[65]

  \section{Deployment in the Raspberry Pi}\label{sec:4}

    \lipsum[75]

  \subsection{Architecture}

    \lipsum[10-11]

    \begin{table}[H]
      \centering
      \begin{tabular}{||c c c c||} 
        \hline
        N & Layer & N Filters/Units & Pool/Kernel Size \\ [0.5ex] 
        \hline\hline
        1 & Conv2D & 32 & 5 x 5\\ 
        \hline
        2 & MaxPooling2D & - & 2 x 2 \\
        \hline
        3 & Conv2D & 64 & 5 x 5 \\
        \hline
        4 & MaxPooling2D & - & 2 x 2 \\
        \hline
        5 & Dropout & - & - \\ [1ex] 
        \hline
        6 & Flatten & - & - \\ [1ex] 
        \hline
        7 & Dense & 128 & - \\ [1ex] 
        \hline
        8 & Dropout & - & - \\ [1ex] 
        \hline
        9 & Dense & 64 & - \\ [1ex] 
        \hline
        10 & Dense & 13 & - \\ [1ex] 
        \hline
      \end{tabular}
      \caption{\label{tab:cnn-architecture}CNN layer architecture.}
    \end{table}

    \pagebreak

    \subsection{Dataset}

      To escape text: $\textit{image\_dataset\_from\_directory}$.

      Citation \cite{1}

      \begin{figure}[H]
        \centering
        \begin{minipage}[b]{0.25\textwidth}
          \includegraphics[width=\textwidth]{example-image-a}
          \caption{Multiple dataset image examples.}
        \end{minipage}
        \hfill
        \begin{minipage}[b]{0.65\textwidth}
          \includegraphics[width=\textwidth]{example-image-b}
          \caption{Image distribution in the dataset.}
        \end{minipage}
      \end{figure}


    \subsection{Training and Validation}

      \lipsum[65-66]

      \pagebreak

  \section{Practical Study}

    \lipsum[65]

    \begin{figure}[H]
      \centering
      \includegraphics[scale=1]{example-image-a}
      \caption{Usage of the application.}\label{fig:usage}
    \end{figure}

    \pagebreak

  \section{Conclusions}\label{sec:5}

    \lipsum[1-2]

  \newpage

  % There is a better way to do the bibliography for sure
  \begin{thebibliography}{9}
    \bibitem{1}
    \href{https://en.wikipedia.org/wiki/Convolutional_neural_network}{Wikipedia. Convolutional Neural Network. (Access date: 04.03.2022) [Online]}
    
    \bibitem{2}
    \href{https://viso.ai/edge-ai/tensorflow-lite/}{Viso.ai. TensorFlow-Lite. (Access date: 04.03.2022) [Online]}
    
    \bibitem{3}
    \href{https://keras.io/guides/sequential_model/}{Keras.io. Sequential Model. (Access date: 04.03.2022) [Online]}
    
    \bibitem{4}
    \href{https://towardsdatascience.com/board-game-image-recognition-using-neural-networks-116fc876dafa}{TowardsDataScience. Board Game Image Recognition. (Access date: 04.03.2022) [Online]}
  \end{thebibliography}

  \end{document}
  ```

### 3.3. Python

#### 3.3.1. Dependencies

- [Automatically create requirements.txt](https://stackoverflow.com/questions/31684375/automatically-create-requirements-txt):  
  - `pip install pipreqs`  
  - Navigate to the project folder  
  - `pipreqs .\`

- Automatically install dependencies:  
`pip install -r requirements.txt`

## 4. Others

### 4.1. Camera (EOS 1100D)

#### 4.1.1. Timelapse

- Connected to computer:
  1. [Install EOS Utility](https://hk.canon/en/support/0200584002)
  2. Take photos in intervals by connecting the camera to the PC
  3. [Use EOS Utility](https://www.youtube.com/watch?v=lkQO0V9j0ac)
- Installing Magic lantern software in Camera
  1. [Make sure it has firmware 1.0.5](https://drivers.softpedia.com/get/SCANNER-Digital-CAMERA-WEBCAM/CANON/Canon-EOS-1100D-DSLR-Firmware-105.shtml)  
  2. [Tutorial on how to install Magic Lantern](https://www.youtube.com/watch?v=6s7_ZO6ELUs), see [here](https://www.youtube.com/watch?v=33Q17zd-0nE) to know where to put the files in the SD card
  3. [Tutorial on timelapse with magic Lantern](https://www.youtube.com/watch?v=1mB_hv3b05Y)
- Turn off autofocuse on a button in front on the lens that you can switch between AF(auto focuse) and MF (manual focuse)

### 4.2. Programs to Install

#### 4.2.1. Android

- Entertainment:
  - Tachiyomi (install from F-droid | manga reader)
  - (Old Manga sites: [Solo Leveling](https://www.mangago.me/read-manga/solo_leveling/?rmgU), https://www.mangago.me/, https://mangakakalot.com/)
  - Charades (group game)
  - Ludo King (4 people game)
  - Micro Battles (1/2/3) (2 people)
  - 4 in a row (2 people)
  - Chess Clock (to play irl chess)
  - Clash Royale
  - InfiniRoom
- Social:
  - Discord
  - Twitter
  - Messenger
  - Signal
  - Whatsapp
  - Instagram
  - Telegram
  - SnapChat
  - [Facebook](https://www.facebook.com) as a link
  - Tinder / Bumble / OKCupid
- Social & Work
  - MS Teams
  - Gmail
  - Outlook (Browser shortcut)
- Explorers:
  - YouTube Vanced / Vanced Manager
  - NewPipe
  - LBRY
  - F-Droid
  - PlayStore
  - Maps
  - Vivaldi Browser
  - Tor Brwoser
- Utilities:
  - Google Keep
  - Google Docs
  - Mini Scanner
  - Google Calendar
  - Shazam
  - Sleep Android
  - Lens
  - DroidCam
  - [Google Translate](https://translate.google.com) (as a link)
- Tech Utils:
  - Bitwarden
  - andOTP
  - FX file explorer
  - F-Droid 
  - Syncthing
  - DiskUsage
  - Github (Browser version)
- Sys/Geek:
  - Termux
  - Sync.ME
  - Hacker's Keyboard (anysoft keyboard? Find better)
  - Vanced Manager
  - Shortcut to whatsappp garbadge (/storage/emulated/0/Android/media/com.whatsapp/WhatsApp/Media)
  - Magisk
- Media:
  - vlc
  - Blackplayer
  - Gallery
  - (Spotify, Netflix, Radio, Photos)
- Money:
  - Caixadirecta
  - MB WAY
  - PayPal
  - Revolut
  - Exodus
  - Too Good To Go
- ✈️🚌🍔🏠🌴:
  - TAP Portugal
  - CP Portugal
  - Bolt
  - Uber
  - Geocashing
  - Miles (car sharing)
  - Moovit
  - Waze (For driving)
- Self Improve:
  - Duolingo
  - Anki
  - Daylio
  - Home Workout
- Discounts/🎁:
  - Cartao Continente
  - Burger King
  - MC Donalds
- Gamezy:
  - MTG Carbon
  - MTG Companion
  - Free PC Games
- Others
  - Soundcorset Tuner & Metronome

#### 4.2.2. Surface (Windows)

- Notepad++
- 7zip
- Visual Studio Code
- VLC Media Player
- OBS Studio
- Anki
- Python
- ffmpeg
- WinDirStat
- Stremio
- Discord
- VBCable, the Virtual Audio Cable
- Oracle Virtual Box
- Blender
- Inkscape
- GIMP
- SyncTrazor
- AnyDesk
- Tor Browser
- Vivaldi Browser
- 4k Video Downloader
- Microsoft Office
- Git
- GitHub Desktop
- Java
- Barrier (to control from linux too)
- (OpenVPN)
- qBittorrent

  - More, For PC:
- AOMEI Partition Assistent
- Lenovo Vantage
- GeForce Experience (for Nvidia drivers)

##### 4.2.2.1. Installing only some apps of Office

You need to do some hacky stuff to get this done.

- [Follow this video](https://www.youtube.com/watch?v=1g0fHoojWuE)
- This is the resulting configuration file to install word and excel with your business account:

  ```xml
  <Configuration ID="0f7a1395-691d-452b-bf60-305f88fdc99b">
    <Add OfficeClientEdition="64" Channel="Current">
      <Product ID="O365BusinessRetail">
        <Language ID="en-gb" />
        <ExcludeApp ID="Access" />
        <ExcludeApp ID="Groove" />
        <ExcludeApp ID="Lync" />
        <ExcludeApp ID="OneDrive" />
        <ExcludeApp ID="OneNote" />
        <ExcludeApp ID="Outlook" />
        <ExcludeApp ID="PowerPoint" />
        <ExcludeApp ID="Publisher" />
        <ExcludeApp ID="Teams" />
      </Product>
    </Add>
    <Updates Enabled="TRUE" />
    <RemoveMSI />
    <Display Level="Full" AcceptEULA="TRUE" />
  </Configuration>
  ```

#### 4.2.3. Linux

- PDF Arranger
