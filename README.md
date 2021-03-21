## Description
The aim of this project is to create a Docker Swarm with two VMs.

I used Vagrant for the preovision of two CentOS VMs on VirtualBox and an Ansible playbook to install e configure the Docker Swarm.

Tested on Ubuntu 20.04.2 LTS
## Technologies used
Ansible 2.9.6
Vagrant 2.2.6
## Additional note 
The additional linter command in .travis-yml  
```
ansible-lint -x command-shell
```
is to avoid errors relating to the direct execution of commands in the shell. To install Docker on the CentOS 8 VMs I needed to execute dnf commands and I wasn't able to find a suitable replacement in the Ansible dnf module.
## Security Issues
As said above, some of the commands are executed in the VMs shell, which is not ideal. The entire Playbook is also executed as root, without taking advantage of the privilege escalation option offered by Ansible. In addition I didn't expose the Docker APIs in a secure way to send commands and setup the swarm, I did all of that with a direct ssh connection to the VMs and the execution of commands in the shell of the machine.

All of this was the simplest solution given my current knowledge, in order to deliver this project in an reasonable time frame.
## References
Besides the official documentation for Ansible, Vagrant and Docker I used this projects and articles as resources for the implementation of the various functions:
* [Hands-On: Provision a Docker Swarm Cluster with Vagrant and Ansible](https://github.com/acuto/swarm-vagrant-ansible) by **acuto**
* [6 practices for super smooth Ansible experience](https://max.engineer/six-ansible-practices) by **Max Chernyak**
## Future improvements 
* Adding Molecule testing 
* Exposing Docker Daemon APIs
