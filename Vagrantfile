Vagrant::Config.run do |config|
  config.vm.box           = 'precise32'
  config.vm.box_url       = 'http://files.vagrantup.com/precise32.box'
  config.vm.host_name     = 'rails-dev-box'
  
  # Make the default OS X ~/Sites directory shared to access Rails apps located there
  config.vm.share_folder  'Sites', '/home/vagrant/Sites', '~/Sites', create: true

  # Forward port 3030 so we can still use 3000 locally
  config.vm.forward_port 3030, 3000

  config.vm.provision :puppet,
    :manifests_path => 'puppet/manifests',
    :module_path    => 'puppet/modules'
end
