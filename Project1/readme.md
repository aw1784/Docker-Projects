# Project 1
Setting up SSH connection between two Ubuntu containers in Docker
## Step 1: Create Docker Network (You can skip this step if you already have a network)
First, we need to create a Docker network that will allow our containers to communicate with each other. Run the following command in your terminal:
```
bash
docker network create my_network
```
## Step 2: Create and Run Ubuntu Containers
Next, we will create two Ubuntu containers and connect them to the network we just created. Run the following commands:
```
bash
docker run -d --name container1 --network my_network ubuntu:latest 
docker run -d --name container2 --network my_network ubuntu:latest 
```
## Step 3: Install SSH Server in Container1
Now, we need to install the SSH server in `container1`. First, access `container1` using the following command:
```
bash
docker exec -it container1 bash
```
Once inside the container, update the package list and install the OpenSSH server:
```
bashapt update
apt install -y openssh-server
```
## Step 4: Configure SSH Server
Next, we need to configure the SSH server. Create a directory for the SSH daemon and set the appropriate permissions:
```
nano /etc/ssh/sshd_config
```
output:
```
# SSH Server Configuration
#Port 22 
#Authentication settings
PermitRootLogin yes
#PasswordAuthentication yes
etc...
```
Then, start the SSH server:
```
bash
service ssh start
```
## Step 5: Set Root Password
To set a password for the root user in `container1`, run the following command inside `container1`:
```
bash
passwd root
```
You will be prompted to enter a new password for the root user. Make sure to remember this password, as you will need it to connect from `container2`.
## Step 6: Install SSH Client in Container2
Now, we need to install the SSH client in `container2` to connect to `container1`. First, access `container2` using the following command:
```
bash
docker exec -it container2 bash
```
Once inside `container2`, update the package list and install the OpenSSH client:
```
bash
apt update
apt install -y openssh-client
```
## Step 7: Get Container1 and Container2 IP Address
To connect to `container1` from `container2`, we need to know the IP address of `container1`. Run the following command in your terminal:
```
bash
docker inspect container1 container2 | grep -i IPAddress
```
Note down the IP address returned by the command, as you will need it to connect from `container2`.
## Step 8: Connect to Container1 from Container2
Now that we have the IP address of `container1`, we can connect to it from `container2`. Run the following command in `container2`:
```
bash
ssh root@<container1_IP_address>
```
Replace `<container1_IP_address>` with the actual IP address of `container1` that you noted down earlier. You will be prompted to enter the root password you set in Step 5. After entering the password, you should be successfully connected to `container1` from `container2` via SSH. You can now run commands in `container1` from `container2`.
## Conclusion
In this project, we successfully set up an SSH connection between two Ubuntu containers in Docker. We created a Docker network, ran two Ubuntu containers, installed and configured the SSH server in one container, and installed the SSH client in the other container to establish a secure connection. This setup allows us to manage and interact with one container from another using SSH.