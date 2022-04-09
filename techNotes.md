<h1> TechNotes

<h2> Table Of Contents

- [1. OSs](#1-oss)
  - [1.1. **Linux** (Manjaro)](#11-linux-manjaro)
    - [1.1.1. Autostart Tasks](#111-autostart-tasks)
    - [1.1.2. PDFs](#112-pdfs)
      - [1.1.2.1. Unite](#1121-unite)
      - [1.1.2.2. OCR (Manjaro)](#1122-ocr-manjaro)
      - [1.1.2.3. Compress](#1123-compress)
  - [KDE Plasma](#kde-plasma)
    - [Latte Dock](#latte-dock)
    - [1.1.3. Button To Boot into Windows](#113-button-to-boot-into-windows)
    - [1.1.4. Ohmy - zsh (instead of bash)](#114-ohmy---zsh-instead-of-bash)
    - [1.1.5. Use laptop as a second monitor](#115-use-laptop-as-a-second-monitor)
  - [1.2. **Windows**](#12-windows)
  - [1.3. **Android**](#13-android)
- [2. Programs](#2-programs)
  - [2.1. VSC (Visual Studio Code)](#21-vsc-visual-studio-code)
    - [2.1.1. VSC Extensions](#211-vsc-extensions)
    - [2.1.2. VSC debugger](#212-vsc-debugger)
    - [2.1.3. VSC - OSS (Open source Visual Studio `code`)](#213-vsc---oss-open-source-visual-studio-code)
  - [2.2. VirtualBox VMs](#22-virtualbox-vms)
    - [2.2.1. Host Manjaro](#221-host-manjaro)
    - [2.2.2. Guest Manjaro](#222-guest-manjaro)
- [3. Coding Languages](#3-coding-languages)
  - [3.1. MarkDown](#31-markdown)
  - [3.2. Python](#32-python)
    - [3.2.1. Dependencies](#321-dependencies)

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

### KDE Plasma

#### Latte Dock

- [Copy latte dock from main screen to the other monitor](https://www.reddit.com/r/kde/comments/gmgpz6/how_to_create_an_additional_latte_dock_on_second/):  
Right Click Dock in main screen > Edit Dock > Right Click it AGAIN > Edit/Add Panels > Duplicate Panel

#### 1.1.3. [Button To Boot into Windows](https://askubuntu.com/questions/42390/one-click-shutdown-ubuntu-and-load-into-alternative-bootup)

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

#### 1.1.4. Ohmy - zsh (instead of bash)

[Installation Guide](https://gist.github.com/yovko/becf16eecd3a1f69a4e320a95689249e)

- Plugins:
  - zsh-autosuggestions
- Commands:
  - Change config: `nano .zshrc`
  - Apply the changes: `source ~/.zshrc`
- [my `.zshrc` configuration](https://github.com/Yeshey/Linux_config/blob/main/.zshrc)

#### 1.1.5. Use laptop as a second monitor

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

---

### 1.2. **Windows**

---

### 1.3. **Android**

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

### 2.2. VirtualBox VMs  

#### 2.2.1. Host Manjaro

- [Make Virtual Box work in arch with USB devices](https://forum.manjaro.org/t/virtualbox-usb-devices-arent-recognized/57361/2):
  1. Install it normally through `pamac-manager` (Add/Remove software)
  2. Install `virtualbox-ext-oracle` package
  3. Add user to vboxusers: `sudo gpasswd -a $USER vboxusers`

#### 2.2.2. [Guest Manjaro](https://forum.manjaro.org/t/root-tip-virtualbox-installation-usb-shared-folder/1178)

1. `sudo pacman -Syu virtualbox-guest-utils`  
2. `sudo gpasswd -a $USER vboxsf`  
3. `sudo systemctl enable --now vboxservice`
4. `reboot`

---

## 3. Coding Languages

---

### 3.1. MarkDown

[MarkDown CheatSheet](https://www.markdownguide.org/cheat-sheet/)  
Extensions for md:

- [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint) for warnings & sugestions
- [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) for more features

---

### 3.2. Python

#### 3.2.1. Dependencies

- [Automatically create requirements.txt](https://stackoverflow.com/questions/31684375/automatically-create-requirements-txt):  
  - `pip install pipreqs`  
  - Navigate to the project folder  
  - `pipreqs .\`

- Automatically install dependencies:  
`pip install -r requirements.txt`
