#  Red Hat System Administration III: Linux Automation with Ansible

My Class notes about my learning process in Red Hat 294 Course

## 1. Introducing Ansible

Infrastructure as code. Avoiding performing manual tasks is the best practice to ensure that no human mistakes are made through the process of our work. Automation can help with the infrastructure management. The use of a machine-readable automation language to define and describe the state of the infrastructure makes the maintenance and display more reliable and safe. The adition of a version control system is a powerfull advantage. 

> Ansible is an open source automation platform. It is a simple automation language that can perfectly describe an IT application infrastructure in Ansible Playbooks. It is also an automation engine that runs Ansible Playbooks.  

- Ansible is Simple, providing human-readable automation. No special skills are require to write them.

- Ansible is Powerful, can be used to orchestrate the entire application life cycle.  

- Ansible is Agentless, it connects to the hosts it manages using OpenSSH or WinRM to perform tasks. No special agents need to be approved for use.

- Ansible has Cross platform support.

- Easy to manage in version control.

### Ansible concepts

- There are two types of machines: control nodes and managed hosts. Ansible is installed and run from a control node. Managed hosts are listed in an inventory. Inventories can be defined in static files or dynamically determined by scripts that got the information from external sources.

- Ansible is used to create plays to ensure a host or a group of hosts are in a particular state. a play performs a series of tasks on the hosts, in YAML format. This files are called playbooks.

- The playbook only applys changes when the system is in a partivular state, so the runs are very safely.

> Ansible is simple to install. The Ansible software only needs to be installed on the control node (or nodes) from which Ansible will be run. Hosts that are managed by Ansible do not need to have Ansible installed. This installation involves relatively few steps and has minimal requirements.
> The control node should be a Linux or UNIX system. Microsoft Windows is not supported as a control node, although Windows systems can be managed hosts.
> Python 3 (version 3.5 or later) or Python 2 (version 2.7 or later) needs to be installed on the control node.

## 2. Deploying Ansible

An inventory defines a collection of hosts that Ansible will manage. These hosts can also be assigned to groups, which can be managed collectively. Groups can contain child groups, and hosts can be members of multiple groups. The inventory can also set variables that apply to the hosts and groups that it defines. Hosts can be defined statically or dynamically.

### Static Inventory through INI-style format

In its simplest form, an INI-style static inventory file is a list of host names or IP addresses of managed hosts, each on a single line:

```
web1.example.com
web2.example.com
db1.example.com
db2.example.com
192.0.2.42
```

Example of Hosts defined into hosts groups. Hosts can be in multiple groups and it is a good practice to organize them in different ways.

```
[webservers]
web1.example.com
web2.example.com
192.0.2.42
[db-servers]
db1.example.com
db2.example.com
[east-datacenter]
web1.example.com
db1.example.com
[west-datacenter]
web2.example.com
db2.example.com
[production]
web1.example.com
web2.example.com
db1.example.com
db2.example.com
[development]
192.0.2.42
```

Defining nested groups
```
[usa]
washington1.example.com
washington2.example.com
[canada]
ontario01.example.com
ontario02.example.com
[north-america:children]
canada
usa
```

Simplifying Host Specifications with Ranges. Ranges match all values from START to END, inclusively.
```
[START:END]
```

```
[a:c].dns.example.com matches hosts named a.dns.example.com, b.dns.example.com, and c.dns.example.com.
```

#### Verifying the inventory

Ansible has a command to verify a machine's presence in the inventory. You can verify individual hosts or groups.

#### Overriding the Location of the inventory

/etc/ansible/hosts file is considered the default static inventory file. However it is a good practice to not use that file and specify the location in the command.

You can also define variables used in playbooks in the host inventory files.

Ansible inventory information can also be dynamically generated, using information provided by external databases. Like for example contact with AWS to get the information from EC2 servers to construct the ansible inventory. The inventory would get updated by adding new EC2 and removing the old hosts that were deleted.