# Ansible
List the installed yum repositories with the following command:

Copy
[ec2-user ~]$ yum repolist all
The resulting output lists the installed repositories and reports the status of each. Enabled repositories display the number of packages they contain.

repo id                             repo name                                                                status
!amzn-main/latest                   amzn-main-Base                                                           enabled: 5,612
amzn-main-debuginfo/latest          amzn-main-debuginfo                                                      disabled
amzn-main-source/latest             amzn-main-source                                                         disabled
amzn-nosrc/latest                   amzn-nosrc-Base                                                          disabled
amzn-preview/latest                 amzn-preview-Base                                                        disabled
amzn-preview-debuginfo/latest       amzn-preview-debuginfo                                                   disabled
amzn-preview-source/latest          amzn-preview-source                                                      disabled
!amzn-updates/latest                amzn-updates-Base                                                        enabled: 1,152
amzn-updates-debuginfo/latest       amzn-updates-debuginfo                                                   disabled
amzn-updates-source/latest          amzn-updates-source                                                      disabled
epel/x86_64                         Extra Packages for Enterprise Linux 6 - x86_64                           disabled
epel-debuginfo/x86_64               Extra Packages for Enterprise Linux 6 - x86_64 - Debug                   disabled
epel-source/x86_64                  Extra Packages for Enterprise Linux 6 - x86_64 - Source                  disabled
epel-testing/x86_64                 Extra Packages for Enterprise Linux 6 - Testing - x86_64                 disabled
epel-testing-debuginfo/x86_64       Extra Packages for Enterprise Linux 6 - Testing - x86_64 - Debug         disabled
epel-testing-source/x86_64          Extra Packages for Enterprise Linux 6 - Testing - x86_64 - Source        disabled 
To add a yum repository to /etc/yum.repos.d

Find the location of the .repo file. This will vary depending on the repository you are adding. In this example, the .repo file is at https://www.example.com/repository.repo.

Add the repository with the yum-config-manager command.

Copy
[ec2-user ~]$ sudo yum-config-manager --add-repo https://www.example.com/repository.repo
Loaded plugins: priorities, update-motd, upgrade-helper
adding repo from: https://www.example.com/repository.repo
grabbing file https://www.example.com/repository.repo to /etc/yum.repos.d/repository.repo
repository.repo                                      | 4.0 kB     00:00
repo saved to /etc/yum.repos.d/repository.repo
After you install a repository, you must enable it as described in the next procedure.

To enable a yum repository in /etc/yum.repos.d

Use the yum-config-manager command with the --enable repository flag. The following command enables the Extra Packages for Enterprise Linux (EPEL) repository from the Fedora project. By default, this repository is present in /etc/yum.repos.d on Amazon Linux instances, but it is not enabled.

Copy
[ec2-user ~]$ sudo yum-config-manager --enable epel

























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
