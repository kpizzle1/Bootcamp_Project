## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/kpizzle1/Bootcamp_Project/blob/master/Diagrams/ELK%20Stack%20Diagram_HW.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  https://github.com/kpizzle1/Bootcamp_Project/blob/master/playbook_files/filebeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _____, in addition to restricting _____ to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
It acts as a gateway distributes traffic from clients across multiple servers without the clients having to understand how many servers are in use or how they are configured.Because the load balancer sits between the clients and the servers it can enhance the user experience by providing additional security, performance, resilience and simplify scaling your website. 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?_It collect docker logs
- _TODO: What does Metricbeat record?_It logs the connections 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web 1    | Webserver| 10.0.0.5   | Linux            |
| Web 3    | Webserver| 10.0.0.6   | Linux            |
| ELK      | ELK Stack| 10.1.0.5   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ___jumpbox__ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 174.56.223.174

Machines within the network can only be accessed by _Jumpbox____.
- Which machine did you allow to access your ELK VM? jumpbox What was its IP address? 52.183.86.151 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 174.56.223.174       |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible? automating Docker and operationalizing the process of building and deploying containers, Free, Agentless

The playbook implements the following tasks:
- - name: Play Web - Create apache directories and username in web servers
    hosts: webservers
    become: yes
    become_user: root
    tasks:
- - name: create username apacheadm
        user:
          name: apacheadm
          group: users,admin
          shell: /bin/bash
          home: /home/weblogic

-  - name: install httpd
        yum:
          name: httpd
          state: installed

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

-shows that the ELK container is running with the correct ports

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
10.0.0.5
10.0.0.6
We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
metricbeats
filebeats
These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

Filebeat is a lightweight shipper for logs.Filebeat comes with internal modules (Apache, Cisco ASA, Microsoft Azure, NGINX, MySQL, and more) that simplify the collection, parsing, and visualization of common log formats down to a single command. Metricbeats is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml
dpkg -i filebeat-7.4.0-amd64.deb
Copy the Filebeat configuration file from your Ansible container to your WebVM's
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_. /etc/ansible/hosts. Add the IP to the config file 
- _Which URL do you navigate to in order to check that the ELK server is running? http://52.247.27.37:5601/app/kibana#/home

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
