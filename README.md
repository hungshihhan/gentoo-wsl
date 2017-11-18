### Gentoo overlay for Windows Subsystem for Linux (WSL)

This repository contains patches for running Gentoo on WSL. 

#### Installing Gentoo on WSL

Following the instruction https://wiki.archlinux.org/index.php/Install_on_WSL, first install any of WSL apps from Windows store. 

1. Installing a Linux instance: Execute the app and wait for the download to complete. Close window when prompt asks new user name. 
2. Download Gentoo stage3: Run app again, create folder `/root/stage3` download Gentoo  through `https://www.gentoo.org/downloads`. Untar to the folder and close window when done. 
3. Navigate to `%localappdata%\Packages\appname\LocalState\rootfs` in Windows File Explorer and delete `bin`, `etc`, `lib`, `lib64`, `sbin`, `usr` and `var`. Move these folders under `%localappdata%\Packages\appname\LocalState\rootfs\root\stage3` as replacement. 
4. Run app again, create new users in shell and change default user with command `ubuntu config --default-user username`.
