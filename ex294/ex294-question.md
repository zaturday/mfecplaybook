# Prepare all managed node and control node
### QUESTION #1:
1. Install and configure Ansible on control node as follows:

   * Install the required packages.
   * Create a static inventory file called /home/student/ansible/inventory as follows:
          -- servera is a member of dev host group.
          -- serverb is a member of test host group.
          -- serverc and serverd are the members of the prod host group.
          -- servere is a member of the balancers host group.
          -- The prod group is a member of the webservers group.

   * Create a configuration file called /home/student/ansible/ansible.cfg so that:
          -- The host inventory file should be defined as /home/student/ansible/inventory
          -- The default roles directory is /home/student/ansible/roles
          -- The default content collections directory is /home/student/ansible/collections

   * The topography will be as follows:
```
control:
work.lab.exsample.com 192.168.1.100

manged node:
servera.lab.exsample.com 192.168.1.101
serverb.lab.exsample.com 192.168.1.102
serverc.lab.exsample.com 192.168.1.103
serverd.lab.exsample.com 192.168.1.104
servere.lab.exsample.com 192.168.1.105
```
***On the Control Node***

# Configure the repository on all nodes
### QUESTION #2:
```
Instructions:

2. Create a playbook called "repo.yml" for configuring the repository on all nodes.
BaseOS:
name: BaseOS
baseurl: http://work.lab.example.com/rhel/BaseOS/
description: Base OS Repo
gpgcheck: yes
gpgkey: http://work.lab.example.com/rhel/BaseOS/RPM-GPG-KEY-redhat-release
enabled: yes

AppStream:
name: AppStream
baseurl: http://work.lab.example.com/rhel/AppStream/
description: AppStream Repo
gpgcheck: yes
gpgkey: http://work.lab.example.com/rhel/RPM-GPG-KEY-redhat-release
enabled: yes
```
***On the Control Node***

### QUESTION #3:
```
Instructions:

3. Install Ansible Content Collections:

i) create a directory "collections" under /home/student/ansible/
ii) using the url "https://galaxy.ansible.com/download/ansible-posix-2.0.0.tar.gz" to install ansible.posix collection under the collections directory.
iii) using the url "https://galaxy.ansible.com/download/community-general-11.1.0.tar.gz" to install the community-general collection under the collections directory.
----------------------------------------------------------------------------


NOTE ON THE EXAM:
Example url: http://content.example.com/rhce/ansible-posix....
```
***On the Control Node***

# Install packages
### QUESTION #3-1: CyberCustodians
```
Instructions:
3-1. Create a playbook called /home/student/ansible/packages.yml and perform the following tasks:
- install the php & mariadb on hosts in the dev,test and prod host group
- install the RPM Development Tools package group on host in the dev host group
- Update all packages to the latest version on host in the dev host group
```

***On the Control Node***

# Use a RHEL system role
### QUESTION #3-2: CyberCustodians
```
Instructions:

3-2. Install the rhel-system-roles package & create a playbook called /home/student/ansible/timesync.yml
i) Runs on all managed nodes
ii) Uses the timesync role
iii) configures the role to use the currently active NTP provider
iv) Configure the role to use the time server 172.25.254.254 or classroom.example.com
v) Configure the role to enable the iburst parameter
ntp server 192.168.1.30

```

# Install the Roles
### QUESTION #4:
```
Instructions:

4. Install the roles
i) create directory "roles" under /home/student/roles
ii) create a "requirements.yml" under the roles directory and download the given roles under it using the galaxy command.
iii) 1st role name should be "balancer" and download it using this url "http://work.lab.example.com/ex294/balancer.tgz".
iv)  2nd role name will be "phpinfo" and download it using this url "http://work.lab.example.com/ex294/phpinfo.tgz".

For this example we will use (This part will not be on the exam, but for real exam you will use WGET for the content files):
https://github.com/RedHatRanger/phpinfo.git                        (phpinfo)
https://github.com/RedHatRanger/balancer.git                       (balancer)

* Note: You can find them on galaxy.ansible.com and search for the roles "geerlingguy.haproxy" and "bagaswh.php".
        Then you can open their github pages and copy the https link.
```

# Create Offline Role For Apache
### QUESTION #5:
```
Instructions:

5. Create an offline role named "apache" under the roles directory.
i) install the httpd package and the service should be started and enabled.
ii) host the webpage using the template.j2
iii) the template.j2 should contain:
     Welcome to HOSTNAME ON IPADDRESS
     where hostname is the Fully Qualified Domain Name (FQDN)
iv) create the playbook called "apache_role.yml" and run the role on the webservers group.
```

# Create and Run a Roles.yml Playbook
### QUESTION #6:
```
Instructions:

6. Create a playbook called roles.yml and it should run balancer and phpinfo roles.

   Use roles from Ansible Galaxy
Create a playbook called /home/rhel/ansible-files/roles.yml
* The playbook contains a play that runs on host in the balancers host group and uses the balancers role.
- This role configures a service to load balance web server request between hosts in the webservers host group.
- Browsing to host in the balancers host group (for example http://node5.example.com) produces the following output:
Welcome to node3.example.com on 172.28.128.103
- Reloading the Browser produces output from the alternet web server:
Welcome to node4. lab.example.com on 172.28.128.104

* The Playbook contains a play the runs on hosts in webserver host group and uses the phpinfo role.
- Browsing to host in the webserver host group with the URL /hello.php produces the following out [ut: Hello PHP World from FQDN
- For example Browsing to http://node3.example.com/hello.php produces the following output:
Hello PHP World from node3.example.com
along with various details of the PHP configuration include the version of PHP that is installed.
- Similarly, Browsing to http://node4.lab.example.com/hello.php, produces the following output:
Hello PHP World from node4.example.com
along with various details of the PHP configuration including the version of PHP that is installed
```
# Install Packages in Muliple Groups
### QUESTION #7:
```
Instructions:

7. Install packages in multiple groups
i) Install vsftpd and mariadb-server packages in dev and test group.
ii) Install "RPM Development Tools" group package in prod group.
iii) Update all packages in dev group.
iv) Use separate play for each task and playbook name should be packages.yml.
```
