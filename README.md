# Setup_Ubuntu

```bash
sudo apt update
sudo apt upgrade
sudo apt install htop git zsh openssh-server vim tmux

#sudo apt install smartmontools hddtemp nvme-cli
#sudo hddtemp /dev/sd*
#sudo smartctl -a /dev/sda | grep Temperature_Celsius
#sudo sudo nvme smart-log /dev/nvme0n1
```

### Docker
```bash
sudo apt-get install ca-certificates curl gnupg lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

### oh-my-zsh and plugins
```bash
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
python3 -c "import os;P=os.getenv('HOME')+'/.zshrc';f=open(P);L=list(f);f.close();O=open(P,'w');[O.write('plugins=(git zsh-autosuggestions zsh-syntax-highlighting)\n') if l.startswith('plugins=') else O.write(l) for l in L]"
```

### Add or remove user
```bash
userdel -r USERNAME
sudo useradd -m -p $(openssl passwd -1 "USER_PASSWORD") -s /bin/bash USERNAME
sudo usermod -aG sudo USERNAME
```

### Setup git
```bash
# git config --list
git config --global credential.helper store
git config --global user.email "example@gmail.com"
git config --global user.name "example"
```

### GPU monitor
```bash
pip install gpustat
gpustat -cupP -i
sudo nvidia-smi -pl 125  # Set power limit
```

### Nvidia GPU fan control 
```bash
sudo nvidia-xconfig -a --cool-bits=28 # then reboot
sudo nvidia-settings -a '[gpu:0]/GPUFanControlState=1' 
sudo nvidia-settings -a '[fan:0]/GPUTargetFanSpeed=50' -a '[fan:1]/GPUTargetFanSpeed=50'
```

### Anaconda
```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash 
```

### Disks
```bash
lsblk
ls -lha /dev/disk/by-uuid
sudo nano /etc/fstab
# /dev/disk/by-uuid/XXXXXXXX /media/XXXXXXXXX auto nosuid,nodev,nofail,x-gvfs-show 0 0
sudo mount -a
```

### Samba
```bash
sudo apt install sambd
sudo nano /etc/samba/smb.conf
# [Data]
#     path = /media/XXXX
#     browseable = yes
#     writable = yes
#     create mode = 0644
#     directory mode = 0744
#     user = USERNAME
sudo service smbd restart
```
