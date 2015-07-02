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
  # ubuntu/precise64 hashicorp atlas cloud image (ubuntu/trusty64 (14.04 LTS))
  config.vm.box = "ubuntu/trusty64"

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


  # setup the hostname for the box
  config.vm.hostname = "jhipster-box-hostname"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # Map the app source to vagrant home directory
  # config.vm.synced_folder "app/", "/home/vagrant/app/", owner: "vagrant", group: "vagrant"

  # config.vm.synced_folder "app", "/home/vagrant/app/", type: "rsync",
  #   rsync__exclude: ".git/"


  # disable vagrant share
  # config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.post_up_message = "\n\n\n\n===========================================================" + 
                              "\n\nThis VM has these tools installed:"+
                              # "\n- apache2" +
                              "\n- git" +
                              "\n- Node.js + npm" + 
                              "\n- Yeoman, Grunt, Bower and JHipster the yo generator" + 
                              "\n- Java 7 with JAVA_HOME and PATH set." +
                              "\n\n==========================================================="
  
  # VirtualBox name is default lets change it to something more than that
  config.vm.define "jhipstermachine" do |jhipstermachine|
  end

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  # Display the VirtualBox GUI when booting the machine
  # Uncommment this to see if theres are problems with VirtualBox
    # vb.gui = true
  #
  # tell npm which system we are running
    vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/home/vagrant/app", "1"]
  # Customize the amount of memory on the VM:
    vb.memory = "1024"
    vb.cpus = 2
    vb.name = "jhipster-box-2"
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
    # make the directory for our app files if it does not exist
    if [ ! -d /home/vagrant/app ]; then
        sudo mkdir /home/vagrant/app
    fi

    # npm no binary links for vagrant
    # echo "alias npm='npm --no-bin-links'" >> /home/vagrant/.bashrc
    # set the node path
    # echo "export NODE_PATH=/usr/local/lib/node_modules:$NODE_PATH" >> ~/.bashrc && source ~/.bashrc

    sudo apt-get update -y

    # install basic tools
    sudo apt-get install build-essential rsync telnet screen man wget -y
    sudo apt-get install strace tcpdump -y
    sudo apt-get install libssl-dev zlib1g-dev libcurl3-dev libxslt-dev -y
    sudo apt-get install software-properties-common python-software-properties libcairo2-dev libav-tools nfs-common portmap -y
    sudo apt-get install -y make g++ curl locate git

    # sudo apt-get install git -y

    # curl -sL https://deb.nodesource.com/setup | sudo bash -
    curl --silent --location https://deb.nodesource.com/setup_0.12 | sudo bash -
    sudo apt-get install -y nodejs

    sudo apt-get update -y
    # sudo apt-get install -y build-essential
    # Upgrade to latest npm
    # npm install -g npm@latest
    # echo NPM version
    # npm --version

    # Upgrade Nodejs to latest with npm
    # npm cache clean -f
    # npm install -g n
    # sudo n stable
    # export NODE_PATH=/usr/local/lib/node_modules:$NODE_PATH
    # associate nodejs symbolic link with node binary, otherwise yo would use nodejs from the /usr/bin folder
    # sudo ln -s /usr/local/bin/node /usr/local/bin/nodejs
    echo NodeJS version
    nodejs -v
    echo Node version
    node -v
    echo NPM version
    npm -version

    # install yeoman
    # npm cache clean -f
    npm install -g yo

    # Install Bower
    # npm cache clean -f
    npm install -g bower
    echo Bower version
    bower -version
    
    #Depending on your preferences, install either Grunt (recommended) with 
    # npm cache clean -f
    npm install -g grunt
    npm install -g grunt-cli
    echo Grunt version
    grunt -version
    # or Gulp.js with 
    # npm install -g gulp.
    # Install JHipster:
    # npm cache clean -f
    npm install -g generator-jhipster

    # the install files for grunt do not have right permissions
    # lets fix them
    # sudo chown -R vagrant:vagrant /usr/lib/node_modules
    # sudo chown -R vagrant:vagrant /home/vagrant/.npm

    # make sure java 1.7 installed
###########    sudo wget --no-check-certificate https://github.com/dkoudlo/ubuntu-equip/raw/master/equip_java7_64.sh && bash equip_java7_64.sh
    # set java defaultsJAVA_HOME and PATH
    # sudo apt-get install -y oracle-java7-set-default

    # sudo updatedb
  SHELL
end
