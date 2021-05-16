# setup script

https://github.com/daniel-thompson/pinebook-pro-debian-installer/

- commands here dont include sudo but most require sudo or root
- run `startx` after all commands have ran to launch i3
- `$WIFI_SSID` is wifi ssid
- `$WIFI_PSWD` is wifi password

```sh
# switch to debian sid/unstable
echo 'deb http://deb.debian.org/debian sid main contrib non-free' > /etc/apt/sources.list
echo 'deb-src http://deb.debian.org/debian sid main contrib non-free' >> /etc/apt/sources.list
apt update
apt full-upgrade

# connect to wifi
wpa_passphrase $WIFI_SSID $WIFI_PSWD > /etc/wpa_supplicant.conf
ip link set wlan0 down
ip link set wlan0 up
wpa_supplicant -B -iwlan0 -c /etc/wpa_supplicant.conf -Dnl80211,wext
dhclient wlan0

# grab package index updates
apt update
apt upgrade

# install basic utils
apt install neofetch
apt install vim
apt instakll wget curl

# meta programs
apt install apt-file
apt install firmware-misc-nonfree

# install i3 x window manager
apt install xinit
apt install i3

# install more tools
apt install flameshot
apt install firefox
apt isntall gnome-terminal
apt install gnome-system-monitor
apt install git git-gui

# configure git
git config --global user.name 'Meghan Denny'
git config --global user.email 'hello@nektro.net'
git config --global init.defaultBranch 'master'

# install vs code
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
echo 'deb https://packages.microsoft.com/repos/code stable main' >> /etc/apt/sources.list
apt update
apt install code

# more code stuff
apt install jq
apt install xz-utils
apt install build-essential

# sound
apt install pulseaudio
apt install pavucontrol

# more stuff
apt install htop
apt install golang

# llvm 11
echo 'deb http://apt.llvm.org/unstable/ llvm-toolchain-11 main' >> /etc/apt/sources.list
echo 'deb-src http://apt.llvm.org/unstable/ llvm-toolchain-11 main' >> /etc/apt/sources.list
wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add -
apt update
apt install llvm-11
