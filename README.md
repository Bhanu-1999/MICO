EC2 Jenkins Setup and Configuration [installed jenkins, ansible]
Connecting to EC2 Instance:

SSH into the EC2 instance:
bash
ssh -i "path_to_your_jenkins.pem" ubuntu@<EC2_PUBLIC_IP>
Setting the Hostname:

Set the hostname for the instance:
bash
sudo hostnamectl set-hostname JENKINS
Updating and Installing Jenkins:

Update package lists:
bash
sudo apt update
Add Jenkins GPG key and repository:
bash
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update

Install Jenkins:
bash
sudo apt-get install jenkins
User Management:

Add Jenkins user to the sudo group and set up a password:
bash
sudo usermod -aG sudo jenkins
sudo adduser jenkins
sudo passwd jenkins

Verify Jenkins user:
bash
id jenkins
Installing Ansible and Dependencies:

Install necessary software packages and Ansible:
bash
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
Installing Python and Docker Support:

Install Python 3, pip, Docker libraries:
bash
sudo apt install python3-pip python3-docker
python3 -m venv venv
sudo apt install pipx
pipx install docker
python3 -m venv myenv
source myenv/bin/activate
pip install docker
deactivate

Managing SSH Keys:
Generate SSH keys for Jenkins:
bash
ssh-keygen

Copy the SSH public key to the target system:
bash
cd ~/.ssh
cat id_pub
Setting Up Playbooks:

Create playbook directories and manage Ansible playbooks:
bash
mkdir ~/playbooks
cd playbooks/
nano deployment.yaml
Working with Jenkins Projects:

Navigate to Jenkins workspace and manage project files:
bash
cd /var/lib/jenkins/workspace/<project_name>/
Docker Setup:

Install Docker and configure it:
bash
sudo apt install docker.io
Running Ansible Playbooks:

Execute the Ansible playbook:
bash
ansible-playbook name.yaml

Docker EC2 Setup and Configuration
Connecting to EC2 Instance:




SSH into the EC2 instance:[installed Docker]
bash
ssh -i "path_to_your_dockerdock.pem" ubuntu@<EC2_PUBLIC_IP>
Setting the Hostname:

Set the hostname to "DOCKER":
bash
sudo hostnamectl set-hostname DOCKER
Adding a New Docker User:

Create a new user docker and assign a password:
bash
sudo adduser docker

Add the user to the sudo and docker groups:
bash
sudo usermod -aG sudo docker
sudo usermod -aG docker docker

Set a new password for the docker user:
bash
sudo passwd docker
Installing Docker:

Update package lists:
bash
sudo apt-get update

Install required dependencies:
bash
sudo apt-get install ca-certificates curl

Add Docker's official GPG key:
bash
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

Add the Docker repository to your system:
bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

Update package lists again to include Docker repository:
bash
sudo apt-get update
Installing Docker Components:

Install Docker Engine, CLI, and associated plugins:
bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

Adding User ubuntu to the Docker Group:

Added the ubuntu user to the Docker group to enable Docker commands without sudo:
bash
sudo usermod -aG docker ubuntu
Attempt to Run Docker Commands as ubuntu:

Executed newgrp docker to apply the group change without logging out:
bash
newgrp docker
Rebooting the EC2 Instance:

Rebooted the EC2 instance to apply changes:
bash
sudo reboot
Reconnecting to EC2:

Reconnected to the EC2 instance using SSH:
bash
ssh -i "C:\Users\bhanu\Downloads\dockerdock.pem" ubuntu@<EC2_PUBLIC_IP>
Running Docker Command Successfully:

Verified that Docker was functioning correctly by running docker ps without any permission issues:
bash
docker ps
Switching to Root User:

Set a new password for the root user:
bash
sudo passwd root
Successfully Switched to Root:

Successfully switched to the root user after setting the password:
bash
su root

-->Generated SSH key pair (id_ed25519) for root, saved in /root/.ssh/, and updated authorized_keys.
-->Attempted Docker login but canceled due to web-based authentication issues.
-->Fixed typo in Dockerfile (ngnix → nginx) and successfully built Docker image mico:latest.
-->Ran mico-container exposing port 80.
-->Moved project files to /root/project/ and cleaned up the ansible-jenkins-pipeline folder.


"After successfully building the Docker image and running the mico-container, I was able to access the mico application through the exposed port."😊




