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

## Create webcontent playbook
### QUESTION #8:
```
Instructions:

8. Create a playbook called webcontent.yml and it should run on webservers group.
   i) create a directory /webdev and it should be owned by wheel group.
  ii) Assign permissions for user=rwx, group=rwx, others=rx and group special permission should be applied to /webdev.
 iii) /webdev directory should have the same selinux context type as "httpd" (httpd_sys_content_t)
  iv) Create a soft link /webdev to /var/www/html/webdev.
   v) Create index.html file under /webdev and file should have content "Development".
  vi) Allow traffic through the firewall for http.

```
# Create a hwreport
### QUESTION #9:
```
Instructions:

9. Collect a hardware report using a playbook on all nodes.
  i)   Download "hwreport.txt" from the url "http://content.example.com/hwreport.txt" and save it under /root.
  ii)  If there is no information it should show "NONE"
  iii) The name of the laybook should be "hwreport.yml"


                                    *** NOTE ***:
For this example we will download the file from:
https://raw.githubusercontent.com/RedHatRanger/RHCE9Vagrant/main/rhce-practice-questions/golden_files/hwreport.txt

/root/hwreport.txt should have content with node information as key=value
#hwreport
HOSTNAME=
MEMORY=
BIOS=
DISK_SIZE_SDA=
DISK_SIZE_SDB=
```
## Create an issue playbook
### QUESTION #10:
```
Instructions:

10. Replace file /etc/issue on all managed nodes

i)   In dev group /etc/issue should have content "Development"
ii)  In test group /etc/issue should have content "Test"
iii) In prod group /etc/issue should have content "Production"
iv)  Playbook name should be issue.yml and run on all managed nodes
```
## Create a hosts playbook
### QUESTION #11:
```
Instructions:

11. Download file "http://content.example.com/Rhce/myhosts.j2"

  1) myhosts.j2 is having the content:
       127.0.0.1 localhost localhost.localdomain localhost4 localhost4.localdomain4
       ::1 localhost localhost.localdomain localhost6 localhost.localdomain6

  ii) The file should collect all node information like ipaddress,fqdn,hostname
       and it should be same as /etc/hosts file,
       if playbook is run on all the managed nodes it must store in /etc/myhosts.

Finally /etc/myhosts should like as below:
127.0.0.1 localhost localhost.localdomain localhost4 localhost4.localdomain4
::1 localhost localhost.localdomain localhost6 localhost.localdomain6

172.28.128.100   control.example.com   control
172.28.128.101   node1.example.com     node1
172.28.128.102   node2.example.com     node2
172.28.128.103   node3.example.com     node3
172.28.128.104   node4.example.com     node4
172.28.128.105   node5.example.com     node5

iii) The playbook name should be "hosts.yml" and run it on dev group.
```
## Create a vault file
### QUESTION #12:
```
Instructions:

﻿12. Create an encrypted variable file locker.yml and that file should contain variable and its value.

  pw_developer is value Iamdev
  pw_manager is value Iammgr

  i) locker.yml file should be encrypted using password "whenyouwishuponastar"
  ii) store password in a file named secret.txt, which is used to encrypt the variable file.
```
## Create a users playbook
### QUESTION #13:
```
Instructions:

﻿13. Download the variable file
"http://content.example.com/Rhce/user_list.yml" and write a playbook named "users.yml" and then run the playbook
on all the nodes using two variable files user_list.yml and locker.yml.

####################### NOTE: For this lab we will use the link below: ################################################
wget https://raw.githubusercontent.com/RedHatRanger/RHCE9Vagrant/main/rhce-practice-questions/golden_files/user_list.yml

i)  * Create a group opsdev
    * Create user from users varaible who job is equal to developer and need to be in opsdev group
    * Assign a password using SHA512 format and run playbook on dev and test group.
    * User password is {{ pw_developer }}

ii) * Create a group opsmgr
    * Create user from users varaible who job is equal to manager and need to be in opsmgr group
    * Assign a password using SHA512 format and run playbook on prod group.
    * User password is {{ pw_manager }}

iii) Use when condition for each play
```
## Rekey the encrypted salaries playbook
### QUESTION #14:
```
Instructions:

14. Rekey variable file from "http://content.example.com/Rhce/salaries.yml"

i) Old password: cisco
ii) New password: redhat
```
## Create a crontab playbook
### QUESTION #15:
```
Instructions:

15. Create a cronjob for the user rhel on all nodes, playbook name is crontab.yml and the job details are below:

  i) Every 2 minutes the job will execute logger "EX294 in progress".
```
