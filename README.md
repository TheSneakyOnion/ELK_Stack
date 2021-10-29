# ELK_Stack
A full elk stack deployed in AWS for demonstration purposes.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](https://raw.githubusercontent.com/TheSneakyOnion/ELK_Stack/main/Diagrams/ELK_Stack.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat_playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

  - [filebeat_playbook.yml](https://github.com/TheSneakyOnion/ELK_Stack/blob/main/Ansible/filebeat_playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. This will help protect the servers from attacks like DDoS by lightening loads on taxed servers. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics. Filebeat watches the logs, while metricbeat handles the metrics.

The configuration details of each machine may be found below.

| Hostname   | IP         | Function     | OS               |
|------------|------------|--------------|------------------|
| Jumpbox    | 10.0.0.204 | Gateway      | Amazon Linux 2   |
| ELK_Server | 10.0.0.21  | Log database | Ubuntu 20.04 LTS |
| Webserver1 | 10.0.0.146 | Webserver    | Ubuntu 20.04 LTS |
| Webserver2 | 10.0.1.64  | Webserver    | Ubuntu 20.04 LTS |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. We configure this machine to accept connections to anywhere to allow mobility among developers, at the risk of security.

Machines within the network can only be accessed by the Jumpbox at 10.0.0.204.

A summary of the access policies in place can be found in the table below.

| Name       | Accesibility | Whitelisted |
|------------|--------------|-------------|
| Jumpbox    | SSH          | *           |
| ELK_Server | Private      | 10.0.0.204  |
| Webservers | Private      | 10.0.0.204  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it ensures we can repeatably deploy servers and maintain identicality between them, as well as speedup common workflows.

The playbook implements the following tasks:
 - installs Python & pip
 - pip installs the Docker
 - Downloads & installs sebp/elk:761 and launches, exposes necessary ports
 - enables docker on boot
 - increases system memory

The following printout shows the result of running `docker ps` after successfully configuring the ELK instance.

> [ec2-user@3.232.134.89]$ docker ps
> CONAINTER ID  IMAGE                   COMMAND                     CREATED     STATUS          PORTS   NAMES
> 08ad78b9b344  cyberxsecurity/ansible  "/bin/sh -c /bin/bas..."    2 days ago  Up 12 minutes           elk

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Webserver1 @ 10.0.0.146
- Webserver2 @ 10.0.1.64

We have installed the following Filebeat and Metricbeat on the above machines.

These Beats allow us to collect the following information from each machine:
- Filebeat tails our logs and forwards the information to ELK_Server to be stored in Logstash on sebp/elk container.
- Metricbeat collects system metrics such as CPU and memory usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the config files to etc/ansible.
- Update the ansible hosts file to include the private IP of the server you'd like your ELK stack on.
- Run the playbook, and navigate to your \[ELK server's public IP]:5601 to check that the installation worked as expected.

### Additional Questions
- _Which file is the playbook? Where do you copy it?_
    - The playbook is [install_elk.yaml](/install_elk.yaml)
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?


