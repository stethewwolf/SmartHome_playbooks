#SMARTHOME playbooks

This repository contain playbook used to configure and maintain my domotics project.

## Requirements
### Local Machine
Follow [ansible intro and installation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

**Fedora:** `sudo dnf install ansible`

### Target Systems
* suppoerted OS: Debian, Raspbian
* target systems require an user with sudo 
* target systems require active ssh server
* user used to connect must login with ssh keys and belong to ssh group

## Playbooks

### Summary

* [common](#/common)
* [nas](#/nas)
* [docker](#/docker)
* [torrentbox](#/torrentbox)

### Roles Description 

#### Common
The "common" role contain some security best practise, like firewall rules, ssh server enforcing etc..

**firewall**
Applayed rules:
```
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

        iptables -I INPUT -p tcp --dport 22 -j ACCEPT
```

**sshd**
This playbook go to disable password access and restrict ssh access only to users that belong to group ssh 

#### NAS
Nas system is build using [OpenMediaVault](https://www.openmediavault.org/), at the end of the process you can manage the nas opening
a browser and visiting the ip of the machine.

default cretdentials:
user : admin
pass : openmediavault


## References
* [ansible docker module](https://docs.ansible.com/ansible/2.6/modules/docker_container_module.html#docker-container-module)
* [installare openmediavault](https://stefano-prina.it/installare-openmediavault-su-debian/) ITA
* [official openmediavault install guide](https://openmediavault.readthedocs.io/en/5.x/installation/on_debian.html)
