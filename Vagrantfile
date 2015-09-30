# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  ip_address = ENV['VAGRANT_IP'] || '192.168.0.29'
  hostname = ENV['VAGRANT_HOSTNAME'] || 'vagrant.local.rf29.net'
  user_key_file = ENV['GITHUB_PRIVATE_KEY'] || '~/.ssh/id_rsa'
  shared_repos = %w(refinery29 rocketship zeppelin)

  config.vm.box = 'r29-alpha2'
  config.vm.network 'private_network', ip: ip_address
  config.vm.hostname = hostname

  shared_repos.each do | dir |
    config.vm.synced_folder dir, "/var/#{dir}",
                            owner: 'devuser', group: 'dev'
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = 'ansible/vagrant_last_mile.yml'
  end
end
