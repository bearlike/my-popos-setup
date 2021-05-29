# Pop!_OS 20.04 LTS: Personal Setup 🤙

I forget a lot of stuff. Plus I should stop flushing my PC after every minor inconvenience. So I made this list of scripts and configurations

**🚫👿 I hate Snaps.** They are slow to install, slow to start, take too much RAM, too much disk space and they auto-update themselves without asking, taking up bandwidth. I would try to avoid snaps as much as possible.  

## Update System Preferences 💿🔧

- **Settings** > **Accessibility** > Seeing > Pointer Control > **2** or **3** Points
- **Settings** > **Accessibility** > Seeing > Large Text > Turn **ON**
- **Settings** > **Accessibility** > Pointing & Clicking > Locate Pointer
- **Settings** > **Privacy** > Screen Lock > Blank Screen Delay > **15 minutes** or **Never**
- **Settings** > **Privacy** > Screen Lock > Blank Screen Delay > Lock Screen on Suspend
- **Settings** > Set your DNS to your **Pi-Hole**.
- **Settings** > **About** > Change **Hostname**
- **GNOME Tweaks** > **General** > Turn OFF "**Suspend When laptop lid is closed**"
- **GNOME Tweaks** > **General** > Turn ON "**Over Amplification**"
- **GNOME Tweaks** > **Window Titlebars** > Titlebar Buttons > Turn **ON** Maximize & Minimize 
- Change **`Root`** Password `sudo passwd root`
- Automatically mount **Network Drives** and setup **NextCloud**.

