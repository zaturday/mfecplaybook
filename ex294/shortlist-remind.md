module list
remide before exam


```
- gpg_rpm
- yum_repository
- file  > optional is setype for using security context
- copy   > optional is setype for using security context and changing src to contect for write some to file
- dnf, yum
- firewalld  #collection posix firewalld

services


```

```
{{ ansible_facts.XXXXXX.XXXX }}
fqdn
hostname
default_ipv4.address
```


```
## get vars form another

{% for host in groups['all'] %}
{{ hostvars[host].ansible_default_ipv4.address }} {{ hostvars[host].ansible_fqdn }} {{ hostvars[host].ansible_hostname }}
{%endfor%}

```
