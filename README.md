# vagrant.provision.bionic64
Provisioning vagrant box ubuntu/bionic64

This Vagrant script creates a Ubuntu's 64bit 18.04 LTS (ubuntu/bionic64) machine and provide it via owns machine SHELL with a LAMP environment with the following actions:

- Install lastest Apache
- Adds the NodeJS & Ansible repos
- Installs latest NodeJS 10.x branch
- Installs Ansible
- Installs PHP 7.2 with the following modules: libapache2-mod-php7.2 php7.2-curl php7.2-json php7.2-cli php7.2-common php7.2-mbstring php7.2-gd php7.2-intl php7.2-xml php7.2-mysql php7.2-zip php7.2-bcmath
- Installs latest MySQL indicating the root password on the process (you can change it for your own)
- Installs composer and makes it global
- Installs Git
- Creates and enable a swap of 2Gb

Change the default password for the MySQL root user located in the Vagrantfile
The total amount of RAM for the SO is 2Gb
The local IP for this machine is 192.168.33.177. Change it for your convenience.
The synced_folder is web (relative on the Vagrantfile location) -> /var/www (default DocumentRoot folder for apache)
