# Playbook:

- Playbooks in Ansible are written in YAML format.
- YAML is a human-readable data serialization language, commonly used for configuration files.
- A playbook is like a file where we write code. It consists of sections such as vars, tasks, handlers, files, templates, and roles.
- Each playbook is composed of one or more 'tasks' listed in a sequence. A task is a module, which is a collection of configuration files.

## Playbooks are divided into sections like:
- Target section: defines the host against which playbook tasks have to be executed.
- Variable section: Defines variables.
- Task section: A list of all modules that need to run in order.

# YAML:
For Ansible, nearly every YAML file starts with a list.
Each item in the list is a collection of key-value pairs, commonly called a dictionary.
All YAML files have to begin with "---".
We can write a playbook, and to dry-run it to see changes without applying it:
```
ansible-playbook <<filename.yml>> --check
```

# Gathering Facts of Nodes using playbook:
```
--- # Testing YAML Playbook
- hosts: demo
  user: ansible
  become: yes
  connection: ssh
  gather_facts: yes
```
- ---: Marks the beginning of a YAML document.
- Testing YAML Playbook: A comment providing a description or purpose for the playbook.
- -: Indicates the start of a new YAML list item.
- hosts: demo: Specifies the target hosts for the playbook. In this case, it targets the group named "demo."
- user: ansible: Specifies the remote user (ansible) to use when connecting to target hosts.
- become: yes: Activates privilege, allowing tasks to run with privileges (typically using sudo).
- connection: ssh: Specifies the connection method to use (SSH in this case).
- gather_facts: yes: Enables the gathering of facts about the target hosts before executing tasks. Facts include information about the host's hardware, operating system, IP addresses, etc.

# Installing HTTPD on Nodes using the module in playbook:
```
---
- hosts: demo
  user: ansible
  become: yes
  connection: ssh
  tasks:
    - name: Install HTTPD on nodes
      yum:
        name: httpd
        state: present
```
- tasks: Indicates the start of the tasks section.
- -name: Install HTTPD on nodes: Defines a task named "Install HTTPD on nodes" for human readability.
- yum: Specifies the Ansible module to use (yum in this case) for package management.
- name: httpd: Specifies the name of the package to be installed (httpd).
- state: present: Specifies that the package should be present, effectively installing it.

# Variables:
Variables are used to store and retrieve data in playbooks or tasks. They can be defined at various levels.
```
---
- hosts: demo
  user: ansible
  become: yes
  connection: ssh

  vars:
    pkgname: httpd

  tasks:
    - name: Install httpd on nodes
      yum:
        name: "{{ pkgname }}"
        state: present
```
- vars: Indicates the start of the variables section.
- pkgname: httpd: Defines a variable named "pkgname" with the value "httpd." This variable will be used later in the playbook.
- name: "{{ pkgname }}": Specifies the name of the package to be installed, using the value of the "pkgname" variable.
# Handler:
A handler is like a task but will only run when called by another task. It is used to perform actions like restarting a service, triggered only if a specific condition is met during playbook execution.
```
---
- hosts: demo
  user: ansible
  become: yes
  connection: ssh

  vars:
    pkgname: httpd

  tasks:
    - name: Install httpd on nodes
      yum:
        name: "{{ pkgname }}"
        state: present
      notify: Restart Service

  handlers:
    - name: Restart Service
      service:
        name: httpd
        state: restarted
```
- notify: Restart Service: Sends a notification to the handler named "Restart Service" after the task completes.
- handlers: Indicates the start of the handlers section.
- -name: Restart Service: Defines a handler named "Restart Service" for human readability.
- service: Specifies the Ansible module to use (service in this case) for managing services.
- name: httpd: Specifies the name of the service to be managed (httpd).
- state: restarted: Specifies that the service should be restarted.

# Loop in Ansible Playbook
A loop in Ansible is a construct that allows you to repeat a particular task or set of tasks for each item in a list or a range. It simplifies the playbook by reducing redundancy and promoting reusability.
## Loop for Adding Users to multiple hosts
```
---
- hosts: demo
  user: ansible
  become: yes
  connection: ssh

  vars:
    user_list:
      - user1
      - user2
      - user3

  tasks:
    - name: Add users
      user:
        name: "{{ item }}"
        state: present
      loop: "{{ user_list }}"
```
- vars:: Indicates the start of the variables section.
- user_list:: Defines a variable named "user_list" as a list containing user names to be added.
- tasks:Indicates the start of the tasks section.
- -name: Add users: Defines a task named "Add users" for human readability.
- user:Specifies the Ansible module to use (user in this case) for managing users.
- name: "{{ item }}": Specifies the name of the user to be added, using the loop variable "{{ item }}" to iterate over the "user_list."
- state: present: Specifies that the user should be present, ensuring it is added.
- loop: "{{ user_list }}": Defines a loop over the "user_list," adding each user in the list.
