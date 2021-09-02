# -*- mode: ruby -*-
# vi: set ft=ruby :
#

# change ips to whatever network you need it to run on
# i have this by default setup to work on host network interface br0 that is configured as a bridge
# this will assign a static ip on my private network range that my host is running on
VAGRANTFILE_API_VERSION = "2"
OSCTRL_IP_ADDRESS = ENV["OSCTRL_IP_ADDRESS"] || "10.0.0.50"

UBUNTU_2004_IP_ADDRESS = "10.0.0.51"
UBUNTU_1804_IP_ADDRESS = "10.0.0.52"
UBUNTU_1604_IP_ADDRESS = "10.0.0.53"
UBUNTU_1404_IP_ADDRESS = "10.0.0.54"
UBUNTU_1204_IP_ADDRESS = "10.0.0.55"

CENTOS_8_IP_ADDRESS = "10.0.0.120"
CENTOS_7_IP_ADDRESS = "10.0.0.121"
CENTOS_6_IP_ADDRESS = "10.0.0.122"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "osctrl" do |osctrl|
    osctrl.vm.box = "ubuntu/focal64"
    osctrl.vm.network "public_network", bridge: 'br0', ip: OSCTRL_IP_ADDRESS
    osctrl.vm.hostname = "osctrl-Dev"
    osctrl.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
    osctrl.vm.provision "shell" do |s|
      s.path = "deploy/provision.sh"
      s.args = [
        "--nginx", "--postgres", "--enroll", "--all-hostname",
        OSCTRL_IP_ADDRESS, "--password", "admin"
      ]
      privileged = false
    end
    osctrl.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 1
      v.customize [ "modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end

  config.vm.define "ubuntu2004" do |ubuntu2004|
    ubuntu2004.vm.box = "ubuntu/focal64"
    ubuntu2004.vm.network "public_network", bridge: 'br0',  ip: UBUNTU_2004_IP_ADDRESS
    ubuntu2004.vm.hostname = "ubuntu2004.node"
    ubuntu2004.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
    ubuntu2004.vm.provision "shell" do |s|
      s.path = "deploy/curl_command.sh"
      privileged = true
    end
    ubuntu2004.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 1
      v.customize [ "modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end

  config.vm.define "ubuntu1804" do |ubuntu1804|
    ubuntu1804.vm.box = "ubuntu/bionic64"
    ubuntu1804.vm.network "public_network", bridge: "br0", ip: UBUNTU_1804_IP_ADDRESS
    ubuntu1804.vm.hostname = "ubuntu1804.node"
    ubuntu1804.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
    ubuntu1804.vm.provision "shell" do |s|
      s.path = "deploy/curl_command.sh"
      privileged = true
    end
    ubuntu1804.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 1
      v.customize [ "modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end

  config.vm.define "ubuntu1604" do |ubuntu1604|
    ubuntu1604.vm.box = "ubuntu/xenial64"
    ubuntu1604.vm.network "public_network", bridge: "br0",  ip: UBUNTU_1604_IP_ADDRESS
    ubuntu1604.vm.hostname = "ubuntu1604.node"
    ubuntu1604.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
    ubuntu1604.vm.provision "shell", inline: "apt-get install dpkg-dev -y"
    # bug for now dont enroll these nodes
    #ubuntu1604.vm.provision "shell" do |s|
    #  s.path = "deploy/curl_command.sh"
    #  privileged = true
    #end
    ubuntu1604.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 1
      v.customize [ "modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end

  config.vm.define "ubuntu1404" do |ubuntu1404| ubuntu1404.vm.box = "ubuntu/trusty64"
    ubuntu1404.vm.network "public_network", bridge: "br0",  ip: UBUNTU_1404_IP_ADDRESS
    ubuntu1404.vm.hostname = "ubuntu1404.node"
    ubuntu1404.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
    ubuntu1404.vm.provision "shell", inline: "apt-get install dpkg-dev -y"
    # bug for now dont enroll these nodes
    #ubuntu1404.vm.provision "shell" do |s|
    #  s.path = "deploy/curl_command.sh"
    #  privileged = true
    #end
    ubuntu1404.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 1
      v.customize [ "modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end
#  config.vm.define "ubuntu1204" do |ubuntu1204|
#    ubuntu1204.vm.box = "ubuntu/precise64"
#    ubuntu1204.vm.network "public_network", bridge: "br0", ip: UBUNTU_1204_IP_ADDRESS
#    ubuntu1204.vm.hostname = "ubuntu1204.node"
#    ubuntu1204.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
#    # fill out provisioner loop here once we get ansible playbook setup
#    ubuntu1204.vm.provider "virtualbox" do |v|
#      v.memory = 1024
#      v.cpus = 1
#      v.customize [ "modifyvm", :id, "--natdnshostresolver1", "on"]
#    end
#  end
#
#  config.vm.define "centos6" do |centos6|
#    centos6.vm.box = "geerlingguy/centos6"
#    centos6.vm.network "public_network", bridge: "br0", ip: CENTOS_6_IP_ADDRESS
#    centos6.vm.hostname = "centos6.node"
#    centos6.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
#    centos6.vm.provision "shell" do |s|
#      s.path = "deploy/curl_command.sh"
#      privileged = true
#    end
#    centos6.vm.provider "virtualbox" do |v|
#      v.memory = 1024
#      v.cpus = 1
#      v.customize [ "modifyvm", :id, "--natdnshostresolver1", "on"]
#    end
#  end

  config.vm.define "centos7" do |centos7|
    centos7.vm.box = "geerlingguy/centos7"
    centos7.vm.network "public_network", bridge: "br0", ip: CENTOS_7_IP_ADDRESS
    centos7.vm.hostname = "centos7.node"
    centos7.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
    centos7.vm.provision "shell" do |s|
      s.path = "deploy/curl_command.sh"
      privileged = true
    end
    centos7.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 1
      v.customize [ "modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end

  config.vm.define "centos8" do |centos8|
    centos8.vm.box = "arfreitas/centos8-vbguest"
    centos8.vm.network "public_network", bridge: "br0", ip: CENTOS_8_IP_ADDRESS
    centos8.vm.hostname = "centos8.node"
    centos8.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
    centos8.vm.provision "shell" do |s|
      s.path = "deploy/curl_command.sh"
      privileged = true
    end
    centos8.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 1
      v.customize [ "modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end

  config.vm.define "splunk" do |splunk|
    splunk.vm.box = "cybersecurity/splunk"
    splunk.vm.network "public_network", bridge: "br0", ip: "10.0.0.130"
    splunk.vm.hostname =  "splunk.server"
    splunk.vm.provision "shell", inline: "cd /opt/splunk && ./splunk start --acept-eula"
    splunk.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
      v.customize [ "modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end
end

