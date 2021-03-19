require_relative './vagrant/key_authorization'


Vagrant.configure('2') do |config|
  config.vm.box = 'centos/8'
  authorize_key_for_root config, '~/.ssh/id_dsa.pub', '~/.ssh/id_rsa.pub'

  {
    'master'    => '192.168.99.10',
    'node'   => '192.168.99.11',
  }.each do |short_name, ip|
    config.vm.define short_name do |host|
      host.vm.network 'private_network', ip: ip
      host.vm.hostname = "#{short_name}.ansible-swarm.dev"
    end
  end
end