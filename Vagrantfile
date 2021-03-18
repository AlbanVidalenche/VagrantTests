## Fichier Vagrant TP
# /!\ Les lignes 16, 26, et 28 sont à modifier selon vos chemins et les noms de vos fichiers 

Vagrant.require_version '>=2.2.10'

Vagrant.configure('2') do |config|

  #SSH
  config.ssh.forward_agent = true
  config.ssh.insert_key = false
  config.ssh.extra_args = ['-q']
  config.ssh.forward_env = ['WORKDIR']

  # VMS
  config.vm.define "ansible" do |ansible|
        ansible.vm.hostname = 'ansible.workshop'
        ansible.vm.provision "shell",
            inline: "apt-get update && apt-get install -y ansible"
        ansible.vm.network 'private_network', ip: '10.20.30.10'
  end

  config.vm.define "node_01" do |node_01|
  	node_01.vm.hostname = 'node-01.workshop'
  	node_01.vm.network 'private_network', ip: '10.20.30.11'
  end

  config.vm.define "node_02" do |node_02|
  	node_02.vm.hostname = 'node-02.workshop'
  	node_02.vm.network 'private_network', ip: '10.20.30.12'
  end

  config.vm.define "node_03" do |node_03|
  	node_03.vm.hostname = 'node-03.workshop'
  	node_03.vm.network 'private_network', ip: '10.20.30.13'
  end


  config.vm.box = 'bento/debian-10'

  #SSH KEYS
  config.vm.provision "file", source: "~/.ssh/id_yubikey.pub", destination: "~/.ssh/yubikey.pub" 
  config.vm.provision "shell", inline: <<-SHELL
  	cat /home/vagrant/.ssh/yubikey.pub >> /home/vagrant/.ssh/authorized_keys 
  SHELL


  #VM - Virtualbox
  config.vm.provider 'virtualbox'
  config.vm.provider :virtualbox do |virtualbox|
     virtualbox.memory = 512
     virtualbox.cpus = 1
     virtualbox.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
  end
end
