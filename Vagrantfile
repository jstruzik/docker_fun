# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

#ENV['VAGRANT_DEFAULT_PROVIDER'] ||= 'docker'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.provider "docker" do |d|
    d.vagrant_vagrantfile = "./custom_vm/Vagrantfile"
    config.vm.network "forwarded_port", guest: 80, host: 8080
  end

  config.vm.define "php" do |php|
    php.vm.provider 'docker' do |d|
      d.build_dir = './php'
      d.name = 'robin_php'
      d.ports  = ['9000:9000']
    end
    php.vm.synced_folder "./src", "/var/www/robin", owner: 'web', group: 'web'
  end

  config.vm.define "nginx" do |nginx|
    nginx.vm.provider 'docker' do |d|
      d.build_dir = './nginx'
      d.name = 'robin_nginx'
      d.create_args = ['-i', '-t']
      d.ports  = ['80:80']
      d.link('robin_php:php')
    end
    nginx.vm.synced_folder "./src", "/var/www/robin", owner: 'web', group: 'web'
  end

  #config.vm.provision "docker" do |d|
  #  d.build_image "./nginx",
  #    args: "-t =\"nginx\""
  #  d.run "nginx",
  #    cmd: "bash -l",
  #    args: "-v '/vagrant:/var/www'"
  #end

end
