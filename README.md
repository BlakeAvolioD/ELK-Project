## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Images/ELK-Stack-Project.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the '*.yml' files may be used to install only certain pieces of it, such as Filebeat.

  - Playbooks-YAML/install-elk-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly stable, in addition to restricting access to the network.

- Load balancers protect the amount of traffic going into and out of a server or database.
- A Jump-box creates one point of entry for a group of machines. Adding an extra layer of security as well as one point to administrate those machines.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system files.
- Filebeat checks for changes to files or logs.
- Metricbeat records the services and system OS files.

The configuration details of each machine may be found below.


| Name       | Function | Private IP address | Public IP Address | Operating System   |
|------------|----------|--------------------|-------------------|--------------------|
| Jump Box   | Gateway  | 10.0.0.4           | 20.24.95.142      | Linux Ubuntu 18.04 |
| Elk Server | Monitor  | 10.1.0.5           | Dynamic           | Linux Ubuntu 18.04 |
| Web-1      | DVWA     | 10.0.0.5           | 20.239.131.49     | Linux Ubuntu 18.04 |
| Port-80    | DVWA     | 10.0.0.6           | 20.239.131.49     | Linux Ubuntu 18.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My home IP Address

Machines within the network can only be accessed by the ansible docker container installed on the jump-box.
- The Jump-Box machine has access through the 10.0.0.4 to the ELK machine by 10.1.0.5

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses      |
|---------------|---------------------|---------------------------|
| Jump Box      | No                  | 10.0.0.5 1.0.0.6 10.1.0.5 |
| Elk Port 5601 | Yes                 | My Home IP                |
| SSH to Jump   | Yes                 | My Home IP                |
| Port-80       | Yes                 | My Home IP                |
| Elk Port 80   | Yes                 | My Home IP                |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Automation removes human error and makes a time consuming job for small to large companies easy and quick. 

The playbook implements the following tasks:
- Install and download docker
- Install Python3 for Yaml 
- Use more memory for container to run
- Start ELK service and enable for future use

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Images/docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.5
- Web-2: 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects specified files and logs, for eample it will collect log events or changes to specified log files.
- Metricbet will record the servive logs and operating system logs. If a change is made on how the server or database runs a file of that event will be made.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the '$BEAT.config' file to '/etc/$BEAT/$BEAT.yml' file.
- Update the /etc/anisble/hosts file to include the desired webservers or groups of machines/containers you wish to habe these configurations and plays on.
- Run the playbook, and navigate to https://(ELK-Public-IP):5601/app/kibana to check that the installation worked as expected.


Commands to run:
- docker start [CONTAINER]
- docker attach [CONTAINER]
- curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat >> /etc/ansible/filebeat-config.yml
- nano /etc/$BEAT/$BEAT-config.yml
- ansible-playbook $BEAT-playbook.yml