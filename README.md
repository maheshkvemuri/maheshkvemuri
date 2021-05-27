## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/maheshkvemuri/maheshkvemuri/tree/main/Diagrams/ELK_Server.png


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

 pentest.yml : to install DVWA containers in web servers 
 
 install-elk.yml : to install elk container in elk server
 
 filebeat-playbook.yml : to install and launch filebeat on web servers
 
 filebeat-config.yml : filebeat config file
 
 metricbeat-config.yml : to install and launch metricbeat on web servers
 
 metricbeat-playbook.yml : metricbeat config file

### This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

What aspect of security do load balancers protect? 
Load balancer can add additional layers of security to the website without any chnages to your application. load balancers  
- Protect applications from emerging threats
- Authenticate User Access
- Protect against DDoS attack
- Simplify PCI compliance

What is the advantage of a jump box?
A jump box is simply a system, usually a single operating system, that is connected to two networks. The first of these networks is the common network and the second is the sensitive security zone. Jump boxes are usually used for a system tool that needs to connect directly to the devices on the security zone in question.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system metrics.
- Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name      | Function         | IP Address | Operating System |
|-----------|------------------|------------|------------------|
| Jump Box  | Gateway          | 10.0.0.4   | Linux            |
| Web-1     | DVWA Containers  | 10.0.0.7   | Linux            |
| Web-2     | DVWA Containers  | 10.0.0.8   | Linux            |
| web-3     | DVWA Containers  | 10.0.0.10  | Linux            |
| ELK Server| ELK              | 10.1.0.4   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

whitelisted IP addresses
123.243.76.253

Machines within the network can only be accessed by Jump Box.

ELK VM is accessed by Jump Box and the IP addresss is 13.73.112.60/10.0.0.4 

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump Box   | Yes                 | 123.243.76.253       |
| VM's       | No                  | 10.0.0.4             |
| ELK Server | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible?
- Ansible is simple, light weight IT automation engine that automates cloud provisioning, configuration management, application deployment, intra-service orchestration.

The playbook implements the following tasks:
    - Install docker.io
    - Install python3-pip
    - Install Docker module
    - Eable service docker on boot
    - Increase virtual memory
    - Use more memory
    - download and launch a docker elk container
    - publish ports elk runs on

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/maheshkvemuri/maheshkvemuri/tree/main/Diagrams/ELK_Container_Status.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
   10.0.0.7
   
   10.0.0.8
   
   10.0.0.10

We have installed the following Beats on these machines:
- filebeat
- metricbeat

These Beats allow us to collect the following information from each machine:
In each machine Filebeat monitors the log files or locations and collects log events, while metricbeats collect metrics and statistics

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to control node.
- Update the hosts file to include webservers and elk
- Run the playbook, and navigate to VM's to check that the installation worked as expected.

- _Which file is the playbook? Where do you copy it?_
playbook is a file where ansible code is written. playbook is written in YAML. YAML stands for Yet Another Markup Language. playbook is copied to Ansible control node.

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
host file is updated with machine ip-address to make the Ansible run the playbook on a specific machine. ipaddress is added in the hosts file under different sections as [webservers] and [elk] to specify the type of vm's.   
By specifying the type of vm's the playbook to install in 'hosts' section of playbook. In the install-elk.yml playbook, hosts: elk  specifiy the playbook to intstall elk on elk server and in filebeat-playbook.yml, hosts:webservers  specify the playbook to install filebeat on webservers that are listed in hosts file.  

- _Which URL do you navigate to in order to check that the ELK server is running?_
http://[ELK-Server-VM-public-ip]:5601/app/kibana
http://20.37.38.19:5601/app/kibana
 
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._


