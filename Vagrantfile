Vagrant.configure("2") do |config|
    # Vagrant Box to use
    config.vm.box = "hashicorp/bionic64"
    # Setting up network details
    config.vm.network "private_network", ip: "192.168.10.150"
    # Specifying which provision file to run
    config.vm.provision "shell", path: "provision.sh"
end