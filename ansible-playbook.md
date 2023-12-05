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
