## Setting Up PiHole - Linux, Windows, Docker

The video tutorial can be found [here](https://www.youtube.com/watch?v=R55Rcv8fwsY&t=367s).
### Description

This video tutorial requires no domain and is 100% free as long as you own spare hardware. Why Nextcloud is the Best Choice for Your Private Cloud | Simple Setup Guide 

Worried about who’s accessing your data in the cloud? With Nextcloud, you can keep your files completely private by storing them on your own hardware. Unlike other cloud services, where your data is stored on someone else’s servers, Nextcloud lets you keep control. It’s secure, customizable, and gives you peace of mind. 

Plus, setting up your own Nextcloud server is a great way to learn more about technology. Even if you’re not an IT expert, this project can help you understand the basics of how networks and data security work. And as you gain these skills, you’ll be ready to tackle more tech projects in the future. Ready to take control of your data?

### Update Linux

```
sudo apt update && sudo apt upgrade -y
```

### Installing Docker

```
curl -fsSL https://get.docker.com | sudo sh
```

### NextCloud Docker Deploy Script

```
docker run -d \ 
--name=nextcloud \ 
-e PUID=1000 \ 
-e PGID=1000 \ 
-e TZ=Etc/UTC \ 
-p 443:443 \ 
-v /var/lib/docker/volumes/Nextcloud/config:/config \ 
-v /Your/Data/Path:/data \ 
--restart unless-stopped \ 
lscr.io/linuxserver/nextcloud:latest
```

### Allowing Local FQDN Access

Open NextCloud config.php and add the FQDN under IP address:

`sudo nano /var/lib/docker/volumes/Nextcloud/config/www/nextcloud/config/config.php`

```
array(
	0=> "192.168.0.85", # <---- Your server IP address
		"Your.local.FQDN", # <---- Place FQDN here.
),
```