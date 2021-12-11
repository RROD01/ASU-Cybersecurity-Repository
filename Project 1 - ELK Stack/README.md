# Docker-Setup-and-ELK-Stack-Deployment
Diagram and setup of how a VNet was established with VM web servers and an ELK stack server.
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Images/ELK_Network_Diagram.drawio.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ELK_Deployment_Playbook.txt file may be used to install only certain pieces of it, such as Filebeat.

Files/ELK_Deployment_Playbook.txt

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting access to the network.
Load balancers help protect against Denial of Service (DoS) attacks through redundancy. Additionally, with the use of a jump box, this will prevent all of the other VMs from being exposed to the public (only the jump box will be exposed via the internet).

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
Filebeat will monitor for changes in log files and the locations that log events occur.
Metricbeat records system and server stats/metrics and how they are running while up.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                 | Function         | IP Address | Operating System |
|----------------------|------------------|------------|------------------|
| Jump-Box-Provisioner | Gateway          | 10.0.0.4   | Linux            |
| Web-1                | Web Server       | 10.0.0.5   | Linux            |
| Web-2                | Web Server       | 10.0.0.6   | Linux            |
| ELK-VM               | ELK Stack Server | 10.1.0.5   | Linux            |

### Access Policies 

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
98.171.51.154/32

Machines within the network can only be accessed by the Jump-Box-Provisioner.
Jump-Box-Provisioner the Jump-Box-Provisioner IP Address is variable and changes once turned on (40.112.224.57/32)

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses |
|----------------------|---------------------|----------------------|
| Jump-Box-Provisioner | Yes                 | 98.171.51.154/32     |
| Web-1                | No                  | 10.0.0.5             |
| Web-2                | No                  | 10.0.0.6             |
| ELK-VM               | No                  | 10.1.0.5             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it reduces the chances for errors and saves time.

The playbook implements the following tasks:
- Install Docker downloads and extracts the docker.io application onto the VM.
- Python3-pip installs the pip package management system allowing python to work with and process the ELK packages.
- vm.max_map_count expands the virtual memory to allow the VM to properly support the ELK stack.
- Download Image sebp/elk:761 downloads and launches the ELK package on the container.
- Enable docker allows for the ELK services to be up and running when the VM starts up.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Images/docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1: 10.0.0.5
Web-2: 10.0.0.6

We have installed the following Beats on these machines:
Filebeats
Metricbeats

These Beats allow us to collect the following information from each machine:
- The Filebeat collects data on the system log files on the web servers, such as system logs that deal with user logon events.
- The Metricbeat collects on the status of the system, such as how long the OS has been running or what applications are being ran on it.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ELK_Deployment_Playbook.txt file to /etc/ansible.
- Update the ELK_Deployment_Playbook.txt file to include the configuration for your IP address and the security group to allow access to the port. 
- Run the playbook, and navigate to http://<ELK IP Address>:5601/app/kibana to check that the installation worked as expected.
