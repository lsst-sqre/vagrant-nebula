required_plugins = %w{
  vagrant-openstack-provider
}

plugins_to_install = required_plugins.select { |plugin| not Vagrant.has_plugin? plugin }
if not plugins_to_install.empty?
  puts "Installing plugins: #{plugins_to_install.join(' ')}"
  system "vagrant plugin install #{plugins_to_install.join(' ')}"
  exec "vagrant #{ARGV.join(' ')}"
end

require 'vagrant-openstack-provider'

Vagrant.configure('2') do |config|
  config.ssh.username = 'vagrant'

  config.vm.define 'el6' do |define|
    define.vm.provider :openstack do |provider, override|
      provider.image = 'a4bd6e75-1ef5-49ca-a71d-15f379626552'
      provider.server_name = "el6-#{ENV['USER']}"
    end
  end

  config.vm.define 'el7' do |define|
    define.vm.provider :openstack do |provider, override|
      provider.image = '3a26f5a2-856a-406f-9ea1-2aa58f230a62'
      provider.server_name = "el7-#{ENV['USER']}"
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
    os.flavor             = 'm1.xlarge'
    os.floating_ip_pool   = 'ext-net'
    os.security_groups    = ['default', 'remote SSH']
    os.networks           = ['fc77a88d-a9fb-47bb-a65d-39d1be7a7174']
  end
end
