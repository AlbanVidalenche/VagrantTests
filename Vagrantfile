## Fichier Vagrant TP 
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
        ansible.vm.synced_folder '/home/alban/testing/vagrant_shared_folder', '/srv/app',  #Chemin à modifier selon votre cas
            type: 'nfs',
            mount_options: ['tcp', 'nolock', 'actimeo=1'],
  	    nfs_udp: 'false'
        ansible.vm.network 'private_network', ip: '10.20.30.10'
  end

  config.vm.box = 'bento/debian-10'

  #SSH KEYS
  config.vm.provision "file", source: "~/.ssh/id_yubikey.pub", destination: "~/.ssh/yubikey.pub" # Même chose ici
  config.vm.provision "shell", inline: <<-SHELL
  	cat /home/vagrant/.ssh/yubikey.pub >> /home/vagrant/.ssh/authorized_keys  # Pareil ici
  SHELL



  #VM - Virtualbox
  config.vm.provider 'virtualbox'
  config.vm.provider :virtualbox do |virtualbox|
     virtualbox.memory = 512
     virtualbox.cpus = 1
     virtualbox.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
  end
end
