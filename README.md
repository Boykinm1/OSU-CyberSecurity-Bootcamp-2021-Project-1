# OSU-CyberSecurity-Bootcamp-2021-Project-1
Project 1: Elk Stack and Azure
Matthew Boykin

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Network Diagram](https://github.com/Boykinm1/OSU-CyberSecurity-Bootcamp-2021-Project-1/blob/563021ed3269494b0ee618ce077d58e8133438c6/Project%201%20Diagram.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

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

Load balancing ensures that the application will be available for use, in addition to restricting high traffic flow to the network.
- Load balancers help prevents overloading servers and increases the productivity and uptime of those servers. It directs the traffic flow to eliminate single point of failure.
- The jumpbox improves the network security onf the virtual network. It acts as a signle point of entry to the network and limits exposure to the public.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- Filbeat looks for any changes to the log files collecting log events. It then sends these log events to Logstash or Elasticsearch so they can be indexed.
- Metricbeat records the statistical data and sends them to the location specified by Logstash or Elasticsearch.

The configuration details of each machine may be found below.

| Name                 | Function | IP Address                                  | Operating System |
|----------------------|----------|---------------------------------------------|------------------|
| Jumpbox              | Gateway  | 10.0.0.4 (Private)/ 40.121.47.42 (Public)   | Linux            |
| Ubuntu-for-Elk-Stack | Server   | 10.1.0.4 (Private)/ 104.45.211.215 (Public) | Linux            |
| Web-1                | Server   | 10.0.0.5 (Private)                          | Linux            |
| Web-2                | Server   | 10.0.0.6 (Private)                          | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 74.83.126.128

Machines within the network can only be accessed from the Jumpbox.
- Jumpbox was the only machine that was allowed access to the Ubuntu-for-Elk-Stack machine.
- The IP address that was whitelisted was the private address of the jumpbox: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses |
|----------------------|---------------------|----------------------|
| Jumpbox              | Yes                 | 74.83.126.128        |
| Ubuntu-for-Elk-Stack | No                  | 10.0.0.4             |
| Web-1                | No                  | 10.0.0.4             |
| Web-2                | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible allows the user to automate the process of springing up the components of the application environments.

The playbook implements the following tasks:
- Installs Docker
- Installs Python-pip
- Installs Docker Python Module
- Increases Virtual Memory
- Downlaods and launches Dokcer Elk Container with available ports: 5601, 9200, 5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat creates log files from changes or activities on the machines and sends them to Logstash or Elasticsearch to be indexed. This can show us the Azure tools used on the VMs.
- Metricbeat collects the data from the system and applications and sends them to Logstash or Elasticsearch as well. For example, it will grab the statistics from the Linux operating system on the VMs.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

  FILEBEAT

- Copy the filebeat-config.yml file to /etc/ansible.
- Update the filebeat-config.yml file to include the Ubuntu-for-Elk-Stack server private IP address in lines 1106 and 1806 and the hosts file under the server part.
- Run the playbook, and navigate to http://104.45.211.215:5601/app/kibana to check that the installation worked as expected.

METRICBEAT

- Copy the metricbeat-config.yml file to /etc/ansible.
- Update the metricbeat-config.yml file to include the Ubuntu-for-Elk-Stack server private IP address in lines 62 and 96 and the hosts file under the server part.
- Run the playbook, and navigate to http://104.45.211.215:5601/app/kibana to check that the installation worked as expected.
