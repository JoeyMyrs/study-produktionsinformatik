# Installation instructions (Ubuntu 22.04 LTS)
## Requirements
- Linux machine (This installation instructions are specifically for Ubuntu 22.04 LTS, can be different for other distributions)
- git has to be installed and configured on the machine
```
  git config --global user.name "Max Mustermann"
  git config --global user.email "max.mustermann@gmail.com"
```
## Install and configure Docker
### Install updates
```
sudo apt update && sudo apt upgrade
```
### Remove old Docker versions (Not needed on new machine)
```
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```
### Add Docker's official GPG key (Only for Ubuntu, see docker documentation)
```
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```
### Add the repository to Apt sources (Only for Ubuntu, see docker documentation)
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update && sudo apt upgrade
```
### Install Docker packages
```
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
### Add current user to Docker group
```
sudo gpasswd -a $USER docker
```
## Install and configure Docker infrastructure for Smartfactory
### Clone repository to local machine
```
git clone https://github.com/JoeyMyrs/study-produktionsinformatik.git ./study-produktionsinformatik
```
### Set ownership for repository to current user
```
sudo chown -R $USER:$USER ./study-produktionsinformatik
```
### Make start and stop script executable
```
chmod +x ./study-produktionsinformatik/start.sh ./study-produktionsinformatik/stop.sh
```
## Run Docker infrastructure for Smartfactory
### Start
```
./start.sh
```
### Stop
```
./stop.sh
```
### Access infrastructure
- Node-RED: http://localhost:1880/
- InfluxDB: http://localhost:8086/
- Grafana: http://localhost:3000/
