required_plugins = %w{
  vagrant-openstack-provider
}

plugins_to_install = required_plugins.select { |plugin| not Vagrant.has_plugin? plugin }
if not plugins_to_install.empty?
  puts "Installing plugins: #{plugins_to_install.join(' ')}"
  system "vagrant plugin install #{plugins_to_install.join(' ')}"
  exec "vagrant #{ARGV.join(' ')}"
end

Vagrant.configure('2') do |config|
  config.ssh.username = 'vagrant'

  config.vm.define 'el6' do |define|
    define.vm.provider :openstack do |provider, override|
      # centos-6-stack-lsst_distrib-w_2016_20-20160516164545
      provider.image = '2ee625d0-bada-4446-831e-c3982f75771e'
      provider.server_name = "el6-#{ENV['USER']}"
    end
  end

  config.vm.define 'el7' do |define|
    define.vm.provider :openstack do |provider, override|
      # centos-7-stack-lsst_distrib-w_2016_20-20160516164545
      provider.image = '2c6ae965-502f-4c43-b486-02e5a865d81b'
      provider.server_name = "el7-#{ENV['USER']}"
    end
  end

  config.vm.define 'el7-docker' do |define|
    define.vm.provider :openstack do |provider, override|
      provider.image       = '59a2a478-11ab-41c5-affc-29706d38d65a'
      provider.server_name = "el7-docker-#{ENV['USER']}"
      provider.flavor      = 'm1.xlarge'
    end
  end

  config.vm.provider :openstack do |os,override|
    os.sync_method        = 'none'
    os.user_data          = <<-EOS
#cloud-config
system_info:
  default_user:
    name: vagrant
    EOS
    os.username           = ENV['OS_USERNAME']
    os.password           = ENV['OS_PASSWORD']
    os.tenant_name        = ENV['OS_PROJECT_NAME']
    os.openstack_auth_url = ENV['OS_AUTH_URL']
    os.flavor             = 'm4.large'
    os.floating_ip_pool   = 'ext-net'
    os.security_groups    = ['default', 'remote SSH']
    os.networks           = ['fc77a88d-a9fb-47bb-a65d-39d1be7a7174']
  end
end
