VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'ubuntu/trusty64'

  config.vm.provider :virtualbox do |vb|
    vb.customize ['modifyvm', :id, '--memory', '2048']
  end

  config.vm.network :forwarded_port, guest: 3000, host: 3001
  config.berkshelf.enabled = true

  config.vm.provision :chef_solo do |chef|

    chef.add_recipe 'apt'
    chef.add_recipe 'nodejs'
    chef.add_recipe 'ruby_build'
    chef.add_recipe 'rbenv::vagrant'
    chef.add_recipe 'rbenv::user'
    chef.add_recipe 'postgresql::server'
    chef.add_recipe 'postgresql::client'
    chef.add_recipe 'postgresql::libpq'
    chef.add_recipe 'postgresql::setup_users'

    chef.json = {
      rbenv: {
        user_installs: [{
          user: 'vagrant',
          rubies: ['2.2.2'],
          global: '2.2.2',
          gems: {
            '2.2.2' => [{
              name: 'bundler'
            }]
          }
        }]
      },
      postgresql: {
        users: [{
          username: 'vagrant',
          password: '1111',
          createdb: true,
          login: true
        }]
      }
    }
  end
end
