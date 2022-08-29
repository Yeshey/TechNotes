<h1> TechNotes

<h2> Table Of Contents

- [1. OSs](#1-oss)
  - [1.1. **Linux** (Manjaro)](#11-linux-manjaro)
    - [1.1.1. Autostart Tasks](#111-autostart-tasks)
    - [1.1.2. PDFs](#112-pdfs)
      - [1.1.2.1. Unite](#1121-unite)
      - [1.1.2.2. OCR (Manjaro)](#1122-ocr-manjaro)
      - [1.1.2.3. Compress](#1123-compress)
    - [1.1.3. Latte Dock](#113-latte-dock)
    - [1.1.4. Notifications](#114-notifications)
      - [1.1.4.1. Fix notifications error in latte dock](#1141-fix-notifications-error-in-latte-dock)
      - [1.1.4.2. Notification badges in electron apps (like discord)](#1142-notification-badges-in-electron-apps-like-discord)
      - [1.1.4.3. Send linux OS notifications through terminal/console/cli](#1143-send-linux-os-notifications-through-terminalconsolecli)
    - [1.1.5. Button To Boot into Windows in a dual boot](#115-button-to-boot-into-windows-in-a-dual-boot)
    - [1.1.6. Ohmy - zsh (instead of bash)](#116-ohmy---zsh-instead-of-bash)
    - [1.1.7. Use laptop as a second monitor](#117-use-laptop-as-a-second-monitor)
    - [1.1.8. CLI Search / find words](#118-cli-search--find-words)
    - [1.1.9. Hotspot](#119-hotspot)
      - [1.1.9.1. linux-wifi-hotspot](#1191-linux-wifi-hotspot)
    - [1.1.10. Image Manipulation](#1110-image-manipulation)
      - [1.1.10.1. Changing Metadata](#11101-changing-metadata)
        - [1.1.10.1.1. Changing DateTime](#111011-changing-datetime)
      - [1.1.10.2. Overlaying DateTime On top of image](#11102-overlaying-datetime-on-top-of-image)
    - [1.1.11. File Systems](#1111-file-systems)
      - [1.1.11.1. BTRFS](#11111-btrfs)
    - [1.1.12. Tested in Other Linuxs](#1112-tested-in-other-linuxs)
      - [1.1.12.1. Add more resolution options (Linux Mint)](#11121-add-more-resolution-options-linux-mint)
    - [1.1.13. rsync](#1113-rsync)
  - [1.2. **Windows**](#12-windows)
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
    - [2.2.4. ssh without password (public & private keys)](#224-ssh-without-password-public--private-keys)
    - [2.2.5. ssh config file (`~/.ssh/config`)](#225-ssh-config-file-sshconfig)
    - [2.2.6. Forward GUI (X11 forwarding)](#226-forward-gui-x11-forwarding)
  - [2.3. VirtualBox VMs](#23-virtualbox-vms)
    - [2.3.1. Host Manjaro](#231-host-manjaro)
    - [2.3.2. Guest Manjaro](#232-guest-manjaro)
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

##### 1.1.2.2. OCR (Manjaro)

[see the language acronyms](https://tesseract-ocr.github.io/tessdoc/Data-Files-in-different-versions.html)

- `pip install ocrmypdf`
- `sudo pacman -Sy tesseract`
- `sudo pacman -Sy tesseract-data-eng`
- `sudo pacman -Sy tesseract-data-por`
- `ocrmypdf -l eng+por combined.pdf ok.pdf`

##### 1.1.2.3. [Compress](https://unix.stackexchange.com/questions/274428/how-do-i-reduce-the-size-of-a-pdf-file-that-contains-images)

- `gs -sDEVICE=pdfwrite -dPDFSETTINGS=/ebook -q -o output.pdf file.pdf`

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
  4. You can change the resolution of the new screen, but you're bounded by presets, as explained in [the post](https://unix.stackexchange.com/questions/559918/how-to-add-virtual-monitor-with-nvidia-proprietary-driver). The bewst we have is `xrandr --output DP-1 --mode 1600x900`

> - Other posts that helped me get here:
>   - [r/linux questions - How can I use my old laptop as second monitor](https://www.reddit.com/r/linuxquestions/comments/qp3p7a/how_can_i_use_my_old_laptop_as_second_monitor/)
>   - [r/linuxquestions - Using VNC to extend the display of desktop into laptop screen.](https://www.reddit.com/r/linuxquestions/comments/gh1307/using_vnc_to_extend_the_display_of_desktop_into/)

#### 1.1.8. CLI Search / find words

- [Find a files location through its name recursively](https://stackoverflow.com/questions/5905054/how-can-i-recursively-find-all-files-in-current-and-subfolders-based-on-wildcard):
  - `find . 2>/dev/null -print | grep -i 'product.json' 2>/dev/null` (the *2>/dev/null* [hides premission errors](https://stackoverflow.com/questions/762348/))
  - `tree -P 'product.json' --prune`
- [Find all files containing specific text on Linux](https://stackoverflow.com/questions/16956810/how-do-i-find-all-files-containing-specific-text-on-linux):
  - `grep -rnw './' -e 'pattern'`

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

#### 1.1.11. File Systems

##### 1.1.11.1. BTRFS

Supports spanning multiple drives with one file system without LVM!!

#### 1.1.12. Tested in Other Linuxs

##### 1.1.12.1. Add more resolution options (Linux Mint)  

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

#### 1.1.13. rsync

- [Command to copy ***Everything***](https://askubuntu.com/questions/117014/what-is-the-easiest-way-to-merge-and-home):
  - `sudo rsync -avz --hard-links --numeric-ids /mnt/oldhome/ /mnt/root/home`

---

### 1.2. **Windows**

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
- Refer to [section 2.2.4](#224-ssh-without-password-public--private-keys) for ssh configuration
- If you want X11 forwarding to your client PC you seemingly need, not one, but booth following options:

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

### 2.3. VirtualBox VMs  

#### 2.3.1. Host Manjaro

- [Make Virtual Box work in arch with USB devices](https://forum.manjaro.org/t/virtualbox-usb-devices-arent-recognized/57361/2):
  1. Install it normally through `pamac-manager` (Add/Remove software)
  2. Install `virtualbox-ext-oracle` package
  3. Add user to vboxusers: `sudo gpasswd -a $USER vboxusers`

#### 2.3.2. [Guest Manjaro](https://forum.manjaro.org/t/root-tip-virtualbox-installation-usb-shared-folder/1178)

1. `sudo pacman -Syu virtualbox-guest-utils`  
2. `sudo gpasswd -a $USER vboxsf`  
3. `sudo systemctl enable --now vboxservice`
4. `reboot`

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

- Hacker's Keyboard (anysoft keyboard? Find better)
- Explorers:
  - YouTube Vanced / Vanced Manager
  - NewPipe
  - LBRY
  - F-Droid
  - PlayStore
Browsers:
  - Vivaldi Browser
  - Tor Brwoser
- Self Improve:
  - Duolingo
  - Anki
  - Daylio
- Utilities:
  - vlc
  - Blackplayer
  - andOTP
  - Google Keep
  - Free PC Games
  - Mini Scanner
  - Google Calendar
  - Bitwarden
  - Syncthing
  - Shazam
  - Sleep Android
  - FX file explorer
  - Lens
  - DroidCam
  - [Google Translate](https://translate.google.com) (as a link)
- Games:
  - Charades (group game)
  - Ludo King (4 people game)
  - Micro Battles (1/2/3) (2 people)
  - 4 in a row (2 people)
  - Chess Clock (to play irl chess)
  - Clash Royale
  - InfiniRoom
- Social Media:
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
  - MS Teams
- Movin:
  - TAP Portugal
  - CP Portugal
  - Bolt
  - Uber
  - Geocashing
  - Miles (car sharing)
- Money:
  - Caixadirecta
  - MB WAY
  - PayPal
  - Revolut
  - Exodus
  - Too Good To Go
- MTG:
  - MTG Carbon
  - MTG Companion
- Discounts:
  - Cartao Continente
  - Burger King
  - MC Donalds
- Techy:
  - Termux
  - Sync.ME
- Manga / Anime:
  - [Solo Leveling](https://www.mangago.me/read-manga/solo_leveling/?rmgU)
  - https://www.mangago.me/
  - https://mangakakalot.com/
- Others
  - Soundcorset Tuner & Metronome
  - Github
  - DiskUsage
  - Home Workout

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
