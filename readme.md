The fastest way to get a shadowsocks-libev server up and running on a Ubuntu 16.04 VM. Just provide an IP address and port. The script will generate a secure password on the remote machine and send you back a QR code you can scan with shadowrocket or other shadowsocks apps to connect instantly.

# Prerequisites

A virtual machine running Ubuntu 16.04. Other versions may work, but I can only confirm this version works. Set up your machine so that the TCP/UDP ports you want to use are open both on the machine and on the virtual network's firewall. If you know what this means then you don't need instructions. If not then just sign up for Vultr. I can confirm that VULTR VPSes work without any configuration needed on your part. Just make sure the ID_RSA ssh key on your host machine is set up on the VPS and your login name is root(vultr lets you add RSA keys on deploy and the default user is root). The cheapest \$3.50 instance is all you need for a personal vpn/proxy. [You can sign up for vultr here(affiliate)](https://www.vultr.com/?ref=7200330)

# Dependencies

virtualenv(installed from python pip) on your host machine. If you already have pip you can skip straight to preparation. We're running ansible in a virtual environment.

## Ubuntu virtualenv setup

Credit for the ansible installation instructions goes to [serverforhackers.com](https://serversforhackers.com/c/an-ansible2-tutorial)

```
# Install python2.7 (Ubuntu 16.04 comes with python 3 out of the box) and Pip
sudo apt-get install -y python2.7 python-pip

## Use Pip to install virtualenv
### -U updates it if the package is already installed
sudo pip install -U virtualenv
```

## MacOS virtualenv

If you don't already have python/pip installed [follow these instructions](https://www.andreagrandi.it/2018/12/19/installing-python-and-virtualenv-on-osx/)

# Preparation

```
cd this directory
# Create a python virtual environment
virtualenv .venv
# Enable the virtual environment
source .venv/bin/activate

# Then anything we intall with pip will be
# inside that virtual environment
pip install ansible
```

# Usage

```
ansible-playbook ss.yml -u root

```

`-u root` is not necessary if you're logged in as root from the host machine. Otherwise, Ansible will try to connect to your remote machine from whatever your login name is(e.g johnDoe123-macbookpro@123.456.789). You will get a script play by play and when its done a QR code will show up in this directory.

# About

This was inspired by the streisand script model of setting up your VPN for you and sending you set up instructions. The difference is this script installs ONLY shadowsocks and doesn't set up a gateway website. This is for people who only want shadowsocks without the additional security measures, like hobbyists who still want to use their VPS resources for other things.
