# Setup Jenkins in EC2 Ubuntu 16

sudo add-apt-repository ppa:webupd8team/java

sudo apt update
sudo apt install oracle-java8-installer

sudo apt install oracle-java8-set-default

cd /tmp && wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
echo 'deb https://pkg.jenkins.io/debian-stable binary/' | sudo tee -a /etc/apt/sources.list.d/jenkins.list

sudo apt update
sudo apt install jenkins

# Start and Stop Jenkins 

sudo systemctl stop jenkins.service
sudo systemctl start jenkins.service
sudo systemctl enable jenkins.service

# Get initial Jenkins Password

sudo cat /var/lib/jenkins/secrets/initialAdminPassword

# Setup Docker

sudo apt-get remove docker docker-engine docker.io
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install docker-ce
sudo usermod -aG docker ubuntu
sudo usermod -aG docker jenkins
sudo reboot

