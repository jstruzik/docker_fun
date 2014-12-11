# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

#ENV['VAGRANT_DEFAULT_PROVIDER'] ||= 'docker'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.provider "docker" do |d|
    d.vagrant_vagrantfile = "./custom_vm/Vagrantfile"
  end

  config.vm.define "nginx" do |nginx|
    nginx.vm.provider 'docker' do |d|
      d.build_dir = './nginx'
      d.name = 'robin_nginx'
      d.ports  = ['80:80']
    end
  end

  config.vm.define "php" do |php|
    php.vm.provider 'docker' do |d|
      d.build_dir = './php'
      d.name = 'robin_php'
      # d.create_args = ['-i', '-t']
      # Forward PHP-fpm to the vagrant box
      d.ports  = ['9000:9000']
    end
    # php.vm.synced_folder ".", "/var/www", owner: 'web', group: 'web'
  end

  config.vm.provision "docker" do |d|
    d.build_image "./nginx",
      args: "-t =\"nginx\""
    d.run "nginx",
      cmd: "bash -l",
      args: "-v '/vagrant:/var/www'"
  end

end
