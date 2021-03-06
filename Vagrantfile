Vagrant.configure("2") do |config|
    # Configure the box to use
    config.vm.box = 'debian/jessie64'

    # Configure the network interfaces
    config.vm.network :private_network, ip: "192.168.33.7"

    # Configure shared folders
    config.vm.synced_folder ".", "/var/www/coopcycle",
        owner: "www-data",
        group: "www-data",
        mount_options: ["dmode=775,fmode=664"]

    # Configure VirtualBox environment
    config.vm.provider :virtualbox do |v|
        v.customize [ "modifyvm", :id, "--memory", 2048 ]
    end

    config.vm.provision :hosts do |provisioner|
        provisioner.add_host '127.0.0.1', ['postgres', 'redis', 'osrm']
    end

    # Just install Docker
    config.vm.provision "docker" do |d|
    end

    # Provision the box with Ansible
    config.vm.provision :ansible do |ansible|
        ansible.extra_vars = { ansible_ssh_user: 'vagrant' }
        ansible.playbook = "ansible/vagrant.yml"
    end
end
