# Elk
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Azure Cloud Network.drawio.png] (/Users/cindygutierrez/Documents/GitHub/Diagrams/Azure Cloud Network.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - Elk.yml_

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
- What aspect of security do load balancers protect? 
    - Load balancers protects the system from DDoS attacks by shifting attack traffic.
  	- Load Balancing contributes to the Availability aspect of security in regards to the CIA Triad.
 
- What is the advantage of a jump box?
    - The advantage of a jump box is to give access to the user from a single node that can be secured and monitored.
   	- The advantage of a Jump Box is the orgination point for launching Administrative Tasks. This ultimately sets the JumpBox as a SAW (Secure Admin Workstation). All Administrators when conducting any Administrative Task will be required to connect to the Jump Box (SAW) before perfoming any task/assignment.
   	
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files, logs and system metrics.
- What does Filebeat watch for?
    - Filebeat watches for any information in the file system which has been changed and when it has.  
   	- Filebeat watches for log files/locations and collects log events

- What does Metricbeat record?
    - Metricbeat takes the metrics and statistics that collects and ships them to the output you specify.
   	- Metricbeat records metric and statistical data from the operating system and from services running on the server.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Server   | 10.0.0.5   | Linux            |
| Web-2    | Server   | 10.0.0.6   | Linux            |
| ELK      |Monitoring| 10.1.0.4   | Linux            |

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.1 10.0.0.2    |
| Web-1    | No                  |                      |
| Web-2    | No                  |                      |
| Elk      | No                  |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?
- Automating configuration with Ansible allows you to deploy to multiple servers using one single playbook.

The playbook implements the following tasks:
- Installs Docker, which intern facilitates instalation of containers
- Installs Python-pip
- Installs Docker python module
- Increases virtual memory
- Downloads and launches a docker ELK container with the ports `5601`, `9200`, `5044`

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
    - Web-1 10.0.0.5
    - Web-2 10.0.0.6

We have installed the following Beats on these machines:
    - filebeat
    - metricbeat

These Beats allow us to collect the following information from each machine:
  	- Filebeat monitors log files or locations you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
   	- Metricbeat collects metrics from the operating system and from services running on the server.

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

- Copy the Elk.yml file to Ansible container folder /etc/ansible/files/
- Update the hosts file /etc/ansible/hosts to include ELK server IP address: 10.1.0.4
- Run the playbook Elk.yml, and navigate to /etc/ansible/http://10.1.4.0.4/:5601 to check that the installation worked as expected.
- The playbook file is Elk.yml and its copied in /etc/ansible
- Updating the host file will make Ansible run the playbook on a specific machine
- By adding a private IP under "servers" you can specify which machine to install and the ELK server on vs filebeat
- The URL to navigate to in order to check ELK server 10.1.0.4.49:5601


The commands needed to run the Ansible configuration for the Elk-Server are:

    - ssh AzAdmin@JumpBox(Public IP)
    - sudo docker container list -a (locate your ansible container)
    - sudo docker start container (name of the container)
    - sudo docker attach container (name of the container)
cd /etc/ansible/
    - ansible-playbook elk.yml (configures Elk-Server and starts the Elk container on the Elk-Server) wait a couple minutes for the implementation of the Elk-Server
    - cd /etc/ansible/roles/
    - ansible-playbook filebeat-playbook.yml (installs Filebeat and Metricbeat)
    - open a new web browser (http://[your.ELK-VM.External.IP]:5601/app/kibana) This will bring up the Kibana Web Portal
    - check the Module status for file beat and metric beat to see their data receiving.

** You will need to ensure all files are properly placed before running the ansible-playbooks.
