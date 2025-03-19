
# Add shotkey
To add it back:go to xfce4-keyboard-settings Application Shortcuts tab
xfce:xfce4-settings:keyboard [Xfce Docs] 40
Click +Add button and use this command for whisker menu:
/usr/bin/xfce4-popup-whiskermenu

# Set defaul login user
/etc/lightdm/lightdm.conf
greeter-hide-users = True                      
user-session = tenwolde

# Keyboard
English US / English (US, intl., with dead keys) 

# Install packages
sudo apt update && sudo apt upgrade
sudo apt-get install jq python3 python3-dev python3-pip systemd-timesyncd build-essential network-manager-openvpn-gnome php-cli wakeonlan davfs2 procps curl file npm telegram-desktop net-tools unzip wget software-properties-common onedrive mate-calc gvfs-backends chromium git sshfs thunderbird thunderbird-l10n-nl blueman htop gnome-control-center dkms linux-headers-$(uname -r) build-essential libdrm-dev -y

# Time sync
sudo systemctl enable systemd-timesyncd --now
timedatectl status

# Just
wget -qO - 'https://proget.makedeb.org/debian-feeds/prebuilt-mpr.pub' | gpg --dearmor | sudo tee /usr/share/keyrings/prebuilt-mpr-archive-keyring.gpg 1> /dev/null
echo "deb [arch=all,$(dpkg --print-architecture) signed-by=/usr/share/keyrings/prebuilt-mpr-archive-keyring.gpg] https://proget.makedeb.org prebuilt-mpr $(lsb_release -cs)" | sudo tee /etc/apt/sources.list.d/prebuilt-mpr.list
sudo apt update
sudo apt-get install just

# Nautilus
sudo apt-get install nautilus
nano ~/.config/xfce4/helpers.rc
FileManager=nautilus
xfdesktop --reload




# NODE
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
source ~/.bashrc
nvm install --lts
nvm use --lts
node -v
npm -v


