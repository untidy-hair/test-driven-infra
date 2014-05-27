VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'CentOS6.4'
  config.vm.box_url = 'https://dl.dropboxusercontent.com/u/515908/CentOS-6.4-x86.box'

  config.vm.provider :digital_ocean do |provider, override|
    override.ssh.private_key_path = '~/.ssh/digital_ocean'
    override.vm.box = 'digital_ocean'
    override.vm.box_url =
      'https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box'
    provider.client_id = ENV['DIGITALOCEAN_CLIENT_ID']
    provider.api_key = ENV['DIGITALOCEAN_API_KEY']
    provider.image = 'CentOS 6.4 x64'
    provider.region = 'San Francisco 1'
    provider.size = '512MB'
    provider.ca_path = '/usr/local/opt/curl-ca-bundle/share/ca-bundle.crt'
    if ENV['WERCKER'] == 'true'
      provider.ssh_key_name = 'wercker'
    else
      provider.ssh_key_name = 'MacOS'
    end 
  end


  config.vm.provision :shell, inline: <<-EOF
    sudo rpm -ivh \
      http://yum.puppetlabs.com/puppetlabs-release-el-6.noarch.rpm 
    sudo yum install -y puppet
  EOF

  config.vm.define :app do |c|
    c.vm.provision :shell do |shell|
      shell.path = 'provision.sh'
      shell.args = 'app'
    end
  end

  config.vm.define :proxy do |c|
    c.vm.provision :shell do |shell|
      shell.path = 'provision.sh'
      shell.args = 'proxy'
    end
  end
end
