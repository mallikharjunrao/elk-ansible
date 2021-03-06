# Ansible Role: elk

An Ansible Role that installs Elasticsearch, Logstash and Kibana 5.0 on Debian/Ubuntu.

**Tested on Ubuntu 16.04**


## Getting started

Make sure that python:2.7 is installed on the host.

Look at `defaults/main.yml` for variables.

This playbook is expected to run under `root`.

**Example of using in playbook**

```
$ ls -l .
hosts
roles/
site.yml
$ ls -l roles
Zhomart.elk/
```

hosts

```
[elk]
138.68.5.100
```

site.yml

```yaml
---
- hosts: all
  remote_user: root

  vars:
    elk_vm_max_map_count:       "262144"

  roles:
    - role: 'Zhomart.elk'
```

And then run ansible playbook

```
$ ansible-playbook site.yml -i hosts
```

Don't forget to allow needed ports on hosts.

```
root@host # ufw allow 5601
```


## Logstash

https://discuss.elastic.co/t/running-multiple-independent-logstash-config-files-with-input-filter-and-output/29757

Logstash currently has a single event pipeline. All configuration files are just concatenated (in order) as if you had written a single flat file. If you don't want all filters to apply to all events you need to have conditionals to select which filters (and outputs) to apply where. For example, you'd typically assign different types to different kinds of messages so you'd wrap your filters like this:

```
if [type] == "sometype" {
  ...
}
```

## TODO

- [x] Elasticsearch 5.0
- [x] Logstash 5.0
- [x] Kibana 5.0
- [x] X-Pack
