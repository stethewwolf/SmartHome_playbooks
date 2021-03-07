#SMARTHOME playbooks

This repository contain playbook used to configure and maintain my domotics project.

## Requirements
### Local Machine
Follow [ansible intro and installation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

**Fedora:** `sudo dnf install ansible`

### Target Systems
* suppoerted OS: Debian
* target systems require an user with no pass sodo ( add `user_name ALL=(ALL) NOPASSWD:ALL` to sudoers file )\
* target systems require active ssh server

## Playbooks

### Summary

* nas

### Recipes Description 

#### NAS


## References
* [ansible docker module](https://docs.ansible.com/ansible/2.6/modules/docker_container_module.html#docker-container-module)
* [installare openmediavault](https://stefano-prina.it/installare-openmediavault-su-debian/) ITA
* [official openmediavault install guide](https://openmediavault.readthedocs.io/en/5.x/installation/on_debian.html)
