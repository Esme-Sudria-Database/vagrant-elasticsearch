# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 9200, host: 9200
  config.vm.network "forwarded_port", guest: 5601, host: 5601

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end

  config.vm.provision "shell", inline: <<-SCRIPT
    mkdir -p /home/vagrant/ansible-local
    cp -rf /vagrant/* /home/vagrant/ansible-local
    chmod -x /home/vagrant/ansible-local/local.ini

    apt-get update
    apt-get install -y python-pip
    apt-get install -y python-dev
    apt-get install -y libffi-dev
    apt-get install -y libssl-dev

    pip install --upgrade setuptools
    pip install cffi
    pip install markupsafe
    pip install ansible

    export PYTHONUNBUFFERED=1
    ansible-playbook -i "/home/vagrant/ansible-local/local.ini" "/home/vagrant/ansible-local/site.yml"
  SCRIPT
end
