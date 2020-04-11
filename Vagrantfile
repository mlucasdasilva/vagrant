# -*- mode: ruby -*-
# vi: set ft=ruby :


$configurando_vm = <<-SCRIPT
sudo yum install epel-release -y
sudo yum install htop git vim -y
sudo curl -fsSL https://get.docker.com | bash
sudo usermod -aG docker vagrant
sudo systemctl enable docker
sudo systemctl start docker
sudo service firewalld stop
sudo systemctl disable firewalld
SCRIPT

$nginx = <<-SCRIPT
sudo yum install epel-release -y
sudo yum install htop git vim nginx keepalived -y
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl start keepalived
sudo systemctl enable keepalived
sudo service firewalld stop
sudo systemctl disable firewalld
SCRIPT


# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

Vagrant.configure("2") do |config|
 
# config.vm.synced_folder ".", "/vagrant", automount: true , type: "smb"

 config.vm.define "sd_docker01", primary: true do |sd_docker01|
  # Conf básica na VM
  sd_docker01.vm.provider "virtualbox" do |v|
   v.name = "sd_docker01"
   v.memory = 1024
   v.cpus = 1
   v.gui = true
  end
  sd_docker01.vm.box = "centos/7"
  sd_docker01.vm.hostname = "docker01"
  sd_docker01.vm.network "private_network", ip: "192.168.56.61"
  sd_docker01.vm.network "private_network", ip: "192.168.50.61", virtualbox__intnet: "dcnet1"
  # Preparando a máquina para rodar o cluster swarm e instalando utilitários
  sd_docker01.vm.provision "shell", inline: $configurando_vm
  config.trigger.after :provision do |trigger|
    trigger.name = "join token"
    trigger.run = {inline: "vagrant ssh --no-tty -c 'sudo docker swarm join-token manager ^| grep token' sd_docker01 > join-mgr.sh"}
  end
  sd_docker01.vm.provision "shell", inline: "docker swarm init --advertise-addr 192.168.50.61"
  sd_docker01.vm.provision "shell", inline: "sudo docker swarm join-token manager | grep token > /home/vagrant/docker-join-mgr.sh"
 end

 config.vm.define "sd_docker02" do |sd_docker02|
  # Conf básica na VM
  sd_docker02.vm.provider "virtualbox" do |v|
   v.name = "sd_docker02"
   v.memory = 1024
   v.cpus = 1
  end
  # Conf básica no S.O
  sd_docker02.vm.box = "centos/7"
  sd_docker02.vm.hostname = "docker02"
  sd_docker02.vm.network "private_network", ip: "192.168.56.62"
  sd_docker02.vm.network "private_network", ip: "192.168.50.62", virtualbox__intnet: "dcnet1"
  # Preparando a máquina para rodar o cluster swarm e instalando utilitários
  sd_docker02.vm.provision "shell", inline: $configurando_vm
 end
 
 config.vm.define "sd_docker03" do |sd_docker03|
  # Conf básica na VM
  sd_docker03.vm.provider "virtualbox" do |v|
   v.name = "sd_docker03"
   v.memory = 1024
   v.cpus = 1
  end
  # Conf básica no S.O
  sd_docker03.vm.box = "centos/7"
  sd_docker03.vm.hostname = "docker03"
  sd_docker03.vm.network "private_network", ip: "192.168.56.63"
  sd_docker03.vm.network "private_network", ip: "192.168.50.63", virtualbox__intnet: "dcnet1"
  # Preparando a máquina para rodar o cluster swarm e instalando utilitários
  sd_docker03.vm.provision "shell", inline: $configurando_vm
 end

 config.vm.define "sd_docker04" do |sd_docker04|
  # Conf básica na VM
  sd_docker04.vm.provider "virtualbox" do |v|
   v.name = "sd_docker04"
   v.memory = 1024
   v.cpus = 1
  end
  # Conf básica no S.O
  sd_docker04.vm.box = "centos/7"
  sd_docker04.vm.hostname = "docker04"
  sd_docker04.vm.network "private_network", ip: "192.168.56.64"
  sd_docker04.vm.network "private_network", ip: "192.168.50.64", virtualbox__intnet: "dcnet1"
  # Preparando a máquina para rodar o cluster swarm e instalando utilitários
  sd_docker04.vm.provision "shell", inline: $configurando_vm
 end

 config.vm.define "sd_nginx01" do |sd_nginx01|
  # Conf básica na VM
  sd_nginx01.vm.provider "virtualbox" do |v|
   v.name = "sd_nginx01"
   v.memory = 512
   v.cpus = 1
  end
  # Conf básica no S.O
  sd_nginx01.vm.box = "centos/7"
  sd_nginx01.vm.hostname = "nginx01"
  sd_nginx01.vm.network "private_network", ip: "192.168.56.71"
  sd_nginx01.vm.network "private_network", ip: "192.168.50.71", virtualbox__intnet: "dcnet1"
  # Preparando a máquina para rodar o cluster swarm e instalando utilitários
  sd_nginx01.vm.provision "shell", inline: $nginx
 end

 config.vm.define "sd_nginx02" do |sd_nginx02|
  # Conf básica na VM
  sd_nginx02.vm.provider "virtualbox" do |v|
   v.name = "sd_nginx02"
   v.memory = 512
   v.cpus = 1
  end
  # Conf básica no S.O
  sd_nginx02.vm.box = "centos/7"
  sd_nginx02.vm.hostname = "nginx02"
  sd_nginx02.vm.network "private_network", ip: "192.168.56.72"
  sd_nginx02.vm.network "private_network", ip: "192.168.50.72", virtualbox__intnet: "dcnet1"
  # Preparando a máquina para rodar o cluster swarm e instalando utilitários
  sd_nginx02.vm.provision "shell", inline: $nginx
 end


  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
##  config.vm.box = "base"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
 
end
