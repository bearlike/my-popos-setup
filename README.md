# Pop!_OS 20.04 LTS: Personal Setup 🤙

I forget a lot of stuff. Plus I should stop flushing my PC after every minor inconvenience. So I made this list of configurations

**🚫👿I hate Snaps.** They are slow to install, slow to start, take too much RAM, too much disk space and they auto-update themselves without asking, taking up bandwidth. I would try to avoid snaps as much as possible.  

## Update System Preferences 💿🔧

- **Settings** > **Universal Access** > Seeing > Pointer Control > **2** or **3** Points
- **Settings** > **Universal Access** > Seeing > Large Text > Turn **ON**
- **Settings** > **Universal Access** > Pointing & Clicking > Locate Pointer
- **Settings** > **Privacy** > Screen Lock > Blank Screen Delay > **15 minutes** or **Never**
- **Settings** > **Privacy** > Screen Lock > Blank Screen Delay > Lock Screen on Suspend
- **Settings** > Set your DNS to your **Pi-Hole**.
- **GNOME Tweaks**  > **General** > Turn OFF "**Suspend When laptop lid is closed**"
- **GNOME Tweaks**  > **General** > Turn ON "**Over Amplification**"
- **GNOME Tweaks**  > **Window Titlebars** > Titlebar Buttons > Turn**ON** Maximize & Minimize 
- Change **`Root`** Password `sudo passwd root`

---

### Upgrade Existing Packages ⬆️

```bash
sudo apt update && sudo apt upgrade -y
```

## Essential Programs 💯

```
Brave_Browser Discord Etcher GIMP Github_Desktop Htop Inkscape JRE Kodi Neofetch Nextcloud_Client PeaZip_GUI PIP3 qbittorrent screen Signal Stacer Telegram Tilix Typora Virtualbox VLC VSCode Zoom_Client
```

### Essential Programs (DEB Packages)

```bash
sudo apt install software-properties-common apt-transport-https ca-certificates wget curl gnupg git && \
sudo add-apt-repository ppa:videolan/stable-daily && \
sudo add-apt-repository ppa:team-xbmc/ppa && \
sudo add-apt-repository ppa:qbittorrent-team/qbittorrent-stable && \
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add - && \
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" && \
wget -qO - https://typora.io/linux/public-key.asc | sudo apt-key add - && \
sudo add-apt-repository 'deb https://typora.io/linux ./' && \
sudo add-apt-repository ppa:oguzhaninan/stacer -y && \
curl -s https://brave-browser-apt-release.s3.brave.com/brave-core.asc | sudo apt-key --keyring /etc/apt/trusted.gpg.d/brave-browser-release.gpg add - && \
echo "deb [arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main" | sudo tee /etc/apt/sources.list.d/brave-browser-release.list && \
wget -qO - https://packagecloud.io/shiftkey/desktop/gpgkey | sudo tee /etc/apt/trusted.gpg.d/shiftkey-desktop.asc > /dev/null && \
sudo sh -c 'echo "deb [arch=amd64] https://packagecloud.io/shiftkey/desktop/any/ any main" > /etc/apt/sources.list.d/packagecloud-shiftky-desktop.list' && \
echo "deb https://deb.etcher.io stable etcher" | sudo tee /etc/apt/sources.list.d/balena-etcher.list && \
sudo apt-key adv --keyserver hkps://keyserver.ubuntu.com:443 --recv-keys 379CE192D401AB61 && \
wget -c https://github.com/peazip/PeaZip/releases/download/7.7.0/peazip_7.7.0.LINUX.x86_64.GTK2.deb && \
wget https://zoom.us/client/latest/zoom_amd64.deb && \
wget https://dl.discordapp.net/apps/linux/0.0.13/discord-0.0.13.deb && \
sudo apt update && \
sudo apt install -y ./zoom_amd64.deb && \
sudo apt install -y ./peazip_7.7.0.LINUX.x86_64.GTK2.deb && \
sudo apt install -y ./discord-0.0.13.deb && \
sudo apt install -y tilix htop neofetch screen vlc kodi code typora stacer brave-browser github-desktop python3-pip balena-etcher-electron qbittorrent default-jre && \
sudo apt upgrade -y && \
sudo rm *.deb && sudo apt autoremove
```

```bash
# Requires Console Intervention to Accept T&C
sudo apt install -y virtualbox virtualbox-ext-pack
```


### Essential Programs (AppImages and Flatpaks) ❤️

```bash
mkdir AppImages && \
flatpak install https://flathub.org/repo/appstream/org.gimp.GIMP.flatpakref && \
flatpak install flathub org.inkscape.Inkscape && \
flatpak install flathub org.signal.Signal && \
flatpak install flathub org.telegram.desktop && \
wget -O "AppImages/Nextcloud.AppImage" https://github.com/nextcloud/desktop/releases/download/v3.1.2/Nextcloud-3.1.2-x86_64.AppImage
```

### Essential Python3 Packages 🐍

```bash
sudo apt update && \
sudo apt install -y libopencv-dev python3-opencv && \
pip3 install wheel flask numpy pymongo selenium opencv-python bs4 matplotlib scikit-learn Pillow pandas requests nltk bokeh pytest
```

### GNOME Tweaks and Extensions ⚡️

```bash
sudo add-apt-repository universe && \
sudo add-apt-repository ppa:afelinczak/ppa && \
sudo apt update && \
sudo apt install -y gnome-tweak-tool && \
sudo apt install -y gnome-shell-extension-gsconnect gnome-shell-extension-docker gnome-shell-screenshot clipit
```

----

## Installing Docker and Deploying Containers 🐳

```bash
sudo apt update && \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && \
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && \
sudo apt update && \
sudo apt install docker-ce && \
sudo usermod -aG docker ${USER} && \
su - ${USER}
```

### Deploying Essential Containers

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