### Change Appearance to my Liking :sunflower: 
[Wallpaper](https://thekrishna.in/my-popos-setup/configs/wallpaper/Abstract-Wallpaper.jpg), Cursor ([**We10XOS-cursors**](https://github.com/yeyushengfan258/We10XOS-cursors)), Icons ([**Papirus**](https://github.com/PapirusDevelopmentTeam/papirus-icon-theme)) etc.
```bash
echo "Changing Wallapaper..." && \
mkdir /home/${USER}/Pictures/Wallpapers && \
wget -q -P /home/${USER}/Pictures/Wallpapers https://thekrishna.in/my-popos-setup/configs/wallpaper/Abstract-Wallpaper.jpg && \
gsettings set org.gnome.desktop.background picture-uri file:////home/${USER}/Pictures/Wallpapers/Abstract-Wallpaper.jpg && \
echo "Changing Icon Theme to Papirus..." && \
sudo add-apt-repository -y ppa:papirus/papirus > /dev/null 2>&1 && \
sudo apt install -y -qq papirus-icon-theme && \
gsettings set org.gnome.desktop.interface icon-theme 'Papirus' && \
echo "Changing Cursor to We10XOS-cursors..." && \
git clone -q https://github.com/yeyushengfan258/We10XOS-cursors.git && \
sudo ./We10XOS-cursors/install.sh > /dev/null 2>&1 && \
gsettings set org.gnome.desktop.interface cursor-theme 'We10XOS-cursors'
sudo rm -r We10XOS-cursors && \
echo "Done :)"
```
---

### Upgrade Existing Packages ⬆️

```bash
sudo apt update && sudo apt upgrade -y
```

## Installing Essential Programs 💯
List of Programs: 
```
Brave_Browser Discord Etcher GIMP Github_Desktop Htop Huluti Inkscape JRE Kodi Lutris_(+Wine_and_Dependencies) MongoDB_Compass Neofetch Nextcloud_Client Onlyoffice PeaZip_GUI PIP3 qbittorrent screen Signal Telegram Tilix Typora Virtualbox VLC VSCode Zoom_Client
```

### Essential Programs (DEB Packages)

```bash
sudo apt update && \
sudo apt install -y -qq software-properties-common apt-transport-https ca-certificates wget curl gnupg git && \
sudo add-apt-repository -y ppa:team-xbmc/ppa && \
sudo add-apt-repository -y ppa:qbittorrent-team/qbittorrent-stable && \
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add - && \
sudo add-apt-repository -y "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" && \
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -  && \
sudo add-apt-repository -y "deb [arch=amd64] https://download.virtualbox.org/virtualbox/debian focal contrib" && \
wget -qO - https://typora.io/linux/public-key.asc | sudo apt-key add - && \
sudo add-apt-repository -y 'deb https://typora.io/linux ./' && \
curl -s https://brave-browser-apt-release.s3.brave.com/brave-core.asc | sudo apt-key --keyring /etc/apt/trusted.gpg.d/brave-browser-release.gpg add - && \
echo "deb [arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main" | sudo tee /etc/apt/sources.list.d/brave-browser-release.list && \
wget -qO - https://packagecloud.io/shiftkey/desktop/gpgkey | sudo tee /etc/apt/trusted.gpg.d/shiftkey-desktop.asc > /dev/null && \
sudo sh -c 'echo "deb [arch=amd64] https://packagecloud.io/shiftkey/desktop/any/ any main" > /etc/apt/sources.list.d/packagecloud-shiftky-desktop.list' && \
curl -1sLf 'https://dl.cloudsmith.io/public/balena/etcher/setup.deb.sh' | sudo -E bash && \
sudo apt-key adv --keyserver hkps://keyserver.ubuntu.com:443 --recv-keys 379CE192D401AB61 && \
wget -c https://github.com/peazip/PeaZip/releases/download/7.7.0/peazip_7.7.0.LINUX.x86_64.GTK2.deb && \
wget https://zoom.us/client/latest/zoom_amd64.deb && \
wget https://dl.discordapp.net/apps/linux/0.0.13/discord-0.0.13.deb && \
wget https://downloads.mongodb.com/compass/mongodb-compass_1.26.1_amd64.deb && \
sudo apt update && \
sudo apt install -y net-tools tilix htop neofetch screen vlc kodi code typora brave-browser github-desktop python3-pip balena-etcher-electron qbittorrent virtualbox lutris default-jre && \
sudo apt install -y ./zoom_amd64.deb && \
sudo apt install -y ./peazip_7.7.0.LINUX.x86_64.GTK2.deb && \
sudo apt install -y ./discord-0.0.13.deb && \
sudo dpkg -i mongodb-compass_1.26.1_amd64.deb && \
sudo apt upgrade -y && \
sudo rm *.deb && sudo apt autoremove
```

```bash
# Requires Console Intervention to Accept T&C
sudo apt install -y virtualbox-ext-pack
```

### Install and Configure Powerline
```bash
sudo apt install -y powerline fonts-powerline && \
echo -e "\nif [ -f /usr/share/powerline/bindings/bash/powerline.sh ]; then \n   powerline-daemon -q\n   POWERLINE_BASH_CONTINUATION=1\n   POWERLINE_BASH_SELECT=1\n   source /usr/share/powerline/bindings/bash/powerline.sh\n fi\n" >> $HOME/.bashrc && \
```

### Installing KVM + related tools (KVM >>> VirtualBox) ⚡️
[VirtIO drivers for Windows Guest Machines](https://github.com/virtio-win/virtio-win-pkg-scripts/blob/master/README.md)
```bash
sudo apt -y install qemu-kvm libvirt-bin bridge-utils virt-manager libvirt-daemon-system libvirt-clients qemu virt-viewer spice-vdagent && \
sudo adduser ${USER} libvirt && \
sudo adduser ${USER} kvm
```


### Installing Essential Programs (AppImages and Flatpaks) ❤️
```bash
mkdir AppImages && \
flatpak install --assumeyes --noninteractive --system https://flathub.org/repo/appstream/org.gimp.GIMP.flatpakref && \
flatpak install --assumeyes --noninteractive --system flathub com.github.huluti.Curtail && \
flatpak install --assumeyes --noninteractive --system flathub org.onlyoffice.desktopeditors && \
flatpak install --assumeyes --noninteractive --system flathub org.inkscape.Inkscape && \
flatpak install --assumeyes --noninteractive --system flathub org.signal.Signal && \
flatpak install --assumeyes --noninteractive --system flathub org.telegram.desktop && \
wget -O "AppImages/Nextcloud.AppImage" https://github.com/nextcloud/desktop/releases/download/v3.1.2/Nextcloud-3.1.2-x86_64.AppImage
```

### Essential Python3 Packages 🐍
```bash
sudo apt update && \
sudo apt install -y libopencv-dev python3-opencv && \
pip3 install wheel flask numpy pymongo selenium opencv-python bs4 matplotlib scikit-learn Pillow pandas requests nltk bokeh pytest
```

### [Patch for GIMP 2.10+ for Photoshop Users](https://github.com/Diolinux/PhotoGIMP) :art:
```bash
# GIMP must installed as a Flatpak before this
wget https://github.com/Diolinux/PhotoGIMP/releases/download/1.0/PhotoGIMP.by.Diolinux.v2020.for.Flatpak.zip && \
unzip PhotoGIMP.by.Diolinux.v2020.for.Flatpak.zip -d /home/$USER  && \ 
rm -r PhotoGIMP.by.Diolinux.v2020.for.Flatpak.zip
```

### [Photoshop CC v19 installer for Linux](https://github.com/Gictorbit/photoshopCClinux):wine_glass:
```bash
sudo apt install -y wine wine64 winetricks mono-complete && \
git clone -q https://github.com/Gictorbit/photoshopCClinux.git && \
cd photoshopCClinux/scripts && \
chmod +x PhotoshopSetup.sh  && \
./PhotoshopSetup.sh 
```

### GNOME Tweaks and Extensions ⚡️
```bash
sudo add-apt-repository -y universe && \
sudo add-apt-repository -y ppa:afelinczak/ppa && \
sudo apt update && \
sudo apt install -y gnome-tweak-tool && \
sudo apt install -y gnome-shell-extension-gsconnect clipit
```

----

## Installing Docker and Deploying Containers 🐳

```bash
sudo apt update && \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && \
sudo add-apt-repository -y "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && \
sudo apt update && \
sudo apt install docker-ce && \
sudo usermod -aG docker ${USER} && \
su - ${USER}
```

### Deploying Essential Containers
[Portainer](https://hub.docker.com/r/portainer/portainer-ce), [MongoDB_Server](https://hub.docker.com/_/mongo), [MySQL_Server](https://hub.docker.com/_/mysql) + [PhpMyAdmin](https://hub.docker.com/_/phpmyadmin), [Grafana](https://hub.docker.com/r/grafana/grafana) 

```bash
docker volume create portainer_data && \
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce --logo "https://thekrishna.in/assets/img/KK.png"
```

```bash
sudo mkdir -p /mongodata && \
docker run -d -t -v /data/db:/mongodata -p 27017:27017 --name mongodb mongo && \
docker run --name=grafana -d -p 3000:3000 grafana/grafana && \
docker run --name mysql -e MYSQL_ROOT_PASSWORD="0000" -p 3306:3306 -d mysql && \
docker run --name phpmyadmin -d --link mysql:db -p 8080:80 phpmyadmin/phpmyadmin
```


## Yesssss! 👊❤️

"Have fun using your completely configured system, future me." - Old you.
