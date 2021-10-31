# Azure-Cloud-Architecture-with-ELK-Deployment
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Azure Cloud architecture with ELK Deployment.drawio.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

  - install_elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
- What aspect of security do load balancers protect? Availability, Web traffic, web security. What is the advantage of jump box? Automation, Security, Network segmentation, Access Control 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system system logs.
- Filebeat collects data about file system
- metricbeat collects machine metrics,such as uptime.
The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web 1    |WebServer | 10.0.0.6   | Linux            |
| Web 2    |Webserver | 10.0.0.7   | Linux            |
| Web 3    |Webserver | 10.0.0.8   | Linux 
|ELK       |ELK Server| 10.1.0.4   | Linux            |
| LB       | LB       |40.83.160.85| Linux


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 104.43.255.268:5601

Machines within the network can only be accessed by Jump box Provisioner.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address? 
web 1 10.0.0.6 web 2 10.0.0.7_

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 10.0.0.4             |
| Web 1    | No                  | 10.0.0.4 via SSH 22  |
| Web 2    | No                  | 10.0.0.4 via SSH 22  |
| ELK      | 
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-  Ansible lets you quickly and easily deploy multiplier apps. you wont need to write custom codes to automate your systems; you list the tasks required to be done by writing a playbook, and ansible will figure out how to get your system to the state you want them to be._

The playbook implements the following tasks:
-   - name: Config elk VM with Docker
    hosts: elk
    remote_user: sysadmin
    become: true
    tasks:
 
 - name: Use more memory
  sysctl:
    name: vm.max_map_count
    value: '262144'
    state: present
    reload: yes

   `docker.io`
   `python3-pip`
   `docker`, which is the Docker Python pip module.

 `5601:5601` 
 `9200:9200`
 `5044:5044`

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- web 1 10.0.0.6
  web 2 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat: log events
  Metricbeat: metrics and system statistics

These Beats allow us to collect the following information from each machine:
- ilebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing
Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the  configuration file to ansible container
- Update the configuration file (filebeat-config.yml)file to include hosts: Ip address of the ELK server ["10.1.0.4"]
- Run the playbook, and navigate to kibana > Logs : Add log data > System logs > 5:Module Status > to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?
Answer : For the ANSIBLE : We will create the my-playbook1.yml as our playbook.
Answer : For FILEBEAT: We will create filbeat-playbook.yml as our playbook. 
Answer: For METRICBEAT: We will create metricbeat-playbook.yml as our playbook.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
#List the IP Addresses of your webservers
#You should have at least 2 IP addresses

[webservers]
10.0.0.4 ansible_python_interpreter=/usr/bin/python3
10.0.0.5 ansible_python_interpreter=/usr/bin/python3
10.0.0.6 ansible_python_interpreter=/usr/bin/python3

#List the IP address of your ELK server
#There should only be one IP address
[elk]
10.1.0.4 ansible_python_interpreter=/usr/bin/python3

- _Which URL do you navigate to in order to check that the ELK server is running?
Test Kibana on web : http://[your.ELK-VM.External.IP]:5601/app/kibana
Test Kibana on localhost: sysadmin@10.1.0.4: curl localhost:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
How to Create the ELK Installation and VM Configuration in the /etc/ansible/ directory:

See the final solution of the Ansible ELK Installation and VM Configuration

Specify a different group of machines as well as a different remote user
      - name: Config elk VM with Docker
        hosts: elk
        remote_user: sysadmin
        become: true
        tasks:
Where: [elk] is the Virtual Machine hosts or the group of machine targetted for this installation and can only be done by a `sysadmin` remote_user

How to Copy the raw Filebeat Module Configuration file from web to the /etc/ansible/files directory:

`curl -L -O https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml'
Note : The filebeat-config.yml as our filebeat configuration file.

hosts: ["10.1.0.4:9200"]
  username: "elastic"
  password: "changeme" 

setup.kibana:
  host: "10.1.0.4:5601"
Where: hosts: ["10.1.0.4:9200"] is the ELK VM that can install Filebeat

How to Copy the raw Metricbeat Module Configuration from web to the /etc/ansible/files/ directory:

`curl -L -O https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat > /etc/ansible/files/metricbeat-config.yml'
Note : the metricbeat-config.yml as our metricbeat configuration file. ```

hosts: ["10.1.0.4:9200"]
  username: "elastic"
  password: "changeme" 

setup.kibana:
  host: "10.1.0.4:5601"
Where: hosts: ["10.1.0.4:9200"] is the ELK VM that can install Metricbeat


