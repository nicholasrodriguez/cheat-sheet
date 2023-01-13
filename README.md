# Cheat sheet

List of freqently used but never remembered commands

# Linux
Mount CDROM
```
mount -r -t iso9660 /dev/sr0 /media
```
Curl stuff
```
curl http://<URL>/folder/file.txt --output file.txt
curl http://<URL>/folder/file.txt -o file.txt
```
Install from local CentOS media repo if no internet
```
mkdir /media/CentOS
mount -t iso9660 /dev/cdrom /media/CentOS
```
Check repo names in brackets [] in the media repo file
```
cat /etc/yum.repos.d/CentOS-Media.repo
```
Install from local repo
```
yum disablerepo=\* --enablerepo=c8-media-BaseOS --enablerepo=c8-media-AppStream install open-vm-tools
```
List Open Files and Ports
```
lsof -i -P -n | grep <PORT NUMBER>
```

# Git/Hub Config

1. Setup Github ssh keys

```
ssh-keygen -t rsa -b 4096 -C "EMAIL Address"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
ssh -T git@github.com
```

2. Add keys to account

[https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account]

3. Push SSH keys to another host if required

`
scp -r .ssh/  <NAME>@<HOST>:~
`

4. Install Git if required

`
sudo yum -y install git
`

5. Git config
```
git config --global color.ui auto
git config --global user.email "<NAME>@users.noreply.github.com"
git config --global user.name "<NAME>"
````

Run Git pull over subdirectories
```
for i in */.git; do ( echo $i; cd $i/..; git pull; ); done
```

# Ansible

```
ansible <HOST> -m ping
ansible <HOST> -a "/bin/echo hello"
ansible-playbook <playbook>.yml --tags <TAG NAME>
```

## Get Ansible facts direct

```
ansible <hostname> -m ansible.builtin.setup
```

## Create Role

Create a repo in Github without readme etc e.g. below using test-role

```
ansible-galaxy init --init-path . test-role
cd test-role
git init
git add .
git commit
git remote add origin git@github.com:nicholasrodriguez/test-role.git
git branch -M main
git push -u origin main
```

Goto [https://galaxy.ansible.com] and import

# .vimrc
```
set shiftwidth=2
set expandtab
set tabstop=4
color desert
```

# AWS
## CLI Install
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```
Configure
```
aws configure
```

# Docker
## Install
```
sudo dnf install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo dnf -y install docker-ce docker-ce-cli containerd.io
sudo systemctl enable --now docker
```
Manage Docker as a non-root user
```
sudo usermod -aG docker $USER
newgrp docker
```
Test Docker
```
docker info
docker run hello-world
```
Install Docker Compose
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
Test docker-compose
```
docker-compose --version
```

## Connect to Remote Docker Engine
Download cert
```
mkdir -pv ~/.docker
unzip cert.zip -d ~/.docker
```
Set env var for remote host
```
export DOCKER_HOST=tcp://<docker host>:<port> DOCKER_TLS_VERIFY=1
```
Or create context and connect remotely
```
docker context create \
    --docker host=ssh://docker-user@host1.example.com \
    --description="Remote engine" \
    my-remote-engine
```
Switch context
```
docker context use my-remote-engine
```
## Create
Create container interactively
```
sudo docker run -i -t centos:8 bash
```
Install stuff then exit
```
docker ps -a
docker commit <CONTAINER ID> infra-tools
```
## Run containers
Run another one
```
sudo docker run -i -t infra-tools bash
```
Connect to a stopped container
```
docker start -ia <CONTAINER ID>
```
Connect to a running container
```
docker exec -it <container name> /bin/bash
```
Mount local filesystem to a container
```
docker run -it -v $(pwd)/:/mnt/ mcr.microsoft.com/azurestack/powershell
```
## Export
Export to a file
```
docker save -o infra-tools.tar infra-tools:latest
```
Stop all containers
```
docker container stop $(docker container ls -aq)
```
Remove all containers
```
docker container rm $(docker container ls -aq)
```
# CentOS 8 to Rocky Linux
https://docs.rockylinux.org/guides/migrate2rocky/

## Prep the box
Got some odd package clashes on my personal CentOS 8 instances
```
sudo yum -y remove docker-ce
sudo yum -y remove docker-ce-cli 
sudo yum -y remove containers-common
sudo yum -y remove containerd.io
sudo yum -y remove rpm-build
```
## Clone the tools
```
cd ~
git clone https://github.com/rocky-linux/rocky-tools.git
cd rocky-tools/migrate2rocky
chmod u+x migrate2rocky.sh
```

## Convert to Rocky
```
cd ~/rocky-tools/migrate2rocky
sudo ./migrate2rocky.sh -r
```

# Terraform

## Windows Install
Plop the executable in 
```
C:\Users\<USER NAME>\AppData\Local\Microsoft\WindowsApps
```

# Python
