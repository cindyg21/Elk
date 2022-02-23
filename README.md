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
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files, logs and system metrics.
- _TODO: What does Filebeat watch for?_
- _TODO: What does Metricbeat record?_

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

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
- _TODO: What is the main advantage of automating configuration with Ansible?_

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
- _Web-1 10.0.0.5_
- _Web-2 10.0.0.6_

We have installed the following Beats on these machines:
- _filebeat_
- _metricbeat_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

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


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
