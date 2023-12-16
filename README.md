<div align=center>
  <h1>Unix-Setup-Cheatsheet</h1>
</div>

## 🔍 Table of Contents
- [💼 Introduction](#-introduction)
- [🎓 Tutorial](#-tutorial)
  - [Bash](#bash)
    - [Bashrc](#bashrc)
    - [Bash\_aliases](#bash_aliases)
  - [Filesystem](#filesystem)
    - [Permissions](#permissions)
      - [Changing permissions](#changing-permissions)
- [🔤 Aliases](#-aliases)
  - [Aliases for apt](#aliases-for-apt)
  - [Aliases for yum](#aliases-for-yum)
  - [Docker aliases](#docker-aliases)
  - [System aliases](#system-aliases)
  - [Safer aliases](#safer-aliases)
- [📦 Package Managers](#-package-managers)
  - [Apt](#apt)
  - [Yum](#yum)
- [🎁 Useful packages](#-useful-packages)
  - [Essentials](#essentials)
  - [Vanity](#vanity)
- [🚀 Devops](#-devops)
  - [🔐 SSH](#-ssh)
  - [🐙 Git](#-git)
    - [How to clone a private repository from github to a server](#how-to-clone-a-private-repository-from-github-to-a-server)
    - [How to setup github actions redeploy (connected)](#how-to-setup-github-actions-redeploy-connected)
  - [🐳 Docker](#-docker)
- [🛡️ Security](#️-security)
- [🛠️ Maintenance](#️-maintenance)
- [🚚 Server Migration](#-server-migration)
- [🐧 Gratitude](#-gratitude)

# 💼 Introduction
This repository aims to provide useful commands, packages, and configuration options to setup on various apt / yum unix distributions, typically with bash as the shell. This can aid with expediting service deployment & devops & system maintenance, all the while promoting ease of use and maintainability, as well as security.

# 🎓 Tutorial
## Bash
### Bashrc
The bashrc file is a file that is executed each time a new terminal is opened. It is located in the home directory, and can be edited with any text editor. The bashrc file is used to set environment variables, aliases, and other settings that are used by the shell.

Edit bashrc file
```bash
nano ~/.bashrc # edit bashrc file
source ~/.bashrc # reload bashrc file
cat ~/.bashrc # show bashrc file
```

### Bash_aliases
The bash_aliases file is a file that is executed each time a new terminal is opened. It is located in the home directory, and can be edited with any text editor. The bash_aliases file is used to set aliases that are used by the shell.

Edit bash_aliases file
```bash
nano ~/.bash_aliases # edit bash_aliases file
source ~/.bash_aliases # reload bash_aliases file
cat ~/.bash_aliases # show bash_aliases file
```

## Filesystem
### Permissions
Permissions are used to restrict access to files and directories. There are three types of permissions: read, write, and execute. These permissions can be set for the owner, group, and others. The owner is the user that owns the file, the group is the group that owns the file, and others are everyone else.

- **Read**: Read permissions allow the user to read the contents of the file. This is represented by the letter `r`.

- **Write**: Write permissions allow the user to write to the file. This is represented by the letter `w`.

- **Execute**: Execute permissions allow the user to execute the file. This is represented by the letter `x`.

#### Changing permissions
Permissions can be changed using the `chmod` command. The `chmod` command takes two arguments: the permissions to set, and the file to set them on. The permissions can be set using the octal notation, or the symbolic notation.

# 🔤 Aliases
Aliases are essentially hotkeys of sorts; that allow you to execute a command with certain flags without actually having to write them out each time. They can be added to the bashrc file (see [~/.bashrc file](#bashrc)), for global use, or to the bash_aliases file (see [~/.bash_aliases file](#bash_aliases)), for user specific use.

## Aliases for apt
```bash
alias update='sudo apt update && sudo apt upgrade -y'
alias install='sudo apt install'
alias remove='sudo apt remove'
alias search='apt search'
alias autoremove='sudo apt autoremove'
```

## Aliases for yum
```bash
alias update='sudo yum update -y'
alias install='sudo yum install'
alias remove='sudo yum remove'
alias search='yum search'
alias autoremove='sudo yum autoremove'
```

## Docker aliases
```bash
# Docker
alias dock='docker'
alias dockps='docker ps'
alias dockpsa='docker ps -a'
alias dockimages='docker images'
alias dockvols='docker volume ls'
alias dockvol='docker volume inspect'
alias docklogs='docker logs --follow --tail 500'
alias dockexec='docker exec -it'
alias dockstop='docker stop'
alias dockstart='docker start'
alias dockkill='docker kill'
alias dockrm='docker rm'
alias dockrmi='docker rmi'
alias dockrmall='docker rm $(docker ps -a -q) && docker rmi $(docker images -q)'
alias dockrmallf='docker rm -f $(docker ps -a -q) && docker rmi -f $(docker images -q)'
alias dockprunei='docker image prune -a -f'
alias dockpruneb='docker builder prune -f'
alias dockprunes='docker system prune -a -f'
alias dockpruneall='docker image prune -a -f && docker builder prune -f && docker system prune -a -f'
alias dockrestart='docker restart'
alias dockrestarta='docker restart $(docker ps -a -q)'
alias dockrestartf='docker restart $(docker ps -f status=exited -q)'
alias dockrun='docker run'
alias dockpull='docker pull'
alias dockpush='docker push'
alias dockbuild='docker build'

# Docker Compose
alias comp='docker-compose'
alias compup='docker-compose up -d --build'
alias compdown='docker-compose down'
alias compps='docker-compose ps'
alias compexec='docker-compose exec'
alias compstop='docker-compose stop'
alias compkill='docker-compose kill'
alias comprm='docker-compose rm'
alias comprmf='docker-compose rm -f'
alias comprmall='docker-compose rm $(docker-compose ps -a -q)'
alias comprmallf='docker-compose rm -f $(docker-compose ps -a -q)'
alias complogs='docker-compose logs --follow --tail 500'
alias compprunei='docker-compose image prune -a -f'
alias comppruneb='docker-compose builder prune -f'
alias compprunes='docker-compose system prune -a -f'
alias comppruneall='docker-compose image prune -a -f && docker-compose builder prune -f && docker-compose system prune -a -f'
```

## System aliases
```bash
alias ls='eza -Fg -l --group-directories-first -S -h' # requires eza package
alias ls='ls -lh --color=auto --group-directories-first' # native ls implementation
alias la='ls -la'
alias ll='ls -l'
alias al='la'
alias sl='ls'
alias df='df -h | sort -k2 -hr'
alias du='du -h'
alias ip='ip -c'
alias cal='cal -m'
alias vim='env -u TERM vim'
alias diff='diff -u --color=always'
alias tree='tree -CF --dirsfirst'
alias less='less -RF'
```

## Safer aliases
```bash
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
alias ln='ln -i'
```

# 📦 Package Managers
Package managers are used to install, update, and remove software. They are used to manage dependencies, and can be used to install software from a repository.

## Apt
Apt is the package manager for Debian based distributions. It is used to install, update, and remove software. It is used to manage dependencies, and can be used to install software from a repository.

```bash
sudo apt update && sudo apt upgrade -y # update package list and upgrade packages
sudo apt install <package> # install package
sudo apt remove <package> # remove package
sudo apt search <package> # search for package
sudo apt autoremove # remove all unused packages, dependencies, and configuration files
```

## Yum
Yum is the package manager for Red Hat based distributions. It is used to install, update, and remove software. It is used to manage dependencies, and can be used to install software from a repository.

```bash
sudo yum update -y # update package list and upgrade packages
sudo yum install <package> # install package
sudo yum remove <package> # remove package
sudo yum search <package> # search for package
sudo yum autoremove # remove all unused packages, dependencies, and configuration files
```

# 🎁 Useful packages
## Essentials
```bash
# Main packages
sudo apt install curl # download files
sudo apt install wget # download files
sudo apt install git # version control
sudo apt install neovim # neovim text editor

# Docker
sudo apt-get remove docker docker-engine docker.io # remove old docker versions
sudo apt install docker.io # docker
sudo apt install docker-compose # docker-compose
sudo apt install docker-registry # docker-registry
sudo apt install docker-machine # docker-machine
sudo apt install docker-doc # docker-doc
sudo apt install docker.io-doc # docker.io-doc
sudo apt install docker-compose-doc # docker-compose-doc
sudo apt install docker-registry-doc # docker-registry-doc
sudo apt install docker-machine-doc # docker-machine-doc

# Netdata
wget <<<........................>>> # install netdata (get full link from https://www.netdata.cloud/, when selecting OS)
sudo systemctl start netdata # start netdata
sudo systemctl enable netdata # enable netdata on startup
sudo systemctl status netdata # show netdata status
sudo systemctl stop netdata # stop netdata
sudo journalctl --unit=netdata --follow # show netdata logs (follow)
sudo /etc/netdata/./edit-config --list # show netdata config
sudo /etc/netdata/./edit-config # edit netdata config
sudo /etc/netdata/./edit-config health_alarm_notify.conf # edit netdata health alarm notify config
# Don't forget to restart netdata!
sudo /usr/libexec/netdata/plugins.d/alarm-notify.sh test discord # test discord webhook notification
```
## Vanity
```bash
sudo apt install eza # ls replacement
sudo apt install bat # cat replacement
sudo apt install htop # top replacement
```

# 🚀 Devops

## 🔐 SSH
```bash
ssh-keygen -t ed25519 -a 100000 -o -f C:/Users/<username>/.ssh/<keyname> # generate strong public/private key (windows)
ssh-keygen -t ed25519 -a 100000 -o -f ~/.ssh/<keyname> # generate strong public/private key (linux)

ssh-keygen -t ed25519 -a 100000 -o -f ~/.ssh/<keyname> -C "<nameORemail>" # generate with description
ssh-keygen -t ed25519 -a 100000 -o -f ~/.ssh/<keyname> -N "<passphrase>" # generate with passphrase

# Note: Private key stays on local machine, public key is copied to server (when SSHing into server).

ssh-copy-id <username>@<ip> # automatically copy ssh key to server
nano ~/.ssh/authorized_keys # # manually copy public key to server (add public key to authorized_keys file on server)
ssh <username>@<ip> # ssh into server
ssh -i <path/to/key> <username>@<ip> # ssh into server with key
ssh -i <path/to/key> -p <port> <username>@<ip> # ssh into server with key and port

chmod 700 ~/.ssh # set permissions for .ssh directory
chmod 600 ~/.ssh/<keyname> # set permissions for private key
chmod 644 ~/.ssh/<keyname>.pub # set permissions for public key
```

## 🐙 Git
### How to clone a private repository from github to a server
```bash
# 1. Generate a new ssh key pair on the server with your GitHub email address as a comment.
ssh-keygen -t ed25519 -a 100000 -f ~/.ssh/<projectname>_github_access -C "<youremail@something>"
# 2. Create a config file in the .ssh directory (if does not already exist)
touch ~/.ssh/config
nano ~/.ssh/config
# 3. Add the following to the config file (adjust as needed):
Host github
  HostName github.com
  User git
  AddKeysToAgent yes
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/<projectname>_github_access
# 2. Copy the contents of the public key to the clipboard
cat ~/.ssh/<projectname>_github_access.pub
# 3. Navigate to the github repository > Settings > Deploy keys > Add deploy key (https://github.com/<usernameORorganization>/<repositoryName>/settings/keys).
# 4. Give the public key a title, and paste the contents of the public key into the key field.
# 5. Go to the server, and clone the repository using the following command:
git clone github:<usernameORorganization>/<repository>.git # e.g., git clone git@github:elendil7/Unix-Setup-Cheatsheet
```

### How to setup github actions redeploy (connected)
```bash
# 1. Generate a new ssh key pair on the server
ssh-keygen -t ed25519 -a 100000 -f ~/.ssh/<projectname>_github_actions
# 2. Add the generated public key to the authorized_keys file on the server
cat ~/.ssh/<projectname>_github_actions.pub
nano ~/.ssh/authorized_keys
# 3. Copy the contents of the private key to the clipboard
cat ~/.ssh/<projectname>_github_actions
# 4. Go to github repository > Settings > Secrets > New repository secret (https://github.com/<usernameORorganization>/<repositoryName>/settings/secrets/actions)
# 5. Add the following secrets to the repository:
SERVER_HOST # ip address of server
SERVER_PORT # port of server (default: 22)
SERVER_USER # username of server
SERVER_KEY # private key of server (copy contents of ~/.ssh/<projectname> file)
# 6. In your github actions file, add the following code as a step in the workflow (adjust as needed):
- name: Connect via SSH to server, and execute redeploy commands.
  uses: appleboy/ssh-action@v0.1.9
  with:
    host: ${{ secrets.SERVER_HOST }}
    port: ${{ secrets.SERVER_PORT }}
    username: ${{ secrets.SERVER_USER }}
    key: ${{ secrets.SERVER_KEY }}
    command_timeout: 10m
    script: |
      echo "** Connected to server via SSH. **"
      echo "Running deploy script..."

      # Change working dir using absolute path
      cd /dir/to/github/repository
        
      echo "Pulling changes from main branch..."

      # Pull changes from main branch
      git pull origin main
        
      echo "** Pulled changes from main branch. **"

      # * Adjust the following according to your needs, or delete it entirely (up to you):

      # Optional #1: Run deploy script
      echo "Running deploy scripts..."

      # docker / docker-compose / npm / pip / etc. commands here
      # e.g., docker-compose up -d --build
      # e.g., npm install
      # e.g., pip install -r requirements.txt

      echo "Deploy scripts finished."

      # Optional #2: Run other commands
      echo "Running other commands..."

      # e.g., docker image prune -a -f
      # e.g., docker builder prune -f
      # e.g., docker system prune -a -f
      # e.g., update / upgrade / install / remove / search / autoremove / etc. commands here

      echo "Other commands finished."

      exit 0
```

## 🐳 Docker
```bash
# Docker commands
docker ps # show running containers
docker ps -a # show all containers
docker images # show images
docker volume ls # show volumes
docker volume inspect <volume> # show specific volume info (including mount point (absolute path to volume on host machine))
docker logs <container> # show container logs
docker logs <container> --follow # show container logs (follow)
docker logs <container> --tail 500 # show container logs (last 500 lines)
docker logs <container> --follow --tail 500 # show container logs (follow and last 500 lines)
docker exec -it <container> /bin/bash # get into container to run commands (sh)
docker exec -it <container> <command> # run command in container (no bash)

docker stop <container> # stop container (gracefully)
docker kill <container> # stop container (forcefully)

docker rm <container> # remove container
docker rm -f <container> # remove container (forcefully)

docker rmi <image> # remove image
docker rmi -f <image> # remove image (forcefully)

docker rm $(docker ps -a -q) # remove all containers
docker rm -f $(docker ps -a -q) # remove all containers (forcefully)

# remove all images
docker rmi $(docker images -q) # remove all images
docker rmi -f $(docker images -q) # remove all images (forcefully)

docker rm $(docker ps -a -q) && docker rmi $(docker images -q) # remove all containers and images
# remove all containers and images (forcefully)
docker rm -f $(docker ps -a -q) && docker rmi -f $(docker images -q) # remove all containers and images (forcefully)

docker image prune -a -f # purge all unused or dangling images (forcefully)
docker builder prune -f # purge all build cache (forcefully)
docker system prune -a -f # purge all unused containers, networks, images (both dangling and unreferenced), and optionally, volumes (forcefully)

# Docker Compose commands
docker-compose up -d --build # build and start containers
docker-compose down # stop and remove containers
docker-compose ps # show running containers
docker-compose exec <service> /bin/bash # get into container to run commands (sh)
docker-compose exec <service> <command> # run command in container (no bash)
docker-compose stop <service> # stop service
docker-compose kill <service> # stop service (forcefully)
docker-compose logs <service> # show service logs
docker-compose logs <service> --follow --tail 500 # show service logs (follow and last 500 lines)
```

# 🛡️ Security
```bash
# httpd-tools
sudo apt install httpd-tools # install httpd-tools
htpasswd -c <path/to/file> <username> # create htpasswd file
htpasswd -bc <path/to/file> <username> <password> # create htpasswd file with username and password (from command line)
htpasswd -bc -B5 -C 16 -r 100000 <path/to/file> <username> <password> # create htpasswd file. HIGHLY SECURE: bcrypt (16 rounds) & SHA-512 (100,000 rounds)
```

# 🛠️ Maintenance
```bash
# System
sudo apt update && sudo apt upgrade -y # update package list and upgrade packages

# System Resources
df -h # show disk usage
du -h --max-depth=1 /var/log # + specific folder disk usage
du -h --max-depth=1 /var/log | sort -hr # + sort disk usage by size
free -h # show memory usage
top # show cpu usage
htop # show cpu usage (better)

ip -c # show network interfaces
ip -c a # show ip addresses
ip -c r # show routing table

# Services / Processes
systemctl status <service> # show service status
systemctl start <service> # start service
systemctl stop <service> # stop service
systemctl restart <service> # restart service
systemctl enable <service> # enable service on startup
systemctl disable <service> # disable service on startup
systemctl list-unit-files --type=service # list all services (active and inactive)
systemctl list-units --type=service --all # list all services (active and inactive) (same as above)
systemctl list-units --type=service --state=active # list all active services
systemctl list-units --type=service --state=inactive # list all inactive services
systemctl list-units --type=service --state=failed # list all failed services

# Logs
journalctl -u <service> # show service logs
journalctl -u <service> -f # show service logs (follow)
journalctl -u <service> -n 100 # show service logs (last 100 lines)
journalctl -u <service> --since "2021-01-01 00:00:00" # show service logs (since date)

# Users
sudo adduser <username> # add user
sudo deluser <username> # delete user
sudo passwd <username> # change user password
sudo usermod -aG sudo <username> # add user to sudo group
sudo usermod -aG docker <username> # add user to docker group
sudo usermod -aG www-data <username> # add user to www-data group
sudo usermod -aG root <username> # add user to root group
sudo usermod -aG adm <username> # add user to adm group

# Groups
sudo addgroup <groupname> # add group
sudo delgroup <groupname> # delete group
sudo groupmod -n <newgroupname> <groupname> # rename group
sudo groupmod -g <gid> <groupname> # change group id
sudo groupmod -o -g <gid> <groupname> # change group id (allow duplicates)

# Permissions
sudo chown <username>:<groupname> <file> # change file owner
sudo chown -R <username>:<groupname> <directory> # change directory owner (recursive)
sudo chmod <permissions> <file> # change file permissions
sudo chmod -R <permissions> <directory> # change directory permissions (recursive)
sudo chown -R <username>:<groupname> <directory> && sudo chmod -R <permissions> <directory> # change directory owner and permissions (recursive)

# SSH
ssh-keygen -t rsa -b 4096 -C "<nameORemail>" # generate ssh key
ssh-copy-id <username>@<ip> # copy ssh key to server
ssh <username>@<ip> # ssh into server
ssh -i <path/to/key> <username>@<ip> # ssh into server with key
ssh -i <path/to/key> -p <port> <username>@<ip> # ssh into server with key and port

# Firewall
sudo ufw status # show firewall status
sudo ufw enable # enable firewall
sudo ufw disable # disable firewall
sudo ufw allow <port> # allow port
sudo ufw deny <port> # deny port
sudo ufw allow <port>/<protocol> # allow port and protocol
sudo ufw deny <port>/<protocol> # deny port and protocol
sudo ufw allow from <ip> # allow ip
sudo ufw deny from <ip> # deny ip
sudo ufw allow from <ip> to any port <port> # allow ip to port
sudo ufw deny from <ip> to any port <port> # deny ip to port
sudo ufw allow from <ip> to any port <port>/<protocol> # allow ip to port and protocol
sudo ufw deny from <ip> to any port <port>/<protocol> # deny ip to port and protocol

# Cron
crontab -e # edit crontab
crontab -l # list crontab
crontab -r # remove crontab
crontab -u <username> -e # edit crontab for user
crontab -u <username> -l # list crontab for user
crontab -u <username> -r # remove crontab for user
```

# 🚚 Server Migration
```bash
# MongoDB (scp)
sudo scp -r <path/to/local/directory> <username>@<ip>:<path/to/directory> # copy directory from one server to another

# MongoDB (mongodump & mongorestore) from docker-compose
docker-compose exec -T <mongodb service> sh -c 'mongodump --archive' > db.dump
docker-compose exec -T <mongodb service> sh -c 'mongorestore --archive' < db.dump
```

# 🐧 Gratitude
Thank you linux penguin for making life easier with regards to hosting / deployment. Would still not use you on main machine though lol.