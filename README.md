## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](https://github.com/ishara66/ishara66/blob/main/Diagrams/Project%20Diagram.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  [Filebeat-Playbook](https://github.com/ishara66/ishara66/blob/main/Ansible/Roles/filebeat-playbook.yml.txt)
  
  [Metricbeat-Playbook](https://github.com/ishara66/ishara66/blob/main/Ansible/Roles/metricbeat-playbook.yml.txt)
  
  [DVWA-Playbook](https://github.com/ishara66/ishara66/blob/main/Ansible/DVWA-Playbook/pentest.yml.txt)
  
  [ELK-Playbook](https://github.com/ishara66/ishara66/blob/main/Ansible/ELK-Playbook/install%20Elk.playbook.txt)
  
This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient and responsive to users, in addition to restricting unwanted access to the network.

-A Load Balancer is the process of distrubting workload evenly across muntiple servers and protect the system by defending against DDoS attacks.  

-What is the advantage of a jump box?
It is the gateway that all user need to connect to a jumpbox before connecting  to any virtual machine or lunching any administrative task to avoid malicious attack.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.
- Filebeats collects the file events,monitors the log files and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat records periodically collected metrics.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    |Server    | 10.0.0.5   | Linux            |
| Web-2    |Server    | 10.0.0.6   | Linux            |
| ELK-VM1  |ELK Server| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My workstation or My device ip address.

Machines within the network can only be accessed by jump box provisioner.

-10.0.0.4 (Private IP),


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | yes                 | 98.169.52.4          |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
|ELK-VM1   | yes                 | 98.169.52.4          |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it has been tested and trobleshooted.
-Playbooks are written in YML and eays for the beginners to troubleshoot.

The playbook implements the following tasks:
-In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

-At first SSH to Jump-Box (ssh sysadmin@13.82.52.22)

-Start and attach the ansible docker like sudo docker start stoic_kapitsa and sudo docker attach stoic_kapitsa

-Navigate /etc/ansible and create install-elk.yml using nano

-Run (ansible-playbook /etc/ansible/roles/install-elk.yml) command to run that playbook

-Finally, SSH to ELK-VM1 to verify that this VM is running or not.



The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](https://github.com/ishara66/ishara66/blob/main/ELK-Images/Docker%20ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

-Web-1 (10.0.0.5)
-Web-2 (10.0.0.6)

We have installed the following Beats on these machines:

-Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:

-Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing. 
-Metricbeat monitor servers by collecting metrics from the system and services running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the configuration file to /etc/ansible/files and playbook to /etc/ansible/roles
- Update the host file to include the private IP address of the machine you wish install and configure ELK in.
- Run the playbook, and navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana to check that the installation worked as expected.

Which file is the playbook? Where do you copy it?

filebeat-playbook.yml and copy to /etc/ansible/roles.

Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?

You must update the hosts file in the etc/ansible directory. By adding the private ip address of the specific machine or machines you wish to install ELK or Filebeat on.

Which URL do you navigate to in order to check that the ELK server is running?
http://40.86.81.132:5601/app/kibana
