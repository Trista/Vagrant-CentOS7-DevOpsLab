# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.network "private_network", type: "dhcp"

  # Jenkins Controller
  config.vm.define "jenkins-controller" do |controller|
    controller.vm.box = "centos/7"
    controller.vm.network "forwarded_port", guest: 8080, host: 8080
    controller.vm.provision "shell", inline: <<-SHELLPROVISION
      # Update packages
	  sudo yum -y update
      # Install wget
      sudo yum install -y wget 
      # Install java
      sudo yum install -y java-1.8.0-openjdk.x86_64
      # Add the Jenkins repository to the yum repos
      sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
      # Import the key
      # TO DO: need clarification on this step
      sudo rpm --import http://jenkins-ci.org/redhat/jenkins-ci.org.key
      # Install Jenkins
      yum install -y jenkins
      # Allow access to jenkins via 8080 port
      sudo firewall-cmd --zone=public --permanent --add-port=8080/tcp
      sudo firewall-cmd --reload
      # Install netstat
      yum install -y net-tools
    SHELLPROVISION
    controller.vm.provider :virtualbox do |v|
         v.gui = false
         v.memory = 2048
      end
  end

  # Jenkins Agent 1
  config.vm.define "agent1" do |agent1|
    agent1.vm.box = "centos/7"
    agent1.vm.provision "shell", inline: <<-SHELLPROVISION
      # Update packages
	  sudo yum -y update
	  echo "TO DO: Install and configure the first Jenkins agent."  
    SHELLPROVISION
    agent1.vm.provider :virtualbox do |v|
         v.gui = false
         v.memory = 512
      end
  end
end