### Gentoo overlay for Windows Subsystem for Linux (WSL)

This repository contains patches for running Gentoo on WSL. 

#### Installing Gentoo on WSL

The following steps basically follows the instruction https://wiki.archlinux.org/index.php/Install_on_WSL. 

1. Installing a Linux instance: Execute the app and wait for the download to complete. Close window when prompt asks new user name. 
2. Download Gentoo stage3: Run app again, create folder `/root/stage3` download Gentoo  through `https://www.gentoo.org/downloads`. Untar to the folder and close window when done. 
3. Navigate to `%localappdata%\Packages\appname\LocalState\rootfs` in Windows File Explorer and delete `bin`, `etc`, `lib`, `lib64`, `sbin`, `usr` and `var`. Move these folders under `%localappdata%\Packages\appname\LocalState\rootfs\root\stage3` as replacement. 
4. Run app again, create new users in shell and change default user with command `ubuntu config --default-user username`.

#### Issues and workarounds

1. IPC not supported https://github.com/Microsoft/WSL/issues/992: Edit `/usr/lib64/python2.7/site-packages/_emerge/AbstractEbuildProcess.py` and set `_enable_ipc_daemon` to `False`. Do so for `python3.4`. These files are installed with `sys-apps/portage`. To disable ipc support for future update,
- Add `USE="-ipc"` in `/etc/portage/make.conf` 
- Put `sys-apps/portage -ipc` in `/etc/portage/profile/package.use.force`.

2. `locale-gen` failed https://github.com/Microsoft/WSL/issues/1878:
```
localedef: ../sysdeps/unix/sysv/linux/spawni.c:360: __spawnix: Assertionec >= 0' failed.
# cd /usr/share/i18n/charmaps/
# gunzip --keep UTF-8.gz
# locale-gen
```
3. Pulseaudio doesn't work https://github.com/Microsoft/WSL/issues/486: Sync the overlay and 
```
# emerge --ask --verbose media-sound/pulseaudio::wsl
```
4. Emacs failed to build https://github.com/Microsoft/WSL/issues/1664
```
# bash -c "echo 0 > /proc/sys/kernel/randomize_va_space"
```
