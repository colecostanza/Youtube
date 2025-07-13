## Setting Up PiHole - Linux, Windows, Docker

The video tutorial can be found [here](https://www.youtube.com/watch?v=0QN1tkib8kk).
### Description

In this video, I’ll show you how to install PiHole on bare metal, in a Docker container, and on Windows. PiHole is a network-wide ad blocker that blocks ads and trackers, improving privacy, speeding up browsing, and reducing bandwidth usage. Self-hosting PiHole gives you full control over your data and enhances network security, without relying on third-party services. Whether you’re using old hardware, Docker, or Windows, PiHole is a great way to protect your network and improve your online experience. Plus, by setting up PiHole, you’ll sharpen your IT skills, learning more about networking, Linux, and Docker management in the process. It’s a great way to dive deeper into self-hosting and system administration!
### Installing on Bare Metal Linux Server

```
sudo apt update && sudo apt upgrade -y

sudo curl -sSL https://install.pi-hole.net | bash
```
### Installing as a Docker Container

This can be run as a shell script or by running the commands individually.

```
#Apply updates
sudo apt update && sudo apt upgrade -y

#If you dont have Curl install curl with:
sudo apt install curl

#Install Docker
sudo curl -fsSL https://get.docker.com | sudo shclear

#Install Docker-Compose
sudo apt-get install docker-compose-plugin

#Create directory for Docker-Compose files
mkdir -p /docker/pihole/compose

#Create docker-compose.yml file
sudo nano /docker/pihole/compose/docker-compose.yml

#Paste Compose Script
##################################################################################
version: "3"

services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "80:80/tcp"
    environment:
      TZ: 'Etc/UTC'
    volumes:
      - /docker/pihole/configs:/etc/pihole
      - /docker/pihole/dnsmasq.d:/etc/dnsmasq.d
    restart: unless-stopped

###################################################################################

#Run docker compose
sudo docker compose -d

#If you get port 53 in use error:
sudo systemctl stop systemd-resolved && sudo systemctl disable systemd-resolved

#To run commands within docker container:
sudo docker exec -it pihole sh

#To change pihole password:
sudo pihole -a -p

```

### Resources Used
Special thanks to Hagezi for the DNS blocklist https://github.com/hagezi/dns-blocklists#pro.
