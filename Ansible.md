<h1> Ansible Configuration Management tool </h1>

<h2>Introduction</h2>
Configuration management tools are essential in the field of IT to automate and streamline the process of configuring and managing the software and hardware infrastructure of a system. These tools play a crucial role in ensuring consistency, efficiency, and security across multiple servers and devices. 

There are two primary types of configuration management tools: push-based and pull-based.
<h3>Push-Based Configuration Management:</h3>
Example Tools: Ansible, SaltStack
In push-based configuration management, a central server actively pushes configuration updates to the target nodes.
Users have direct control over when updates are pushed, providing a higher degree of control.
Ansible, for instance, utilizes YAML (Yet Another Markup Language) for configuration files and operates on a key-pair basis.
Push-based tools are beneficial when precise control over the update process is required.

<h3>Pull-Based Configuration Management:</h3>
Example Tools: Chef, Puppet
In pull-based configuration management, nodes periodically check with a central server to fetch and apply configurations.
This approach is advantageous when dealing with scenarios where new machines are added, as they automatically check and synchronize with the central server.
Chef and Puppet are examples of pull-based tools commonly used in enterprise environments.
Ansible:

<h3>Architecture:</h3>
Ansible uses a server-client architecture where the Ansible server communicates with nodes (systems to be configured).
It operates in a push mode, directly pushing updates and configurations to the nodes.
Ansible is agentless, meaning it doesn't require an agent to be installed on nodes. Communication is established through SSH.
Scripting Language: Ansible uses YAML for its configuration files and playbooks.

<h3>Advantages:</h3>
<ul>
<li>Open Source: Ansible is an open-source tool, making it accessible and adaptable for a wide range of users.</li>
<li>Consistency: Ansible ensures consistency in configurations across multiple nodes.</li>
<li>Lightweight: Ansible is known for its lightweight nature, making it easy to deploy and use.</li>
<li>Security: The agentless architecture and integration with OpenSSH enhance security.</li>
</ul>

<h2>Ansible Terminology</h2>
<h3>Ansible Server</h3>
The machine where Ansible is installed and used to run tasks and playbooks. It serves as the control node.

<h3>Module</h3>
A module is a command or set of similar commands meant to be executed on the client (managed) side. Modules are the building blocks for tasks in Ansible playbooks.

<h3>Task</h3>
A task is a unit of work in Ansible, representing a single procedure to be completed. Tasks are defined in playbooks and are executed on the managed hosts.

<h3>Role</h3>
A way of organizing tasks and related files to promote reusability and maintainability. Roles are collections of playbooks, variables, and files grouped together for easier management.

<h3>Fact</h3>
Information fetched from the managed host, representing global variables about the host's characteristics. Facts are automatically collected by Ansible and can be used in playbooks for conditional execution.

<h3>Inventory</h3>
A file containing data about client servers, such as IP addresses, hostnames, and connection details. The inventory file is where you define the hosts that Ansible will manage.

<h3>Play</h3>
The execution of a playbook. A play consists of one or more tasks applied to a specific set of hosts defined in the inventory.

<h3>Handler</h3>
A task that is called only if a specific condition is met. Handlers are often used for actions like restarting a service after a configuration change.

<h3>Notifier</h3>
A section attributed to a task that calls a handler if the output is changed. It is used to trigger specific actions based on the result of a task.

<h3>Playbook</h3>
A script written in YAML format that describes a set of tasks to be executed on one or more hosts. Playbooks define the desired state of the system.

<h3>Host</h3>
Nodes or servers that are automated by Ansible. Hosts are defined in the inventory file and are the target machines for Ansible tasks and playbooks.
