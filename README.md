# Vagrant Ansible Wordpress
A virtual machine running Wordpress. Vagrant and Ansible are used to provision the virtual machine.

### Requirements
1. VirtualBox
2. Vagrant

### Running
From a command line, run the following
```
# clone the repository
git clone git@github.com:jamienicholls/vagrant-ansible-wordpress.git

# change into the repository directory
cd vagrant-ansible-wordpress

# Provision the virtual machine
vagrant up

```

Once the machines are up and running, you will be able to access the Wordpress from the browser using the webapp1 servers ip (http://192.168.50.30).

### Troubleshooting
The provisioning sometimes errors on adding the REMI reop, re-running the provisioner which should run through successfully
```
vagrant reload --provision webapp1
```
Once it provisions successfully, you will need to run the provisioning of the db box seperatly as the initial vagrant up had errors
```
vagrant up db1
```
