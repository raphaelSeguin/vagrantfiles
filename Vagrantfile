# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "centos/7"

  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "forwarded_port", guest: 8081, host: 8081
  config.vm.network "forwarded_port", guest: 8082, host: 8082
  config.vm.network "forwarded_port", guest: 8083, host: 8083
  config.vm.network "forwarded_port", guest: 22, host: 8022

  # config.vm.synced_folder "./data", "/vagrant_data", create: true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = "2"
  end

  config.vm.provision "shell", inline: <<-SHELL
    yum update -y
    # EPEL repo
    yum install -y epel-repo
    yum update -y

    # ansible
    yum install -y ansible
    # git
    yum install -y git 
    # tree
    yum install -y tree
    # midnight commander
    yum install -y mc
    # unzip
    yum makecache
    yum install -y unzip

    # docker
    yum install -y yum-utils device-mapper-persistent-data lvm2
    yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    yum install -y docker-ce docker-ce-cli containerd.io
    systemctl start docker
    systemctl enable docker

    # terraform
    curl -s -LO https://releases.hashicorp.com/terraform/0.12.21/terraform_0.12.21_linux_amd64.zip
    unzip terraform_0.12.21_linux_amd64.zip
    mv terraform /usr/local/bin/
    rm terraform_0.12.21_linux_amd64.zip

    # az cli
    rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sh -c 'echo -e "[azure-cli]
name=Azure CLI
baseurl=https://packages.microsoft.com/yumrepos/azure-cli
enabled=1
gpgcheck=1
gpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/azure-cli.repo'
    yum install -y azure-cli

    ##### kubernetes


  SHELL
end
