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

# Docker
Create container interactively
```
sudo docker run -i -t centos:8 bash
```
Install stuff then exit
```
docker ps -a
docker commit <CONTAINER ID> infra-tools
```
Run another one
```
sudo docker run -i -t infra-tools bash
```
Export to a file
```
docker save -o infra-tools.tar infra-tools:latest
```

# Python
