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
  - [Vanity aliases](#vanity-aliases)
- [📦 Package Managers](#-package-managers)
  - [Apt](#apt)
  - [Yum](#yum)
- [🎁 Useful packages](#-useful-packages)
  - [Essentials](#essentials)
  - [Vanity](#vanity)
- [🚀 Devops](#-devops)
  - [🔐 SSH](#-ssh)
  - [🐳 Docker](#-docker)
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
alias dockerps='docker ps'
alias dockerpsa='docker ps -a'
alias dockerimages='docker images'
alias dockervols='docker volume ls'
alias dockervol='docker volume inspect'
alias dockerlogs='docker logs --follow --tail 500'
alias dockerexec='docker exec -it'
alias dockerstop='docker stop'
alias dockerkill='docker kill'
alias dockerrm='docker rm'
alias dockerrmi='docker rmi'
alias dockerrmall='docker rm $(docker ps -a -q) && docker rmi $(docker images -q)'
alias dockerrmallf='docker rm -f $(docker ps -a -q) && docker rmi -f $(docker images -q)'
alias dockerprunei='docker image prune -a -f'
alias dockerpruneb='docker builder prune -f'
alias dockerprunes='docker system prune -a -f'
alias dockerpruneall='docker image prune -a -f && docker builder prune -f && docker system prune -a -f'
```

## Vanity aliases
```bash
alias ls='exa -Fg -l --icons --group-directories-first' # prerequisities: exa
alias df='df -h'
alias ip='ip -c'
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
sudo apt install exa # ls replacement
sudo apt install bat # cat replacement
sudo apt install htop # top replacement
```

# 🚀 Devops

## 🔐 SSH
```bash
ssh-keygen -t ed25519 -a 100 # generate strong public/private key
ssh-copy-id <username>@<ip> # copy ssh key to server
ssh <username>@<ip> # ssh into server
ssh -i <path/to/key> <username>@<ip> # ssh into server with key
ssh -i <path/to/key> -p <port> <username>@<ip> # ssh into server with key and port
```

## 🐳 Docker
```bash
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