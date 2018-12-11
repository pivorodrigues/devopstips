## Vagrant
_(Based on Alura´s Vagrant Course)_

#

**1.** Install Virtualbox and Vagrant

**2.** Create directory and Vagrant file

_Vagrantfile example:_

```
Vagrant.configure("2") do |config|

    config.vm.box = "hashicorp/precise32"
    config.vm.define :web do |web_config|
        web_config.vm.network "private_network", ip: "192.168.33.10"
        web_config.vm.provision "puppet" do |puppet|
        	puppet.manifest_file = "web.pp"
        end
    end
end
```

**3.** Start the virtual machine

`$ vagrant up`

**4.** Access the virtual machine

`$ vagrant ssh`

#

**OBS:** Common commands in Vagrant

_$ Vagrant_
            - up

            - status

            - halt

            - reload

            - provision

            - ssh

            - destroy

            - suspend

            - resume

            - reload --provision

            - provision --debug
