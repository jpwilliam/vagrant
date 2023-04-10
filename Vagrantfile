VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config| 
  # Use the same key for each machine 
  config.ssh.insert_key = false
#  config.vm.provider "virtualbox"
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024", "--cpus","1"]
  end

  config.vm.define "vagrant1" do |vagrant1|
    vagrant1.vm.box = "bento/debian-11"
    vagrant1.vm.network "forwarded_port", guest: 80, host: 8080 
    vagrant1.vm.network "forwarded_port", guest: 443, host: 8443
  end
  
  config.vm.define "vagrant2" do |vagrant2|
    vagrant2.vm.box = "bento/debian-11"
    vagrant2.vm.network "forwarded_port", guest: 80, host: 8081
    vagrant2.vm.network "forwarded_port", guest: 443, host: 8444
  end
  
  config.vm.provision :ansible do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.groups = {
      "web" => ["vagrant1"],
      "db" => ["vagrant2"],
      "group3" => ["vagrant[1:2]"]
    }  
  end
end
