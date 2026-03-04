Vagrant.configure("2") do |config|
  
  # 1. CONTROL NODE
  config.vm.define "control" do |control|
    control.vm.box = "ubuntu/focal64"
    control.vm.hostname = "ansible-control"
    control.vm.network "private_network", ip: "192.168.56.10"
    
    control.vm.provider "virtualbox" do |vb|
      vb.memory = "2048" # 2GB
      vb.cpus = 2
      vb.name = "Ansible-Control"
    end

    control.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y software-properties-common
      add-apt-repository --yes --update ppa:ansible/ansible
      apt-get install -y ansible
    SHELL
  end

  # 2. MANAGED NODE 1
  config.vm.define "node1" do |node1|
    node1.vm.box = "ubuntu/focal64"
    node1.vm.hostname = "ubuntu-target"
    node1.vm.network "private_network", ip: "192.168.56.11"
    
    node1.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = 1
      vb.name = "Ubuntu-Target"
    end
  end

  # 3. MANAGED NODE 2
  config.vm.define "node2" do |node2|
    node2.vm.box = "almalinux/9"
    node2.vm.hostname = "alma-target"
    node2.vm.network "private_network", ip: "192.168.56.12"
    
    node2.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = 1
      vb.name = "Alma-Target"
    end

    node2.vm.provision "shell", inline: "dnf install -y python3"
  end
end