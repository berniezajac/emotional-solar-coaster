Raspberry Pi:

* Fresh image - ensure 64bit install of Raspberry Pi OS

Steps:

```
# initial
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install git vim
sudo reboot

# install docker
cd ~
mkdir workspace
cd ~/workspace/
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
usermod -aG docker pi
sudo usermod -aG docker pi

# install docker-compose
sudo apt-get install libffi-dev libssl-dev
sudo apt install python3-dev
sudo apt-get install -y python3 python3-pip
sudo pip3 install docker-compose

# setup ssh
cd ~
mkdir .ssh
touch ~/.ssh/github_id_rsa
chmod 600 ~/.ssh/github_id_rsa
echo -e "Host github.com\n\tHostName github.com\n\tIdentityFile ~/.ssh/github_id_rsa" >> ~/.ssh/config

# clone repo (this repo - lol)
cd ~/workspace/
git clone git@github.com:berniezajac/emotional-solar-coaster.git

# set perms on bound volume directories
cd ~/workspace/emotional-solar-coaster
mkdir -p influxdb/data && sudo chown -R 472:472 influxdb/data
mkdir -p grafana/data && sudo chown -R 472:472 grafana/data

# update main.env with enphase ip and JWT
nano main.env

docker-compose up
```

