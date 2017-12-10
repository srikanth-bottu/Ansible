# Ansible
## RHEL/CentOS 7 64-Bit ##
# wget http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
# rpm -ivh epel-release-latest-7.noarch.rpm

How Do I Verify EPEL Repo?
You need to run the following command to verify that the EPEL repository is enabled. Once you ran the command you will see epel repository.

# yum repolist

Step 1: Installing Controlling Machine – Ansible
1. Before installing ‘Ansible‘ on the server, let’s first verify the details of the server like hostname and IP Address. Login into server as a root user and execute the below command to confirm system settings that we’re going to use for this setup.

# sudo ifconfig | grep inet

On RHEL/CentOS/Fedora

Unfortunately, there are no official Ansible repository for RedHat based clones, but we can install Ansible by enabling epel repository under RHEL/CentOS 6, 7 and currently supported fedora distributions.

Fedora users can directly install Ansible through default repository, but if you are using RHEL/CentOS 6, 7, you have to enable EPEL repo.

After configuring epel repository, you can install Ansible using following command.

$ sudo yum install ansible -y
After installed successfully, you can verify the version by executing below command.

# ansible --version

Step 2: Preparing SSH Keys to Remote Hosts
4. To perform any deployment or management from the localhost to remote host first we need to create and copy the ssh keys to the remote host. In every remote host there will be a user account tecmint (in your case may be different user).

First let we create a SSH key using below command and copy the key to remote hosts.

# ssh-keygen -t rsa -b 4096 -C "admin@tecmintlocal.com"

 After creating SSH Key successfully, now copy the created key to all three remote server’s.

# ssh-copy-id tecmint@192.168.0.112
# ssh-copy-id tecmint@192.168.0.113
# ssh-copy-id tecmint@192.168.0.114

After copying all SSH Keys to remote host, now perform a ssh key authentication on all remote hosts to check whether authentication working or not.

$ ssh tecmint@192.168.0.112
$ ssh tecmint@192.168.0.113
$ ssh tecmint@192.168.0.114
