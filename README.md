# Ansible Playbook for the Ubiquiti Unifi Network Controller Installation

Ansible playbook for installing the Unifi Network Controller.

## Supported Operating Systems

| OS | Supported | Notes
| :-- | :-- | :--
| Debian 11 (bullseye) | ✅ | Recommended
| Ubuntu 22.04 LTS (jammy) | ✅ | Uses old libssl deb package for mongodb, uses focal for Adopjdk repo
| Ubuntu 20.04 LTS (flocal) | ✅ | Uses old libssl deb package for mongodb

## Prerequisites

1. Ansible is installed in your PC ([instructions are here](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible)).
2. One of the supported operating systems above is reachable by ssh.

## Instructions

To run the playbook you will need the IP or hostname of the target server you want to install the Unifi controller on.

1. Open a terminal and run the following. The below command assumes you
````bash
TARGETPC=  # put your IP address, hostname or fqdn here. Can be comma seperated for multiple servers

ansible-playbook unifi_network_controller_setup.yml -i $TARGETPC,
````
2. Append the following based on your how connect to your server
````bash
--user myusername       # To connect with a specific user account
--ask-pass              # If an SSH password is required.
--become                # for sudo escalation
--ask-become-pass       # If you need to enter a password for sudo escalation.
````
example below:
````bash
TARGETPC=192.168.2.4

ansible-playbook unifi_network_controller_setup.yml -i $TARGETPC, --ask-pass --become --ask-become-pass --user larry
````

## Notes
- MongoDB 3.x is the only release that is currently supported by the Unifi Netowrk Controller. However 3.6 was retired in April 2021 and is now end of life. Unfortunetly until Ubiquiti improves their mongodb support, 3.6 must be installed.
