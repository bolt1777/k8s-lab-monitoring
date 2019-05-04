ENV["LC_ALL"] = "en_US.UTF-8"

Vagrant.configure("2") do |config|


  config.vm.box = "geerlingguy/centos7"
  config.ssh.forward_agent = true # So that boxes don't have to setup key-less ssh
  config.ssh.insert_key = false # To generate a new ssh key and don't use the default Vagrant one

  config.vm.define:"k8s-minikub"
  config.vm.hostname = "k8s-minikub"

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.manage_guest = true
  
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "8096"
    vb.cpus = 4
   end
  config.vm.network :private_network, ip: "192.168.50.50", auto_config: true
  config.vm.provision :ansible do |ansible|
        ansible.playbook = "ansible/playbook.yml"
        ansible.inventory_path = "ansible/inventory"
  end
end
