<h1> Ansible Configuration and Automation </h1>
<h2>Introduction</h2>
In the realm of IT, the role of a system administrator traditionally involved managing servers, including tasks such as installing applications, changing IP addresses, creating users, and overall system maintenance. Configuration management tools have become crucial for automating and streamlining the process of configuring and managing software and hardware infrastructure, ensuring consistency, efficiency, and security across multiple servers and devices. Two primary types of configuration management tools are push-based and pull-based.

Push-Based Configuration Management
Example Tools: Ansible, SaltStack

In push-based configuration management, a central server actively pushes configuration updates to the target nodes.
Users have direct control over when updates are pushed, providing a higher degree of control.
Ansible, for instance, utilizes YAML (Yet Another Markup Language) for configuration files and operates on a key-pair basis.
Push-based tools are beneficial when precise control over the update process is required.
Pull-Based Configuration Management
Example Tools: Chef, Puppet

In pull-based configuration management, nodes periodically check with a central server to fetch and apply configurations.
This approach is advantageous when dealing with scenarios where new machines are added, as they automatically check and synchronize with the central server.
Chef and Puppet are examples of pull-based tools commonly used in enterprise environments.
Ansible Overview
Type: Push-based configuration management tool.
Acquisition: Red Hat acquired Ansible in 2015.
Architecture:
Ansible employs a server-client architecture where the Ansible server communicates with nodes (systems to be configured).
It operates in a push mode, directly pushing updates and configurations to the nodes.
Ansible is agentless, meaning it doesn't require an agent to be installed on nodes. Communication is established through SSH.
Scripting Language: Ansible uses YAML for its configuration files and playbooks.
Advantages:
Open Source: Ansible is an open-source tool, making it accessible and adaptable for a wide range of users.
Consistency: Ansible ensures consistency in configurations across multiple nodes.
Lightweight: Ansible is known for its lightweight nature, making it easy to deploy and use.
Security: The agentless architecture and integration with OpenSSH enhance security.
Configuration Management Concepts
Configuration management involves the systematic handling of changes to a system's configuration in a way that maintains integrity and traceability. It includes processes, tools, and techniques to automate and manage the configuration of software and hardware components in an IT infrastructure. The goal is to ensure that systems are configured correctly, securely, and consistently, reducing manual errors and enhancing overall system reliability and security.

Ansible Terminology
Ansible Server
The machine where Ansible is installed and used to run tasks and playbooks. It serves as the control node.

Module
A module is a command or set of similar commands meant to be executed on the client (managed) side. Modules are the building blocks for tasks in Ansible playbooks.

Task
A task is a unit of work in Ansible, representing a single procedure to be completed. Tasks are defined in playbooks and are executed on the managed hosts.

Role
A way of organizing tasks and related files to promote reusability and maintainability. Roles are collections of playbooks, variables, and files grouped together for easier management.

Fact
Information fetched from the managed host, representing global variables about the host's characteristics. Facts are automatically collected by Ansible and can be used in playbooks for conditional execution.

Inventory
A file containing data about client servers, such as IP addresses, hostnames, and connection details. The inventory file is where you define the hosts that Ansible will manage.

Play
The execution of a playbook. A play consists of one or more tasks applied to a specific set of hosts defined in the inventory.

Handler
A task that is called only if a specific condition is met. Handlers are often used for actions like restarting a service after a configuration change.

Notifier
A section attributed to a task that calls a handler if the output is changed. It is used to trigger specific actions based on the result of a task.

Playbook
A script written in YAML format that describes a set of tasks to be executed on one or more hosts. Playbooks define the desired state of the system.

Host
Nodes or servers that are automated by Ansible. Hosts are defined in the inventory file and are the target machines for Ansible tasks and playbooks.

Setting Up Ansible on AWS Instances
Step 1: Launch AWS Instances
Launch three EC2 instances on AWS.
Access all machines using PuTTY, including going inside the Ansible server.
Step 2: Install Ansible on the Ansible Server
bash
Copy code
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
adduser ansible
passwd ansible
su - ansible

# Grant sudo permissions to the ansible user
visudo
# Add: ansible ALL=(ALL) NOPASSWD:ALL

# Repeat the above steps on all nodes where you want the ansible user

# Connect to nodes through SSH
vi /etc/ssh/sshd_config
# Uncomment: PermitRootLogin yes, PasswordAuthentication yes
# Comment: PasswordAuthentication no
# Restart SSH configuration: service sshd restart
# Connect to nodes using SSH: ssh ansible@<<ipaddress>>

# Download and install Ansible
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
yum install epel-release-latest-8.noarch.rpm
yum install ansible
Step 3: Establish SSH Connections
Generate an SSH key on the Ansible server: ssh-keygen
Copy the SSH key to nodes: ssh-copy-id ansible@<<ipaddress>>
Step 4: Check Hosts Connected to Ansible Server
bash
Copy code
ansible all --list-hosts
Ansible Modules: Ad-hoc Commands
Ad-hoc commands are used for quick, one-time-use tasks:

bash
Copy code
# Example: Check files in all hosts belonging to the 'demo' group
ansible <groupname> -a "ls"

# Update files for the 'demo' group
ansible <groupname> -a "touch filez"
Ansible Modules: Predefined Commands
Ansible ships with predefined modules for various tasks:

bash
Copy code
# Install or update httpd package
ansible <groupname> -b -m yum -a "pkg=httpd state=present"

# Update httpd package to the latest version
ansible <groupname> -b -m yum -a "pkg=httpd state=latest"

# Remove httpd package
ansible <groupname> -
