# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  # TODO define method for instance boilerplate

  config.vm.define :db do |db|
    db.vm.network :private_network, ip: '192.168.22.4'
    db.vm.hostname = "db"
    
    db.vm.provider 'virtualbox' do |v|
      v.name = 'db'
      v.customize ['modifyvm', :id, '--memory', 512]
    end

    db.vm.provision :chef_solo do |chef|
      # Librarian like to control the cookbooks dir, so store our
      # own cookbooks separately
      chef.cookbooks_path = ["chef/cookbooks", "chef/lib/cookbooks"]

      chef.add_recipe "db-main"
    end
  end

  # Webapp instance with OE war on Tomcat 
  # Not needed if you run a Tomcat instance on host 
  # (hit web.host.local VHost in that case)
  # config.vm.define :app do |app|
  #   app.vm.network :private_network, ip: '192.168.22.3'
  #   app.vm.hostname = "app"
  #
  #   app.vm.provider 'virtualbox' do |v|
  #     v.name = 'app'
  #     v.customize ['modifyvm', :id, '--memory', 2048]
  #   end
  #
  #   app.vm.provision :chef_solo do |chef|
  #     chef.cookbooks_path = ["chef/cookbooks", "chef/lib/cookbooks"]
  #     chef.add_recipe "app-main"
  #   end
  # end
   
  config.vm.define :geoserver do |geoserver|
    geoserver.vm.network :private_network, ip: '192.168.22.5'
    geoserver.vm.hostname = "geoserver"
    
    geoserver.vm.provider 'virtualbox' do |v|
      v.name = 'geoserver'

      # GeoServer needs a lot more memory
      v.customize ['modifyvm', :id, '--memory', 1024]
    end

    geoserver.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = ["chef/cookbooks", "chef/lib/cookbooks"]
      chef.add_recipe "geoserver-main"
    end
  end
   
  config.vm.define :web do |web|
    web.vm.network :private_network, ip: '192.168.22.2'
    web.vm.hostname = "web"

    web.vm.provider 'virtualbox' do |v|
      v.name = 'web'
      v.customize ['modifyvm', :id, '--memory', 512]
    end
    
    web.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = ["chef/cookbooks", "chef/lib/cookbooks"]
      chef.add_recipe "web-main"
    end 
  end
   
end