# NODE methode van Jort
nvm alias default lts/*
nvm install --latest-npm --reinstall-packages-from=default 'lts/*'


# Signal
wget -O- https://updates.signal.org/desktop/apt/keys.asc | gpg --dearmor > signal-desktop-keyring.gpg
cat signal-desktop-keyring.gpg | sudo tee /usr/share/keyrings/signal-desktop-keyring.gpg > /dev/null

echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/signal-desktop-keyring.gpg] https://updates.signal.org/desktop/apt xenial main' |\
  sudo tee /etc/apt/sources.list.d/signal-xenial.list

sudo apt update && sudo apt install signal-desktop

# Install displaylink
sudo apt update
sudo apt install linux-headers-$(uname -r) build-essential dkms libdrm-dev
git clone https://github.com/DisplayLink/evdi.git
cd evdi
git checkout v1.14.1
sudo dkms add ./module
sudo dkms build evdi/1.14.1
sudo dkms install evdi/1.14.1
sudo bash displaylink-driver-6.1.0-17.run
sudo reboot
lsmod | grep evdi
sudo systemctl status displaylink.service


# Flatpak
sudo apt install flatpak
sudo flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak search slack
sudo flatpak install Slack
sudo flatpak install flathub org.gtk.Gtk3theme.Adwaita-dark 
sudo flatpak install flathub io.kinvolk.Headlamp



# Packages via snap
snap install kustomize
sudo snap install just --classic
sudo apt install snapd

# Kubent
sh -c "$(curl -sSL https://git.io/install-kubent)"

# Github Desktop
wget -qO - https://mirror.mwt.me/shiftkey-desktop/gpgkey | gpg --dearmor | sudo tee /usr/share/keyrings/mwt-desktop.gpg > /dev/null
sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/mwt-desktop.gpg] https://mirror.mwt.me/shiftkey-desktop/deb/ any main" > /etc/apt/sources.list.d/mwt-desktop.list'
sudo apt update && sudo apt install github-desktop -y


gpg --full-generate-key (enter enter enter y Wilco ten Wolde wilco@tenwolde.nu)
gpg --list-secret-keys --keyid-format=long	
	sec   rsa3072/DDFE0A6EAB2786AA 2025-01-27 [SC]
gpg --armor --export DDFE0A6EAB2786AA    

Sleutel toevoegen op https://github.com/settings/keys

git config --global --edit
toevoegen;
[user]
  name = Wilco ten Wolde
  email = wilco@tenwolde.nu
  signingkey = DDFE0A6EAB2786AA
[gpg]
  program = /usr/bin/gpg
[commit]
  gpgsign = true
[tag]
  gpgsign = true



# VScode
wget -O vscode.deb 'https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64'
sudo dpkg -i vscode.deb



# ArgoCD CLI
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo mv argocd-linux-amd64 /usr/local/bin/argocd
chmod +x argocd-linux-amd64
argocd version

# temp sensors
sudo apt-get install lm-sensors 
sudo sensors-detect
sudo service kmod start
sensors

# KubeCTL
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check   << deze moet oke geven
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client



# Aliasses
Toevoegen in .bashrc;

alias ctx='kubectl config get-contexts'
alias kswitch='kubectl config use-context'

# AWS Cli
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "/tmp/awscliv2.zip"
unzip -d /tmp/ /tmp/awscliv2.zip
sudo /tmp/aws/install
/usr/local/bin/aws --version

# CDK
npm install -g aws-cdk

# Helm 3
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
sudo bash get_helm.sh
sudo rm get_helm.sh

# K9S
Kijken wat de laatste release is https://github.com/derailed/k9s/releases en dat nummer hieronder in de URL zetten 
curl -Lo k9s.tar.gz https://github.com/derailed/k9s/releases/download/v0.32.5/k9s_Linux_amd64.tar.gz
tar -xvzf k9s.tar.gz
sudo mv k9s /usr/local/bin/

# PG Admin
sudo curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add
sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list'
sudo apt update
sudo apt install pgadmin4-desktop


# Docker
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
sudo usermod -a -G docker $USER

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Webdav mount nextcloud
sudo usermod -a -G davfs2 tenwolde
sudo mount -t davfs -o rw,uid=tenwolde,gid=tenwolde https://storage.tenwolde.nu/remote.php/webdav/ /media/n100webdav/

# Font 
Fonts plaatsen in ~/.local/share/fonts/
Herladen met; fc-cache -fv
In vscode; 'ComicCodeLigatures Nerd Font','FiraCode Nerd Font Mono'

# Java
wget https://download.java.net/openjdk/jdk21/ri/openjdk-21+35_linux-x64_bin.tar.gz (of kijk even hier https://jdk.java.net/java-se-ri/21)
sudo tar -xvf openjdk-21+35_linux-x64_bin.tar.gz -C /opt

Onderstaande toevoegen aan /etc/profile
export JAVA_HOME=/opt/jdk-21
export PATH=$JAVA_HOME/bin:$PATH

Bende opnieuw inladen en versie controleren
source /etc/profile
java -version

Download gradle
wget https://services.gradle.org/distributions/gradle-8.4-bin.zip
sudo unzip gradle-8.4-bin.zip -d /opt
sudo ln -s /opt/gradle-8.4/bin/gradle /usr/bin/gradle

Toevoegen aan ~/.bashrc
export JAVA_HOME=/opt/jdk-21
export PATH=$JAVA_HOME/bin:$PATH

Bende opnieuw inladen en versie controleren
source ~/.bashrc
gradle -v


# Google chrome
sudo apt-get install libxss1 libappindicator1 libindicator7
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome*.deb


# Virtual box
wget -O- -q https://www.virtualbox.org/download/oracle_vbox_2016.asc | sudo gpg --dearmour -o /usr/share/keyrings/oracle_vbox_2016.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/oracle_vbox_2016.gpg] http://download.virtualbox.org/virtualbox/debian bookworm contrib" | sudo tee /etc/apt/sources.list.d/virtualbox.list
sudo apt-get update
sudo apt install virtualbox-7.1

# vscode externties
ctrl+p
ext install nefrob.vscode-just-syntax


# Overige notities
lsusb
xrandr 
xrandr --auto
env BAMF_DESKTOP_FILE_HINT=/var/lib/snapd/desktop/applications/slack_slack.desktop /snap/bin/slack %U



# Docker station debian 12 
systemd-cryptenroll en dracut methode

sudo apt install dracut tpm2-tools

sudo systemd-cryptenroll --tpm2-device=auto --tpm2-pcrs=0+7 /dev/sda3
	🔐 Please enter current passphrase for disk /dev/sda3:              
	New TPM2 token enrolled as key slot 4.



# Debian 12 auto boot encrypted disk 
sudo apt update
sudo apt install clevis clevis-luks tpm2-tools clevis-tpm2

sudo tpm2_createprimary -C e -g sha256 -G rsa -c primary.ctx

sudo nano /etc/default/grub
	GRUB_CMDLINE_LINUX="rd.auto rd.luks=1"

sudo update-grub
sudo dracut -f


# Debian 12 docker

sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
sudo groupadd docker
newgrp docker
sudo usermod -aG docker $USER

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin


# rpi-imager
echo $PATH
export PATH=$PATH:/snap/bin  (indien die er niet bij staat)
echo 'export PATH=$PATH:/snap/bin' >> ~/.bashrc
source ~/.bashrc
sudo snap install rpi-imager
snap list rpi-imagerkubectl get secret -n argo-cd argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode




# Swapp volledig uitzetten
sudo swapoff -a


# Minikube

Installatie
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube version

Starten
minikube start --driver=docker

Status
minikube status

Als het draait kan je nu context switchen 



# USB Disk ecrypt
lsblk
sudo dd if=/dev/zero of=/dev/sda bs=1M status=progress

sudo apt update
sudo apt install cryptsetup

sudo cryptsetup luksFormat /dev/sda

sudo cryptsetup open /dev/sda usb_disk
sudo mkfs.ext4 /dev/mapper/usb_disk

# Raspberry Docker station
$ nmtui
$ raspi-config







# TODO
teams mysql-client mysql-workbench 
