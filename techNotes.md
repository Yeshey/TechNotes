<h1> TechNotes

<h2> Table Of Contents

- [1. OSs](#1-oss)
  - [1.1. **Linux** (Manjaro)](#11-linux-manjaro)
    - [1.1.1. Autostart Tasks](#111-autostart-tasks)
    - [1.1.2. PDFs](#112-pdfs)
      - [1.1.2.1. Unite](#1121-unite)
      - [1.1.2.2. OCR (Manjaro)](#1122-ocr-manjaro)
      - [1.1.2.3. Compress](#1123-compress)
    - [1.1.3. Button To Boot into Windows](#113-button-to-boot-into-windows)
    - [1.1.4. Ohmy - zsh (instead of bash)](#114-ohmy---zsh-instead-of-bash)
  - [1.2. **Windows**](#12-windows)
  - [1.3. **Android**](#13-android)
- [2. Programs](#2-programs)
  - [2.1. VSC](#21-vsc)
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

- gs -sDEVICE=pdfwrite -dPDFSETTINGS=/ebook -q -o output.pdf file.pdf

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
- [my `.zshrc` configuration](https://github.com/Yeshey/Linux_config/blob/main/.zshrc)

---

### 1.2. **Windows**

---

### 1.3. **Android**

## 2. Programs

### 2.1. VSC

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
