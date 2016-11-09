#  ansible-glastopf

## Table of Contents

   * [ansible-glastopf](#ansible-glastopf)
      * [Install ansible](#install-ansible)
      * [Update the inventory.ini file with the master and client IP addresses](#update-the-inventoryini-file-with-the-master-and-client-ip-addresses)
      * [Raspberry Pi](#raspberry-pi)
      * [Vagrant lab](#vagrant-lab)

[https://github.com/mushorg/glastopf](https://github.com/mushorg/glastopf)

Glastopf is a Python web application honeypot founded by Lukas Rist.

## Install ansible

Ubuntu
```
sudo apt-get install ansible
```

Alternatively you can install ansible using pip.
```
sudo apt-get intsall python-pip
sudo pip install ansible
```

## Update the inventory.ini file with the master and client IP addresses

ex:
```
[pi]
pi ansible_host=192.168.1.100 ansible_user=pi

[vagrant]
vagrant ansible_host=127.0.0.1 ansible_port=2222 ansible_user=root

[aws]
ec2 ansible_host={{ ec2_public_ip }} ansible_user=ubuntu ansible_python_interpreter=/usr/bin/python2.7
```

## Raspberry Pi

```
ansible-playbook -l pi site.yml 
```

## Vagrant lab

```
vagrant up
ansible-playbook -l vagrant site.yml 
```
