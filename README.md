# manjaro-dell-7480
This repo contains useful information for the installation and configuration of manjaro on dell latitude 7480

After the installation update the mirrors and the system, run:
```bash	
$ sudo pacman-mirrors --fasttrack && sudo pacman -Syyu
```
This will take several minutes, so grab a cup of coffee

#### Activate the AUR repository in the package manager 
- Open add/remove software
- click menu option
- Preferences
- go to the AUR tap
- Check: Enable AUR support
- Check: Updates from AUR

#### Install Oracle JDK 8
```bash
$ pamac build jdk8
```

select oracle jdk 8 as default
```bash
$ sudo archlinux-java set java-8-jdk
```
create the env variable, add to ./bashrc
```bash
$ echo 'export JAVA_HOME=/usr/lib/jvm/default' >> ~/.bashrc
$ exec $SHELL
```

### Install nvm for node
```bash
$ pamac build nvm
$ echo 'source /usr/share/nvm/init-nvm.sh' >> ~/.bashrc
$ exec $SHELL
```

### Install System apps
```bash
$ sudo pacman -S sbt
$ sudo pacman -S maven
$ sudo pacman -S gradle
$ sudo pacman -S terminator
$ sudo pacman -S vlc
```

### Remove not necessary packages
```bash
$ sudo pacman -Rs ms-office-online
```

### Install AUR apps
```bash
$ pamac build google-chrome
$ pamac build postman-bin
$ pamac build android-studio
$ pamac build giteye
$ pamac build webstorm
$ pamac build datagrip
$ pamac build pycharm
$ pamac build intellij-idea-ultimate-edition
$ pamac build slack-desktop
$ pamac build spotify
$ pamac build skypeforlinux-stable-bin
$ pamac build oracle-sqldeveloper

$ pamac build copyq
$ pamac build openfortivpn
$ pamac build wps-office
```

### Install gnome shell plugins
- system-monitor: https://extensions.gnome.org/extension/120/system-monitor/
- no-topleft-hot-corner: https://extensions.gnome.org/extension/118/no-topleft-hot-corner/

### Install and configure docker 

install docker and docker compose
```bash
$ sudo pacman -S docker docker-compose
$ sudo systemctl start docker
$ sudo systemctl enable docker
$ sudo usermod -aG docker $USER
```

### Solve the Issue with the bluetooth audio

LDAC/aptX codec support can be enabled by installing pulseaudio-modules-bt-git
```bash
$ pamac build pulseaudio-modules-bt-git
```

If PulseAudio fails when changing the profile to A2DP while using GNOME with GDM, you need to prevent GDM from starting its own instance of PulseAudio

- Prevent Pulseaudio clients from automatically starting a server if one is not running by adding the following:
```bash
$ sudo gedit /var/lib/gdm/.config/pulse/client.conf
```
and add:
```text
autospawn = no
daemon-binary = /bin/true
```

- Prevent systemd from starting Pulseaudio anyway with socket activation:
```bash
$ sudo -ugdm mkdir -p /var/lib/gdm/.config/systemd/user
$ sudo -ugdm ln -s /dev/null /var/lib/gdm/.config/systemd/user/pulseaudio.socket
```
- Restart, and enjoy. 
