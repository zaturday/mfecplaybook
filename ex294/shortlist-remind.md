module list
remide before exam


```
- gpg_rpm
- yum_repository
- file  > optional is setype for using security context
- copy   > optional is setype for using security context and changing src to contect for write some to file
- dnf, yum
- replace
- firewalld  #collection posix firewalld
- lvol
- debug
- services
- setup # list all facts




```

```
get for one server to text
ansible servera -m setup > facts.log

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
      when: ansible_lvm.vgs.research is not defined  # Run this only if the volume group 'research' does NOT exist in ansible_lvm facts

```
ansible_lvm.vgs.research เพื่อจะหาชื่อ research แล้วโชว์ใน msg.\n

