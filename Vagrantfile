# -*- mode: ruby -*-
# vi: set ft=ruby :

require "yaml"
y = YAML.load File.open ".chef/rackspace_secrets.yaml"

Vagrant.configure("2") do |config|

  config.butcher.knife_config_file = '.chef/knife.rb'

  1.times do |num|

    index = "%02d" % [num + 1]

    config.vm.define :"elasticsearch_theodi_org_#{index}" do |config|
      config.vm.box      = "dummy"
      config.vm.hostname = "elasticsearch-#{index}"

      config.ssh.private_key_path = "./.chef/id_rsa"
      config.ssh.username         = "root"

      config.vm.provider :rackspace do |rs|
        rs.username        = y["username"]
        rs.api_key         = y["api_key"]
        rs.flavor          = /512M/
        rs.image           = /Precise/
        rs.public_key_path = "./.chef/id_rsa.pub"
        rs.auth_url        = "https://lon.identity.api.rackspacecloud.com/v2.0"
      end

      config.vm.provision :shell, :inline => "curl -L https://www.opscode.com/chef/install.sh | bash"

      config.vm.provision :chef_client do |chef|
        chef.node_name              = "elasticsearch"
        chef.environment            = "production"
        chef.chef_server_url        = "https://chef.theodi.org"
        chef.validation_client_name = "chef-validator"
        chef.validation_key_path    = ".chef/chef-validator.pem"
        chef.run_list               = chef.run_list = [
            "role[elasticsearch_server]"
        ]
      end
    end
  end

  config.vm.define :logstash_theodi_org do |config|
    config.vm.box      = "dummy"
    config.vm.hostname = "logstash"

    config.ssh.private_key_path = "./.chef/id_rsa"
    config.ssh.username         = "root"

    config.vm.provider :rackspace do |rs|
      rs.username        = y["username"]
      rs.api_key         = y["api_key"]
      rs.flavor          = /512M/
      rs.image           = /Precise/
      rs.public_key_path = "./.chef/id_rsa.pub"
      rs.auth_url        = "https://lon.identity.api.rackspacecloud.com/v2.0"
    end

    config.vm.provision :shell, :inline => "curl -L https://www.opscode.com/chef/install.sh | bash"

    config.vm.provision :chef_client do |chef|
      chef.node_name              = "logstash"
      chef.environment            = "production"
      chef.chef_server_url        = "https://chef.theodi.org"
      chef.validation_client_name = "chef-validator"
      chef.validation_key_path    = ".chef/chef-validator.pem"
      chef.run_list               = chef.run_list = [
          "role[logstash_server]"
      ]
    end
  end

  config.vm.define :kibana_theodi_org do |config|
    config.vm.box      = "dummy"
    config.vm.hostname = "kibana"

    config.ssh.private_key_path = "./.chef/id_rsa"
    config.ssh.username         = "root"

    config.vm.provider :rackspace do |rs|
      rs.username        = y["username"]
      rs.api_key         = y["api_key"]
      rs.flavor          = /512M/
      rs.image           = /Precise/
      rs.public_key_path = "./.chef/id_rsa.pub"
      rs.auth_url        = "https://lon.identity.api.rackspacecloud.com/v2.0"
    end

    config.vm.provision :shell, :inline => "curl -L https://www.opscode.com/chef/install.sh | bash"

    config.vm.provision :chef_client do |chef|
      chef.node_name              = "kibana"
      chef.environment            = "production"
      chef.chef_server_url        = "https://chef.theodi.org"
      chef.validation_client_name = "chef-validator"
      chef.validation_key_path    = ".chef/chef-validator.pem"
      chef.run_list               = chef.run_list = [
          "role[kibana]"
      ]
    end
  end
end