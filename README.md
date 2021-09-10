# ELK-to-STACK
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Red-Team Network](https://github.com/jlashay/ELK-to-STACK/blob/main/Diagrams/hwdia.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook YAML file may be used to install only certain pieces of it, such as Filebeat.

-![Elk deployement](https://github.com/jlashay/ELK-to-STACK/blob/main/Ansible/install-elk.yml)


This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
-The aspect of security a load balancer protects is availbity. It distrubites traffic through multiple servers which can preven a Denial of Service Attack.
-The advantage of a a jump box is that it control access to other servers by a single node intead of mutiple conncections. It only allows connectiong from specified IP addresses.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat watches for system logs data and montiors and reports changes made on the server.
- Metricbeat records data of running services on your server, and forwards the collected data to Elasticsearch.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function  | IP Address | Operating System |
|----------|-----------|------------|------------------|
| Jump Box | Gateway   | 10.0.0.5   | Linux            |
| Web-1 VM | Web Server| 10.0.0.8   | Linux            |
| Web-2 VM | Web Server| 10.0.0.7   | Linux            |
| ELK VM   | Web Server| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Local/Personal IP Address 72.210.65.178

Machines within the network can only be accessed by _____.
- Jumpbox | IP private : 10.0.0.5 | IP public : 20.102.120.182

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |  72.210.65.178       |
| Web-1 VM | No                  |  10.1.0.4            |
| Web-2 VM | No                  |  10.1.0.4            |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because the services running can be limited, installations and updates to the system can be streamlined, and the process are replicable.

-An main advantage of automating configuration with Ansible is that it is written in Python; which is a human readable langauage.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- The first install task is for docker.io installations, so we would be able to use the docker engine to run and controll the state of our Ansible containers. Then in order to start the docker, we create a dcker 
- We used a a map count task to allow of target machine to user more memory so our Elk can run.
- Also, another task in the installation is to list the ports that the elk server runs on, and downloading

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Elk docker ps](https://github.com/jlashay/ELK-to-STACK/blob/main/images/setpelkscreenshot.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 VM 10.0.0.8
- Web-2 VM 10.0.0.7

We have installed the following Beats on these machines:
-Filebeats ![Filebeat YAML](https://github.com/jlashay/ELK-to-STACK/blob/main/Ansible/filebeat.yml)
-Metricbeats 

These Beats allow us to collect the following information from each machine:
- Filebeats helps collect_TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible playbook file to the roles directory created.
- Update the hotst file to include the servers for Ansible to connect to. You can specify which yaml playbook file to run on which machine by specifying the group to run it on (i.e webservers or elk).
- Run the playbook, and navigate to http://40.112.190.157:5601/app/kibana to check that the installation worked as expected.
- To check the data being recevied; on the Kibana site, you can click on the check data option. 

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
-First, you will have to be inside of your ansible container. Syntax "sudo docker start (container name)", then use the syntax "sudo docker attach (container name).
-Next, you will navigate to your anisble directory using the syntax "cd ~/etc/ansible/". 
-To update a host file, you would need to " nano host" , then iput the IP address of the Elk and webservers group with the ending syntax of  "ansible_python_interpreter=/usr/bin/python3".
-To run the yaml playbook file, you will need to enter the sytax " ansible-playbook (yaml file name)" into the command line.
