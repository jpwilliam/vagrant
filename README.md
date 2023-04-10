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


