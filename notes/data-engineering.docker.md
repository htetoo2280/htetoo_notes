---
id: vtnax07km54wm49ou0gcjkk
title: Docker
desc: ''
updated: 1762571562061
created: 1761214129788
---



ssh tony@172.16.238.10

to check linux - 
sudo su

to check linux version - cat etc/*release

to check is installed 
	- docker --version
	- docker compose version

to start docker 
	- systemctl start docker
	- systemctl status docker

### creating container and using image (name = nginx , tag = alpine)
	- sudo docker pull nginx:alpine (optional but good)
	- sudo docker run -d --name nginx_3 nginx:alpine
🔹 -d → run in detached mode (background)
🔹 --name nginx_3 → sets container name
🔹 nginx:alpine → image to use

### delete docker container 
	- sudo docker stop kke-container
	- sudo docker rm kke-container


------------------- 

