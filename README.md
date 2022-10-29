# TW_CS_Bootcamp_Project_1
Repo for all Project 1 Deliverables including all asnible playbooks and network diagrams
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below:

 TW_CS_Bootcamp_Project_1/Diagrams/Elk_Vnet-Diagram_All_Red_Team.drawio.png 

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible playbooks may be used to install only certain pieces of it, such as Filebeat.

  -  TW_CS_Bootcamp_Project_1/Ansible/install-elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network, by requiring all SSH access to webservers to be directed through the jump-box machine

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the machines and system file structures.

The configuration details of each machine may be found below:

| Name      | Function | IP Address | Operating System |
|---------- |----------|------------|------------------|
| Jump-Box  | Gateway  | 10.0.0.4   | Linux            |
| Elk-Server| Monitor  | 10.1.0.4   | Linux            |
| Web-1     | server   | 10.0.0.5   | Linux            |
| Web-2     | server   | 10.0.0.6   | Linux            |
| DVWA-Web3 | server   | 10.0.0.7   | Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
 185.207.249.10

Machines within the network can only be accessed by Jump-Box (10.0.0.4)

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses |
|-----------|---------------------|----------------------|
| Jump Box  | Yes/No              | 185.207.249.10       |
| Elk-Server| No                  | 10.0.0.4             |
| Web-1     | No                  | 10.0.0.4             |
| Web-2     | No                  | 10.0.0.4             |
| DVWA-Web3 | NO                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous as it allows for easy and convenient destruction and redployment of machines if need be

The playbook implements the following tasks:
- Installs docker.io
- Installs python3-pip
- Installs docker module
- Increases virtual memory
- Download and launches a docker elk container
- Enables docker service on boot 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

 TW_CS_Bootcamp_Project_1/Screenshots/Week_13_ansible_playbook_success.png 

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 (10.0.0.5)
- Web-2 (10.0.0.6)
- DVWA-Web3 (10.0.0.7)

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects log events then inpsects and analyzes the compiled log files
- Mtericbeat collects metrics from the VMs Operating Systems and services

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. These steps are largely the same for Metricbeat and Filebeat. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the filebeat configuration file to /etc/ansible/files/filebeat-config.yml.
- Update the filebeat config file to include the private IP address of the Elk-Server VM at line #1106 and line #1806
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.
- Commands are listed below:
-  curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml
-  nano --linenumbers filebeat-config.yml
-  Create playbook and run it with ansible-playbook filebeat-playbook.yml 
