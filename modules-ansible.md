# Ansible Modules: Predefined Commands
<p> Modules in Ansible are small, standalone scripts that carry out tasks on managed nodes. They are the building blocks of Ansible playbooks and ad hoc commands. 
  Modules performs specific actions, such as managing files, installing packages, or restarting services on remote hosts. </p>

```
# Install or update httpd package
ansible <groupname> -b -m yum -a "pkg=httpd state=present"

# Update httpd package to the latest version
ansible <groupname> -b -m yum -a "pkg=httpd state=latest"

# Remove httpd package
ansible <groupname> -b -m yum -a "pkg=httpd state=absent"
```
## Explaination of above commands
- ansible <groupname>: This part specifies the Ansible command to target a group of hosts defined in inventory. Replace <groupname> with the actual name of your host group.

- -b (or --become): This option instructs Ansible to run the command with sudo privileges.

- -m yum: This specifies the Ansible module to use. In this case, it's the yum module, which is responsible for managing packages on systems that use the YUM package manager.

- -a "pkg=httpd state=present": This is the argument section. It provides parameters to the yum module.
  <p> pkg=httpd: Specifies the name of the package (httpd) to be installed.</p>
  <p>state=present: Ensures that the specified package is present on the system. If it's not installed, Ansible will install it. </p>
