# Setup_Ubuntu

```bash
sudo apt update
sudo apt upgrade
sudo apt install htop git zsh openssh-server
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

### oh-my-zsh and plugins
```bash
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
python3 -c "import os;P=os.getenv('HOME')+'/.zshrc';f=open(P);L=list(f);f.close();O=open(P,'w');[O.write('plugins=(git zsh-autosuggestions zsh-syntax-highlighting)\n') if l.startswith('plugins=') else O.write(l) for l in L]"
```

### Bashtop
```bash
sudo add-apt-repository ppa:bashtop-monitor/bashtop
sudo apt update
sudo apt install bashtop
```

### GPU monitor
```bash
pip install gpustat
gpustat -cupP -i
sudo nvidia-smi -pl 125  # Set power limit
```

### Anaconda
```bash
wget https://repo.anaconda.com/archive/Anaconda3-2020.07-Linux-x86_64.sh
chmod +x Anaconda3-2020.07-Linux-x86_64.sh
./Anaconda3-2020.07-Linux-x86_64.sh
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

### Hugo
```bash
# snap install hugo
snap install hugo --channel=extended
```

### Google Cloud enable passwd login
```bash
sudo nano /etc/ssh/sshd_config
# PasswordAuthentication yes
sudo service sshd restart
```