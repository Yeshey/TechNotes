<h1> TechNotes

<h2> Table Of Contents

- [1. OSs](#1-oss)
  - [1.1. **Linux**](#11-linux)
    - [1.1.1. Autostart Tasks](#111-autostart-tasks)
  - [1.2. **Windows**](#12-windows)
  - [1.3. **Android**](#13-android)
- [2. Programs](#2-programs)
  - [2.1. VSC](#21-vsc)
  - [2.2. VirtualBox VMs](#22-virtualbox-vms)
- [3. Coding Languages](#3-coding-languages)
  - [3.1. MarkDown](#31-markdown)
  - [3.2. Python](#32-python)
    - [3.2.1. Dependencies](#321-dependencies)

## 1. OSs

---

### 1.1. **Linux**

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

---

### 1.2. **Windows**

---

### 1.3. **Android**

## 2. Programs

### 2.1. VSC

### 2.2. VirtualBox VMs 

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
