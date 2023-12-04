# Setting Up Ansible on AWS Instances
## Step 1: Launch AWS Instances. 
1. Launch EC2 instances on AWS.
2. Access all machines using PuTTY, including going inside the Ansible server.

## Step 2: Install Ansible on the Ansible Server

```console
# Download the EPEL Ansible installation script
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

# Install necessary software
yum install git python python-level python-pip openssl ansible -y

# Edit the Ansible hosts file
vi /etc/ansible/hosts
# Add the IP addresses of the host nodes

# Edit the main Ansible configuration file
vi /etc/ansible/ansible.cfg
# Uncomment the inventory and sudo lines

# Create a user on the Ansible server
adduser <<put username>>
passwd <<put password>>
su - ansible - this will let you switch user as ansible user

# Grant sudo permissions to the ansible user
visudo
# Add: ansible ALL=(ALL) NOPASSWD:ALL

# Repeat the above steps on all nodes where you want the ansible user

# Settings to connect to nodes through SSH
vi /etc/ssh/sshd_config
# Uncomment: PermitRootLogin yes, PasswordAuthentication yes
# Comment: PasswordAuthentication no
# Restart SSH configuration: service sshd restart
# Connect to nodes using SSH: ssh ansible@<<ipaddress>>
```

## Step 3: Establish SSH Connections (Setting Up SSH Key-Based Authentication)
- Generate an SSH key on the Ansible server: ssh-keygen
- Copy the SSH key to nodes: ssh-copy-id ansible@<<put ipaddress>>

## Check Hosts Connected to Ansible Server
```
ansible all --list-hosts
```
