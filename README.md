# Ansible Go Continuous Delivery Role

## Description

*ansible-gocd* is an [Ansible](http://ansible.com) role.
Use this role to install Go Continuous Delivery Server.

## Provides

1. Latest Go Continuous Delivery server

## Requires

1. Ansible 1.7 o higher
2. Ubuntu Server 14.04
3. Vagrant (optional)

## Usage

### Get the code

```bash
$ git clone git@github.com:codingbunch/ansible-gocd.git
```

The code should reside in the roles directory of ansible ( See [ansible documentation](http://docs.ansible.com/playbooks.html#roles) for more information on roles ), in a folder named gocd.

### Create a host file

Following example make ansible aware of the Vagrant box reachable on localhost port 2222.

```bash
$ vi ansible.host
```

with

```ini
[gocd-server]
127.0.0.1 ansible_ssh_port=2222
```

### Create host specific variables

Make the host_vars directory where *ansible.host* file is located.

```bash
$ mkdir host_vars
```

Create a file in the newly created directory matching your host.

```bash
$ cd host_vars
$ vi 127.0.0.1
```

with

```yaml
---

timezone: Europe/Madrid

# NTP servers
ntp_server1: ntp0.ox.ac.uk
ntp_server2: ntp1.ox.ac.uk
ntp_server3: ntp2.ox.ac.uk
ntp_server4: ntp3.ox.ac.uk
ntp_server5: 0.uk.pool.ntp.org
ntp_server6: 1.uk.pool.ntp.org
ntp_server7: ntp.ubuntu.com # fallback

# GOCD
gocd_version: 14.3.0-1186

```

### Run the playbook

First create a playbook including the gocd role, naming it gocd.yml

```yml
- name: gocd
  hosts: gocd-server
  roles:
    - gocd
```

Use *ansible.host* as inventory. Run the playbook only for the remote host *gocd-server*. Use *vagrant* as the SSH user to connect to the remote host. *-k* enables the SSH password prompt.

```bash
$ ansible-playbook -k -i ansible.host gocd.yml -u vagrant
```
