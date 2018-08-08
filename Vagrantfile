# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--memory", 2048]
  end

  config.vm.network "private_network", ip: "192.168.33.177"

  config.vm.synced_folder "web", "/var/www"

  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    echo "Updating source list" | tee /home/ubuntu/vm_build.log
    apt-get update >> /home/ubuntu/vm_build.log
    echo "Installing apache2" | tee /home/ubuntu/vm_build.log
    apt-get install -y apache2 >> /home/ubuntu/vm_build.log
    echo "Installing nodejs repo" | tee /home/ubuntu/vm_build.log
    curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash - >> /home/ubuntu/vm_build.log
    echo "Installing ansible repo" | tee /home/ubuntu/vm_build.log
    sudo apt-add-repository -y ppa:ansible/ansible
    echo "Updating source list" | tee /home/ubuntu/vm_build.log
    apt-get update -y >> /home/ubuntu/vm_build.log
    echo "Installing NodeJS 10" | tee /home/ubuntu/vm_build.log
    apt-get install -y nodejs >> /home/ubuntu/vm_build.log
    echo "Installing Ansible" | tee /home/ubuntu/vm_build.log
    apt-get install -y ansible >> /home/ubuntu/vm_build.log
    echo "Installing php7.2" | tee /home/ubuntu/vm_build.log
    apt-get install -y php7.2 libapache2-mod-php7.2 php7.2-curl php7.2-json php7.2-cli php7.2-common php7.2-mbstring php7.2-gd php7.2-intl php7.2-xml php7.2-mysql php7.2-zip php7.2-bcmath >> /home/ubuntu/vm_build.log
    echo "Installing mysql" | tee /home/ubuntu/vm_build.log
    debconf-set-selections <<< 'mysql-server mysql-server/root_password password your_password'
    debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password your_password'
    apt-get install -y mysql-server >> /home/ubuntu/vm_build.log
    echo "Restart apache2" | tee /home/ubuntu/vm_build.log
    service apache2 restart >> /home/ubuntu/vm_build.log
    echo "Installing composer" | tee /home/ubuntu/vm_build.log
    curl --silent https://getcomposer.org/installer | php >> /home/ubuntu/vm_build.log
    mv composer.phar /usr/local/bin/composer >> /home/ubuntu/vm_build.log
    echo "Installing git" | tee /home/ubuntu/vm_build.log
    apt-get install -y git >> /home/ubuntu/vm_build.log
    echo "Create swap file" | tee /home/ubuntu/vm_build.log
    fallocate -l 2G /swapfile
    chmod 600 /swapfile
    mkswap /swapfile
    swapon /swapfile
    echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
    echo "Enable mod_rewrite" | tee /home/ubuntu/vm_build.log
    sudo a2enmod rewrite >> /home/ubuntu/vm_build.log
    echo "Update & upgrade system packages" | tee /home/ubuntu/vm_build.log
    apt-get update && apt-get upgrade -y >> /home/ubuntu/vm_build.log
  SHELL
end

