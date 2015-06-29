# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/precise64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 80, host: 8080

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
  # Map the app source to vagrant home directory
  config.vm.synced_folder "./app", "/home/vagrant/app"

  config.vm.post_up_message = "\n\n\n\n\n\n\n" + 
                              "This VM has these installed:"+
                              # "\n- apache2" +
                              "\n- git" +
                              "\n- Node.js + npm" + 
                              "\n- Yeoman, Grunt, Bower and JHipster the yo generator" + 
                              "\n- Java 7 with JAVA_HOME and PATH set.\n"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  # Customize the amount of memory on the VM:
    vb.memory = "1024"
    vb.name = "jhipster-box"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  

  config.vm.provision "shell", inline: <<-SHELL
    # make the directory for our app
    sudo mkdir ~/app

    sudo apt-get update -y

    # install basic tools
    sudo apt-get install build-essential rsync telnet screen man wget -y
    sudo apt-get install strace tcpdump -y
    sudo apt-get install libssl-dev zlib1g-dev libcurl3-dev libxslt-dev -y
    sudo apt-get install software-properties-common python-software-properties libcairo2-dev libav-tools nfs-common portmap -y
    sudo apt-get install -y make g++ curl locate

    sudo apt-get install git -y

    curl -sL https://deb.nodesource.com/setup | sudo bash -
    sudo apt-get install -y nodejs

    sudo apt-get update -y
    # sudo apt-get install -y build-essential
    # Upgrade to latest npm
    sudo npm install -g npm@latest

    # Upgrade Nodejs to latest with npm
    sudo npm cache clean -f
    sudo npm install -g n
    sudo n stable
    node -v

    # install yeoman
    sudo npm cache clean -f
    sudo npm install -g yo

    # Install Bower
    sudo npm cache clean -f
    sudo npm install -g bower
    bower -version
    
    #Depending on your preferences, install either Grunt (recommended) with 
    sudo npm cache clean -f
    sudo npm install -g grunt-cli
    sudo npm install grunt
    grunt -version
    # or Gulp.js with 
    # npm install -g gulp.
    # Install JHipster: 
    sudo npm cache clean -f
    sudo npm install -g generator-jhipster

    # make sure java 1.7 installed
  
    sudo wget --no-check-certificate https://github.com/aglover/ubuntu-equip/raw/master/equip_java7_64.sh && bash equip_java7_64.sh
    java -version
    # # set java defaultsJAVA_HOME and PATH
    # sudo apt-get install -y oracle-java7-set-default
    # echo $JAVA_HOME
    # echo $

    sudo updatedb
  SHELL
end
