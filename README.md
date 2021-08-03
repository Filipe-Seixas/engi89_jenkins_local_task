# Jenkins Hosting Task

## Installing Jenkins (Vagrant)

- Setup a directory for vagrant with `vagrant init`
- Open the Vagrantfile and change it:
```bash
Vagrant.configure("2") do |config|
	# Vagrant Box to use
    config.vm.box = "hashicorp/bionic64"
    # Setting up network details
    config.vm.network "private_network", ip: "192.168.10.150"
    # Specifying which provision file to run
    config.vm.provision "shell", path: "provision.sh"
end
```
- Create a provision.sh file:
```bash
#!/bin/bash

# Update and Upgrade machine
sudo apt-get update -y
sudo apt-get upgrade -y
# Install java which jenkins requires
sudo apt install openjdk-11-jdk -y
java -version
# Get and install jenkins
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update -y
sudo apt-get install jenkins -y
sudo systemctl status jenkins
```

## 1st Time Running Jenkins

- The first time jenkins is ran, it needs to be unlocked. Connect to `http://192.168.10.150:8080/`
- When prompted to enter a password, ssh into vagrant machine and use `sudo cat /var/lib/jenkins/secrets/initialAdminPassword` to check the password
- Enter the password on the browser and you can now complete the setup process