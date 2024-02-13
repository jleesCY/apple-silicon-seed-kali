### Task 1: Setup
The Labsetup document provided on canvas is not the correct architecture for our system (provided is amd64, we need arm64). The arm version of the same docker containers is available on the seed website for download. However, this does not include `attacker.c`. I have provided an identical file for download, which includes the `attacker.c` file, and works on the UTM SEED machine:
[`Labsetup-arm.zip`](https://1drv.ms/u/s!As06ehb0pJGBh-xjFfEAAmUqQ0Tnxg?e=oe7QS3) (Onedrive, 8.44 KB)

#### Install the correct version of Docker
Docker-compose is not installed by default on the UTM SEED machine. To do so, we need to jump through a few hoops.

Ensure everything is up to date:
```
sudo apt-get update; sudo apt-get upgrade
```

Add the docker repository key:
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Add the Docker ARM64 Repository
```
sudo add-apt-repository "deb [arch=arm64] https://download.docker.com/linux/ubuntu focal stable"
```

Install dependencies
```
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

Install docker (run this even if it may already be installed)
```
sudo apt install -y docker-ce
```

Verify Docker Installation
```
sudo systemctl status docker
```

If it is not started, start it
```
sudo systemctl start docker
```

If it fails to start, wait for a bit longer, then try starting it again

Lastly, ensure everything is up-to-date once more:
```
sudo apt-get update; sudo apt-get upgrade
```

#### Install docker-compose
Get the binary
```
sudo curl -L “https://github.com/docker/compose/releases/download/v2.18.1/docker-compose-$(uname -s)-$(uname -m)” -o /usr/local/bin/docker-compose
```

Make it executable
```
sudo chmod +x /usr/local/bin/docker-compose
```

Verify the installation
```
docker-compose --version
```

#### Edit aliases
SEED already has aliases set up, but we need to edit them. Edit ~/.bashrc by: adding `sudo` to all docker commands

The final docker aliases section of ~/.bashrc will look like:
```
# Commands for for docker 
alias dcbuild='sudo docker-compose build'
alias dcup='sudo docker-compose up'
alias dcdown='sudo docker-compose down'
alias dockps='sudo docker ps --format "{{.ID}}  {{.Names}}"'
docksh() { sudo docker exec -it $1 /bin/bash; }
```
