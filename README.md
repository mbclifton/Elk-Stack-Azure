## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

- (Images/RedTeam network diagram.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

  - ansible-playbook.yml
  - filebeat-playbook.yml

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
- What aspect of security do load balancers protect? Availability. 
- What is the advantage of a jump box? You can use it to deploy containers (pre-set configurations) to multiple machines quickly.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system access.
- What does Filebeat watch for? Activity involving the file system.
- What does Metricbeat record? Machine metrics, such as uptime.

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | WebServer| 10.0.0.5   | Linux            |
| Web-2    | Webserver| 10.0.0.6   | Linux            |
|ELK-SERVER|Log Server| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 65.118.17.50

Machines within the network can only be accessed by the RedTeam Jump Box.
- 104.214.98.188

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |     No              | 65.118.17.50 (SSH)   |
| Web-1    |     Yes (on Port 80)|                      |
| Web-2    |     Yes (on Port 80)|                      |
|ELK-SERVER|     No              | 65.118.17.50 (SSH)   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it avoids human error and can be done quickly.

The playbook implements the following tasks:
- install docker
- enable docker service
- download and launch/start a docker container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

-(Images/docker ps on ELK-SERVER.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5 (Web-1)
- 10.0.0.6 (Web-2)

We have installed the following Beats on these machines:
- Filebeat
(NOTE: I was not able to complete the bonus "Metricbeat" installation successfully despite repeated attempts and help from Stephen P. and Scotty H.)

These Beats allow us to collect the following information from each machine:
- Filebeat collects data about the file system. Filebeat monitors log files, or it can also be set to monitor specific locations. Filebeat centralizes log management. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible-playbook.yml file to /etc/ansible
- Update the ansible.cfg file to include the hosts' network IP addresses
- Run the playbook, and navigate to http://23.101.113.54:5601/ to check that the installation worked as expected.