## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](https://raw.githubusercontent.com/PercyGC/ELK-Stack-Project-1/Project/Images/Cloud_Network_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Elk Deployment file may be used to install only certain pieces of it, such as Filebeat.

  - /etc/ansible/install-elk.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting traffic to the network.
- What aspect of security do load balancers protect? The Load Balancer helps defends from denial-of-service (DDOs) attack by shifting the server. 
- What is the advantage of a jump box? It reduces the unnecessary exposure of critical servers by forcing one point of entry to network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic activity
- What does Filebeat watch for? Monitors the log files or locations that you specify, collects log events, and send them to Elasticsearch.
- What does Metricbeat record? Is a lightweight shipper that periodically collects metrics from OS and from services running on the server. It takes the metrics and statistics that it collects and forwards them to Elasticsearch.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Ubuntu            |
| WEB-01     | WASRV         | 10.0.0.5           | Ubuntu                 |
| WEB-02     | WASVR         | 10.0.0.6           | Ubuntu                 |
| WEB-03     | WASVR         | 10.0.0.7           | Ubuntu                 |
| ELK-SVR     | ELK         | 10.1.0.4           | Ubuntu                 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _Personal IP Address_

Machines within the network can only be accessed by SSH Port 22.
- Which machine did you allow to access your ELK VM? What was its IP address?10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | NO              | Personal IP    |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible? The main advantage of automating configuration with Ansible is that it enables IT administrators the ability to automate your daily work tasks and give the administrator more time to focus on the needs of the business.

The playbook implements the following tasks:
- The header of the Playbook can specify a different group of machines as well as a different remote user.
- The playbook should install the following services docker.io, python3-pip, and docker.
- Launching and exposing the container run sebp/elk:761 the container should be started with these published ports. 5601:5601 9200:9200 5044:5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](https://github.com/PercyGC/ELK-Stack-Project-1/blob/Project/Images/Docker%20Result.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- `WEB1 10.0.0.5` `WEB2 10.0.0.6` `WEB3 10.0.0.7`

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- `Filebeat` collects data about the file system. It enables analysts to monitor files for suspicious changes.
- `Metricbeat` collects machine metrics, such as uptime and CPU usage. It makes it easy to collect specific information aboout the machines in the network.
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the `filebeat-config.yml` and `metricbeat-config.yml` file to /etc/ansible/roles
- Update the private IP of the Elk-server to the Kibana.
- Run the playbook, and navigate to Elk-Server to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_
- _Which file is the playbook? filebeat-playbook.yml
- _Where do you copy it? /etc/ansible/roles/filebeat-playbook.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? pentest.yml 
- _How do I specify which machine to install the ELK server on versus which to install Filebeat on? install-elk.yml
- _Which URL do you navigate to in order to check that the ELK server is running? `http://[my-private-IP]:5601/app/kibana`

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

- _SSH into jumpBox Vm ssh sysadmin@[Public IP address]
- _Run sudo docker container list -a
- _Run sudo docker start container [Container name]
- _Run sudo docker attach container [Container name]
- _Run ansible-playbook install-elk.yml
- _After the Elk container is installed double check elk-docker container is running by SSH into Elk-SVR VM ssh sysadmin@[private IP address]
- _Run sudo docker ps
- _Since the Elk server runs on specific ports you need to create an incoming rule for the security group that allows TCP traffic over the necessary port from your IP address.
- _Check that you can load the ELK stack server at http://[your-IP]:5601/app/kibana.
- _If everthing works correcty, you should see the home webpage of kibana.
