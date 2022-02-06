# Vanderbilt-Project1

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
 



 Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ___Yaml__ file may be used to install only certain pieces of it, such as Filebeat.

![image](https://user-images.githubusercontent.com/90538632/152669164-8053d1fa-1d10-4800-afdc-c4fac4f44d7f.png)

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available_____, in addition to restricting ___Access__ to the network.

- What aspect of security do load balancers protect? What is the advantage of a jump box?_
Load Balancers work by proctecting again DDoS attacks. LB’s Determines what server to send the traffic to. It prevents one server from getting overloaded with traffic and distributes the traffic evenly throughout the servers. A jump box limits the access that the public has to your virtual network because in order to access the other virtual machines, an individual needs the private IP’s of the machines. A jump box allows more control over the virtual network



Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the ___Logs__ and system __Traffic___.
 
What does Filebeat watch for? Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.

 What does Metricbeat record?_Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.5   | Linux            |
| Web-1    |     Web Server used to run DVWA     |     10.0.0.4       |     Ubuntu Linux             |
| Web-2     |    Web Server used to run DVWA     |   10.0.0.6         |      Ubuntu Linux                         |
| ElkNet    |     Run Elk Container & Kibana     |        |    10.3.0.4              | Ubuntu Linux                         

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the __Jump-Box-Provisioner___ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Add whitelisted IP addresses 
47.184.73.103

Machines within the network can only be accessed by _JBP VM____.
- Which machine did you allow to access your ELK VM? Jump-Box-Provisioner 

 What was its IP address?_ 20.127.48.27

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes            | 20.127.48.27   |
|    Web-1      |    No                 |       10.0.0.4               |
|     Web-2     |    No                 |        10.0.0.6              |

 Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

The playbook implements the following tasks:
-  In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
•	The first task of the elk playbook installs docker.io on the Elk virtual machine
•	Python is then installed on the Elk VM
•	Downloads, installs and executes the docker elk container on the Elk vm on restart so the elk container doesn't need to be manually started
•	This enables docker on boot so you don't have to manually start docker when you turn your VM back on.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/90538632/152669200-b8cad346-935f-4be5-9d4d-8b61dd7f8a05.png)

Target Machines & Beats
This ELK server is configured to monitor the following machines:
-  List the IP addresses of the machines you are monitoring_
	Web-1 10.0.0.4
	Web-2 10.0.0.6

We have installed the following Beats on these machines:
-Specify which Beats you successfully installed_
	Filebeat and Metricbeat were installed. 

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
	Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash. 

Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the __Filebeat-config.yml___ file to __/etc/ansible/files/filebeat-config.yml___.
- Update the __ Filebeat-config.yml___ ___ file to include host 10.3.0.4:9200 with username elastic an dpassword changeme an dsetup.Kibana host to 10.1.4.4:5601
- Run the playbook, and navigate to _Kibana___ to check that the installation worked as expected.

![image](https://user-images.githubusercontent.com/90538632/152669235-b90183bd-9c83-4346-a0db-1201d4f324e8.png)
 
_Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Filebeat-playbook.yml  Where do you copy it? /etc/ansible/files/filebeat-config.yml

- _Which file do you update to make Ansible run the playbook on a specific machine? Filebeat-config.yml How do I specify which machine to install the ELK server on versus which to install Filebeat on? First, we need to ssh into our jump-start VM with the public IP 20.127.48.27. We had to add our private IP to this host file. We added our Elk server to this host along with our two web VM’s. Elk Server (10.3.0.4). we added this to the config file to specify the location for the installation. (See links below)

https://github.com/Amoseley77/Vanderbilt-Project1/blob/main/Ansible/Filebeat-config.yml

https://github.com/Amoseley77/Vanderbilt-Project1/blob/main/Ansible/Host



- _Which URL do you navigate to in order to check that the ELK server is running?

http://13.78.131.33:5601/app/kibana#/home.


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc. 

https://github.com/Amoseley77/Vanderbilt-Project1/blob/main/Ansible/metric-config.yml

To create/edit: nano nameofplaybook.yml

To run the playbook: ansible-playbook nameofplaybook.yml

