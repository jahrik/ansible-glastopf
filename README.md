#  ansible-glastopf

Glastopf is a Python web application honeypot founded by Lukas Rist.

[https://github.com/mushorg/glastopf](https://github.com/mushorg/glastopf)

## Table of Contents

   * [ansible-glastopf](#ansible-glastopf)
      * [Install ansible](#install-ansible)
      * [Update the inventory.ini](#update-the-inventoryini)
      * [Raspberry Pi](#raspberry-pi)
      * [Vagrant lab](#vagrant-lab)
      * [EC2 instance](#ec2-instance)

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

## Update the inventory.ini

ex:
```
[pi]
pi ansible_host=192.168.1.100 ansible_user=pi

[vagrant]
vagrant ansible_host=127.0.0.1 ansible_port=2222 ansible_user=root
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

## EC2 instance

```
ssh-keygen ~/.ssh/glastopf_rsa
ssh-add ~/.ssh/glastopf_rsa

export AWS_ACCESS_KEY_ID=XXXXXXXXXXXXXXXXXX
export AWS_SECRET_ACCESS_KEY=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

ansible-playbook -i ec2.py setup_ec2.yml
asnible-playbook -i ec2.py site.yml -u ubuntu
```
