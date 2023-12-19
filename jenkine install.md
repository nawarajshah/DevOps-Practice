## Install jenkins in a docker container on ubuntu
### Install ubuntu Docker image

	curl -s https://get.docker.io/ubuntu/ | sudo sh

### Pull jenkins docker image

	sudo docker pull orchardup/jenkins

### Start jenkins container

	sudo docker run -d -p 80:8080 orchardup/jenkins

### Access it the public ip of ec2 instance
