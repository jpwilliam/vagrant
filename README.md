# vagrant
## Config Vagrant
Dans ce projet nous allons créer deux machines virtuelles à partir d'un fichier `Vagrantfile`.


```ruby
config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024", "--cpus","1"]
  end
``` 

Avec cette option on peut définir la RAM de la machine virtuelle ainsi que le nombre de processeurs dédiés à la VM.

Pour créer les VM sur votre terminal, vous pouvez taper la commande suivante:

```bash
vagrant up
``` 

## Config ansible

A la fin du demarrage des VM , nous avons la possibilité d'installer de nombeuses applications sur chacun des serveurs.

Dans l'exemple présent nous créons un fichier d'inventaire dynamique à partir des informations présents dans une partie du fichier `Vagrantfile` ci-dessous:

```ruby
config.vm.provision :ansible do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.groups = {
      "web" => ["vagrant1"],
      "db" => ["vagrant2"],
      "group3" => ["vagrant[1:2]"]
    }
  end
```

Cette entrée permet de créer des groupes composants les VM indiquées. Le fichier `playbook.yml` contient les informations qui seront appliquées aux différentes VM. Dans le cas présent nous allons installer le package `apache2` sur la VM `vagrant1` qui compose le groupe `web` 

