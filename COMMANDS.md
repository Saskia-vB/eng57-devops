Terminal commands:

```bash

vagrant init ubuntu/xenial64

vagrant up

put console.log in gitignore

vagrant ssh

sudo apt-get update -y

sudo apt-get install nginx -y

sudo systemctl start nginx

```

Vagrant file:

- Install required plugins

- In order to give an aliase to your IP:
```ruby
required_plugins = ["vagrant-hostsupdater"]
```

```ruby
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end
```

- Configuration: 
	- The settings within config.vm modify the configuration of the machine that Vagrant manages.
	- config.vm.box : configures what box the machine will be brought up against. The value here should be the name of an installed box (bash: vagrant init unbuntu/xenial64)
```ruby

Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.network "private_network", ip: "192.168.10.150"
```
```ruby
    config.hostsupdater.aliases = ["database.local"]
    config.vm.provision "shell", path: "environment/db/provision.sh", privileged: false
end

```
