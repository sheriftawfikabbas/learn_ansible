# Write basic ansible playbooks

Ansible is an IT automation software that can easily automate a IT system admin tasks. To achieve such automation, Ansible get its instructions from a playbook, which you will learn how to write in this project. First, you will learn how to setup an inventory of hosts which, for our case here, will only contain one hosts, which is the local host. You will learn how to run Ansible ad-hoc commands. Then you will learn what an Ansible playbook looks like, and how to write a playbook to perform basic operations. You will write playbooks to run file tasks and to setup software.

## Objectives
Understand the purpose of Ansible as an IT automation system
Understand the structure and function of playbooks
Understand how to perform basic tasks ad-hoc and with playbooks


## Tasks
- Setup your Ansible inventory
- Execute ad-hoc commands
- Understand the structure and syntax of the playbook yaml file
- Write a playbook that performs basic operations
- Write a playbook that performs file operations
- Write a playbook that installs software



### Task 1. Setup your Ansible inventory
Ansible is a simple IT automation system. That is, it automates a range of IT system administration tasks, including system configuration, setting up and deploying applications in a network, cloud provisioning, task execution, network automation, and multi-node orchestration. 

You find the word “orchestration” frequently used for Ansible, and that’s because of how Ansible really works: imagine your computer network, whether big or small, as an orchestra. Ansible makes one computer node acts as the maestro, the manager of that orchestra. 

The music notebook that the maestro reads and manages the orchestra with, that’s the ansible playbook. Writing the music notebook, or the playbook, is what we will be learning in this project.

In Ansible, the maestro is called the Ansible server.


cd Desktop
cd pos
code .

Let’s have a look at the hosts file, and add the localhost
vi /etc/ansible/hosts
Let’s see how this file is structured. You can write the IP addresses or names of your hosts straightaway, or group them into groups using the square brackets.

Task 2: Execute ad-hoc commands
Ad-hoc commands are a quick way to run commands in ansible. Ansible provide a rich list of such commands in case you are on a hurry and want to update some software, clear out some storage, or any small task, and don’t have time to sit down and write a playbook.
In this task we are 
going to demo a few of those ad-hoc commands.
Display all hosts: --list-hosts parameter
ansible --list-hosts all
Create a new hosts file and add a host: localhost. Then display all hosts: -i parameter to identify hosts inventory file
ansible --list-hosts -i hosts all
Ping the hosts available: -m parameter
ansible all -i hosts -m ping -c local
Response:
localhost | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
Explanation: successful execution of Ansible task. “changed”: whether a host was changed at all. In this case, nothing changed in any host.
Copy a file
ansible -i hosts all -m copy -a "src=/etc/ansible/hosts dest=./testfile" -c local

Task 3: Understand the structure and syntax of the playbook yaml file

So far we’ve been executing ad-hoc commands. Now let’s learn how to create the playbook.
A Playbook is a set of plays, each play is a set of tasks. Each play and task can be given a name.
Each play has two key attributes: name and tasks. You can also add other attributes to a play to modify its behavior.
The syntax looks as follows:
---
-	name: Play 1
hosts: all
connection: local #only when we are only connecting to localhost
become: true # like calling sudo
tasks:
#Task 1
- name: Task 1 of play 1
   Module name
Play attributes here include:
•	Hosts: which group of hosts to apply changes to, or are we doing this to all?
•	Connection: specify local if we are applying the play to localhost
•	Become: in case we need to sudo or su to escalate privilates, set it to true
Ansible playbooks support a large number of modules, which you can find here: 
https://docs.ansible.com/ansible/2.9/modules/archive_module.html#archive-module
In this tutorial we are going to use the following modules:
ping
apt: to setup new software
shell: execute shell commands
command: execute commands
archive: archive files into a zip, gz, bzip2 or lzma
copy: copy a file from a src to a dist
debug: printing things while execution
find: find a file based on give criteria
Task 4: Write a playbook that performs basic operations

In this task we will learn how to write a playbook that performs the following tasks: create a folder, create a file into a folder and delete a folder. We will perform these tasks via the modules: command, shell and archive.
We will also learn how to register an output variable, so you can get Ansible to print out things while it is performing a task, or to print out the results of executing a task.

Task 5: Write a playbook that performs file operations

In this task we will learn how to write a playbook that perform basic file operations: archive a folder, copy a file from a source to a destination directory, and finding a file based on criteria.
Task 6: Write a playbook that installs software
In this task we will learn how to write a playbook that installs software using the apt module. We will use the apt module to remove software, install software and update the apt cache. We will install software by also calling apt via the command module.



