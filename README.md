## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.


<figure><img src=/Diagrams/Elkproject.png><figcaption></figcaption></figure>


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _playbook__ file may be used to install only certain pieces of it, such as Filebeat.




This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _available___, in addition to restricting ___traffic__ to the network.


- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_    Load balancers play a crucial role as computing moves evermore to cloud.It requests for authentication (username/password) before accessing any website to mitigate any unauthorized access.

A jump box is a secure computer that all admins first connect to before launching any administrative task  to connect to other servers or untrusted environments. It prevents Azure Virtual machines from being exposed to the public. It also helps to open one port instead of several ports to connect different Vms present in the azure cloud.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the __logs__ and system __traffic___.

:What does Filebeat watch for?_

Filebeat works as an agent on our servers. Their aim is to record information about the system by monitoring the log files or locations that we specify,collect log events and forward them to Elasticsearch or Logstash for indexing.
 
 What does Metricbeat record?
Metricbeat is responsible for collecting hosts' metrics and statistics periodically from the operating system and services running on the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                Function            | IP Address | Operating System |
|---------------------|------------------|----------------|------------------|
| Jump Box        | Gateway             | 10.0.0.4    |   Linux            
| Web-1             |  Server          |  10.0.0.10   |   Linux
| Web-2             |  Server          |  10.0.0.6    |   Linux
| Elk server       |  Monitoring        |    10.1.1.4   |   Linux  



### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_99.235.137.134  (My public ip address) 

Machines within the network can only be accessed by __Jump Box Provisioner___.
- _TODO: Which machine did you allow to access your ELK VM? Jump Box Provisioner will have access to ELK VM
 What was its IP address?_ Private ip address: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name            | Publicly Accessible | Allowed IP Addresses |
|-------------------|---------------------------|----------------------|
| Jump Box      |      Yes                    | 99.235.137.134  (internet,my public ip)
|  Web-1           |       Yes                   |   10.0.0.4(Jump box) , 20.106.144.83 (load balancer)   
|  Web-2          |        Yes                   | 10.0.0.4 (Jump box)  ,  20.106.144.83 (load balancer)
|    Elk                       Yes       | 99.235.137.134(my public i  ,10.0.0.0/16(red team virtual network)
### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

What is the main advantage of automating configuration with Ansible?_
The main advantage of automating configuration with Ansible are as follows:
Reliable :  Users can set up the entire application environment no matter where it’s deployed. They can also change based on their needs. 
Robust :  Ansible automates and simplifies, complex and tedious IT workflow operations.
Free : Ansible is an open source tool.
Agentless: Users don’t need to install any other software or firewall ports on the client systems.
Efficient:  We don’t need to install any extra software. There is more room for application resources on the server.
 
The playbook implements the following tasks:
 In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._


Install docker.io
Install pip3
Install docker python module
Increase virtual memory
Download and launch a docker elk_container
Enable service on boot



The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
<figure><img src=/Screenshots/Elk project.PNG><figcaption></figcaption></figure>




### Target Machines & Beats
This ELK server is configured to monitor the following machines:
List the IP addresses of the machines you are monitoring_


WEB-1     Private ip address: 10.0.0.10
WEB-2     Private ip address : 10.0.0.6

We have installed the following Beats on these machines:
Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._


Filebeat :  Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash

Metricbeat : Metricbeat is responsible for collecting hosts’ metrics and statistics periodically.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the __playbook.yml___ file to ansible__.
- Update the ____config.yml_ file to include...ip address of web server and elk
- Run the playbook, and navigate to __kibana__ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_

Filebeat and metricbeat
I copied to /etc/ansible/roles
- _Which file do you update to make Ansible run the playbook on a specific machine? The host files

How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

For Web-1 and Web-2 virtual machines, I have placed them under [websevers] and create an independent category for [elk] under all the web servers.

- _Which URL do you navigate to in order to check that the ELK server is running?
My Elk server public ip address is 102.37.124.15. 
http://102.37.124.15:5601/app/kibana  I used this link to check my elk server is running.


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

To download the playbook

ansible-playbook metricbeat-playbook.yml

ansible-playbook filebeat-playbook.yml


To update the files


Nano the files in specific location or directory to update

I 
ansible-playbook install-elk.yml

