### Chapter 1 Quiz: Automating Linux Administration with Ansible
1. a
2. d
3. c
4. d

#### Solutions

1. a
2. d
3. c
4. d

### Guided Exercise: Installing Ansible

```
docker run -ti centos:centos8
yum update
yum install epel-release
yum install ansible
ansible --version
ansible -m setup localhost | grep ansible_python_version
```

Find out more about EPEL Repository [here](https://www.liquidweb.com/kb/enable-epel-repository/)