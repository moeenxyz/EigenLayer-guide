EigenLayer Node Operator Guide

Introduction

Welcome to the EigenLayer Node Operator Guide. This step-by-step tutorial will assist you in setting up and running a node on EigenLayer.

Connect with Me
Twitter
Lens Profile
If you find this guide helpful, consider delegating to me:

Moeen's Operator Profile
Setting Up Your Node

Choosing a VPS
For optimal performance, it's recommended to purchase a Virtual Private Server (VPS) with the following minimum specifications:

vCPUs: 16
Memory: 32GB
Storage: 3.6T (High-performance SSD)
Network Utilization: 24 Mbps download, 120 Mbps upload, Peak 1 Gbps
Suggested EC2 Equivalent: m5.4xlarge
I personally use Hetzner. Here's a referral link that provides €20 credit: Hetzner Cloud.

Operating System Requirements
Preferred OS: Ubuntu 22.04
Recommended CPU: AMD
Installation Steps

Update Ubuntu
First, update your Linux system:

shell
Copy code
sudo apt update
sudo apt upgrade
Installing Docker and Docker Compose
Install Docker and Docker Compose using the following commands:

shell
Copy code
# Adding Docker's GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Adding Docker repository:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
Verify Docker installation:

shell
Copy code
sudo docker run hello-world
Next, install Docker Compose:

shell
Copy code
sudo apt install docker-compose
sudo curl -L https://github.com/docker/compose/releases/download/v2.16.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker compose version
You should see: Docker Compose version vX.XX.X

Installing EigenLayer CLI
Download and install the EigenLayer CLI:
