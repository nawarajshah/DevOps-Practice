
## Scan Docker Image with Trivy
### Make instance with ubuntu 22.04
Go to aws account and create instance as in yesterday session with **ubuntu** as OS.

Install updates

	sudo apt update

### Install Docker in ubuntu
Run the following command to uninstall all conflicting packages:

    for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
    
Set up Docker's `apt` repository.

    # Add Docker's official GPG key:
	sudo apt-get update
	sudo apt-get install ca-certificates curl gnupg
	sudo install -m 0755 -d /etc/apt/keyrings
	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
	sudo chmod a+r /etc/apt/keyrings/docker.gpg

	# Add the repository to Apt sources:
	echo \
	  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
	  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
	  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
	sudo apt-get update

Install the latest version of Docker packages.

	sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

Check docker version for installation 

	sudo docker --version
	
Refrence: [docs.docker.com](https://docs.docker.com/engine/install/ubuntu/)

### Install Trivy Vulnerability Scanner in ubuntu 22.04

	sudo snap install trivy

Refrence: [snapcraft.io](https://snapcraft.io/install/trivy/ubuntu)

### Download and run Docker Image

Clone docker image from github.

	git clone https://github.com/nemanjam/mern-docker.git

Enter into *dockerized-mern-app* folder

	cd mern-docker

Run docker image

	sudo docker compose up -d

Check **Process Status**

	sudo docker ps

Let's examine **mern-docker-client** image.

	sudo trivy image --scanners vuln mern-docker-client
