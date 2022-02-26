sudo apt-get update

#Install this one by one incase of error on PUTTY terminal 
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

OR

On other Terminal
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common


curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-get install docker-ce docker-ce-cli containerd.io

The above command couldn't work, so trying this one below
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu `lsb_release -cs` test"
sudo apt update

sudo apt upgrade

sudo apt install docker-ce

apt-cache madison docker-ce

sudo apt-get install docker-ce docker-ce-cli containerd.io

sudo apt install docker.io

sudo apt install docker-compose

Check docker version, to confirm we have docker installed
docker -v

then copy your project to the server
scp -i "nathawspb.pem" -r flask-standard ubuntu@ec2-13-58-101-54.us-east-2.compute.amazonaws.com:~/ubuntu/

then build your app
sudo docker-compose build

to run docker in background
sudo docker-compose up -d

Then add your expose docker container to the security group,
the 9900 is my docker container while 8080 is for nginx
check the ec2-docker.jpg in the images folder


check all network details
sudo netstat -tulpn


HOW TO VIEW NGINX LOG
for example, container-name = nginx-standard
sudo docker logs -f container-name 1>/dev/null

HOW TO VIEW NGINX ACCESS LOG 
sudo docker logs -f nginx-standard 2>/dev/null














