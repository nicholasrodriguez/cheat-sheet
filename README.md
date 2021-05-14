# Cheat sheet

List of freqently used but never remembered commands

# Linux

```
mount -r -t iso9660 /dev/sr0 /media
```

```
curl http://<URL>/folder/file.txt --output file.txt
curl http://<URL>/folder/file.txt -o file.txt
````

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

Get Ansible facts direct

```
ansible <hostname> -m ansible.builtin.setup
```

# .vimrc
```
set shiftwidth=2
set expandtab
set tabstop=4
color desert
```

# Python
