# ELKStackProject
Cybersecurity Bootcamp first project 

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics such as CPU usage, suo escalation failures, attempted SSH logins etc.

The configuration details of each machine may be found below.

| Name     	| Function   	| IP Address 	| Operating System 	|
|----------	|------------	|------------	|------------------	|
| Jump Box 	| Gateway    	| 10.0.0.7   	| Linux            	|
| Web-1    	| Server     	| 10.0.0.5   	| Linux            	|
| Web-2    	| Server     	| 10.0.0.6   	| Linux            	|
| Web-3    	| Server     	| 10.0.0.8   	| Linux            	|
| ELK-VM   	| Monitoring 	| 10.2.0.4   	| Linux            	|


In addition to the above, Azure has provisioned a load balancer for all machines except for the jump box. The load balancer's targets are organized into the following availability zones:
•	Availability Zone 1: Web-1, Web-2 and Web-3
•	Availability Zone 2: ELK-VM


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address: 174.105.138.216

Machines within the network can only be accessed by SSH into Jumpbox with public IP address 52.168.16.173.

A summary of the access policies in place can be found in the table below.
| Name     	| Publicly Accessible 	| Allowed IP Address 	|
|----------	|---------------------	|--------------------	|
| Jump Box 	| YES                 	| 174.105.138.216    	|
| Web-1    	| NO                  	| 10.0.0.7           	|
| Web-2    	| NO                  	| 10.0.0.7           	|
| Web-3    	| NO                  	| 10.0.0.7           	|
| ELK-VM   	| NO                  	| 10.0.0.7           	|


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it will ensure our automated configurations will do exactly the same thing every time they run, eliminating as much variability between configurations as possible.

The playbook implements the following tasks:
1.	Install docker.io
2.	Install pip3
3.	Install docker python module
4.	Download and launch a docker web container
5.	Enable docker service 


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

The playbook is duplicated below.

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

Web-1: 10.0.0.5
Web-2: 10.0.0.6
Web-3: 10.0.0.8

We have installed the following Beats on these machines:
Filebeat and metricbeat

These Beats allow us to collect the following information from each machine:

Filebeat monitors the log files or locations you specify, collects log events, and forwards them to elasticsearch or logstash for indexing. Some of the log types are Apache and nginx.

Metricbeat collects system’s metrics and application metrics and sends them to Elasticsearch. Some of the applications are Apache, NGINX

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible

- Update the hosts file to include the private IP address of the machines you want the playbook to run on. If the hosts file does not exist, create one in the /etc/ansible folder and add the IP addresses as shown in the example below: 

[webservers]
10.0.0.5 ansible_python_interpreter=/usr/bin/python3
10.0.0.6 ansible_python_interpreter=/usr/bin/python3
10.0.0.8 ansible_python_interpreter=/usr/bin/python3

[elk]
10.2.0.4 ansible_python_interpreter=/usr/bin/python3

- Run the playbook with the command: ansible-playbook (name of playbook) (machine name). eg. ansible-playbook elkplaybook.yml webservers. 

After running the playbook, navigate to http://<ELK.VM.External.IP>:5601/app/kibana to check that the installation worked as expected.

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
