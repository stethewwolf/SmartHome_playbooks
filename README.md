#SMARTHOME playbooks

This repository contain playbook used to configure and maintain my domotics project.

## Requirements
### Local Machine
Follow [ansible intro and installation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

**Fedora:** `sudo dnf install ansible`

### Target Systems
* suppoerted OS: Debian, Raspbian
* target systems require an user with sudo (with no password: user ALL=(ALL) NOPASSWD:ALL)
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

NB : see [iptables_module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/iptables_module.html)

**sshd**
This playbook go to disable password access and restrict ssh access only to users that belong to group ssh 

#### NAS
Nas system is build using [OpenMediaVault](https://www.openmediavault.org/), at the end of the process you can manage the nas opening
a browser and visiting the ip of the machine.

default cretdentials:
user : admin
pass : openmediavault

#### Docker

This role install docker ( pkg docker.io availables from the debian repository ) end install portainer container running on port 9000.

After the role is installed you can visit the system at http://<ip>:9000 to setup portainer.

For reference :

* [Docker Home Page](https://www.docker.com/)
* [Portainer](https://www.portainer.io/)

#### 389ds
This role require Docker installed (by default will install it), 
Create an instance of 389-direcotry service

* [389ds dockerhub](https://hub.docker.com/r/389ds/dirsrv)
* [fedora doc](https://directory.fedoraproject.org/docs/389ds/design/docker.html)

**NOT TESTED**

#### OpenLdap

Data stored in volumes:
        ldap_data
        ldap_conf

Default conf variables:
```
ldap_organization: "my company"
ldap_domain: "my-company.com"
ldap_admin_password: "My-C0mp4nY"
```

to override them by command line:
```
 ansible-playbook -i hosts.yml ldapservers.yml --extra-vars " ldap_organization='my company' ldap_domain='my-company.com' ldap_admin_password='My-C0mp4nY'"
```

to login into the web ui use the user:
```
cn=admin,dc=my-company;dc=com
```

Once both containers are up adn running 

* [docker-openldap](https://github.com/osixia/docker-openldap)
* [docker-phpLDAPadmin](https://github.com/osixia/docker-phpLDAPadmin)

#### NextCloud

This role is built using nextcloud docker image, by default use sqlite db

Default variables:
```
nextcloud_root: "nextcloud_root"
nextcloud_apps: "nextcloud_apps"
nextcloud_config: "nextcloud_config"
nextcloud_data: "nextcloud_data"
smpt_host: ""
smpt_mail_from: ""
nextcloud_admin_user: "nxtcadmin"
nextcloud_admin_password: "nxtcpassword"
```

* [dockerhub nextcloud](https://hub.docker.com/_/nextcloud/)
* [nextcloud](https://nextcloud.com/)

### Kodi
This role is meant to be used with a raspberry.
here some interesting links:
* [enable graphical target](https://raspberrypi.stackexchange.com/questions/72218/raspbian-stretch-lite-lightdm-doesnt-run)
* [fix vchi init](https://chewett.co.uk/blog/258/vchi-initialization-failed-raspberry-pi-fixed/)
* [raspberri+kodi+netflix](https://www.maketecheasier.com/run-kodi-netflix-raspberry-pi/)
* [kodi install on raspbian](https://kodi.wiki/view/HOW-TO:Install_Kodi_on_Raspberry_Pi)
* [kodi enable web interface](https://kodi.wiki/view/Web_interface)


## General References
* [ansible docker module](https://docs.ansible.com/ansible/2.6/modules/docker_container_module.html#docker-container-module)
* [installare openmediavault](https://stefano-prina.it/installare-openmediavault-su-debian/) ITA
* [official openmediavault install guide](https://openmediavault.readthedocs.io/en/5.x/installation/on_debian.html)
* [playbooks best practices](https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html#playbook-tips)
* [playbooks sample directory layout](https://docs.ansible.com/ansible/latest/user_guide/sample_setup.html#sample-directory-layout)
* [ansible variables](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html)
