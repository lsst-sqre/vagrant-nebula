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
#require 'aws-sdk-v1'
#require 'vagrant-aws-route53'

Vagrant.configure('2') do |config|
  config.ssh.username = 'vagrant'

  config.vm.define 'es-1' do |define|
    define.vm.provider :openstack do |provider, override|
      provider.image = 'ubuntu_pan_es_20160420034425'
      provider.flavor = 'n-rd1.large'
      provider.server_name = "es-1-#{ENV['USER']}"
    end
  end

  config.vm.define 'es-2' do |define|
    define.vm.provider :openstack do |provider, override|
      provider.image = 'ubuntu_pan_es_20160420034425'
      provider.flavor = 'n-rd1.large'
      provider.server_name = "es-2-#{ENV['USER']}"
    end
  end

  config.vm.define 'es-3' do |define|
    define.vm.provider :openstack do |provider, override|
      provider.image = 'ubuntu_pan_es_20160420034425'
      provider.flavor = 'n-rd1.large'
      provider.server_name = "es-3-#{ENV['USER']}"
    end
  end

  config.vm.define 'es-4' do |define|
    define.vm.provider :openstack do |provider, override|
      provider.image = 'ubuntu_pan_es_20160420034425'
      provider.flavor = 'n-rd1.large'
      provider.server_name = "es-4-#{ENV['USER']}"
    end
  end

  config.vm.define 'es-k' do |define|
    define.vm.provider :openstack do |provider, override|
      provider.image = 'ubuntu_pan_es_k_20160420013734'
      provider.flavor = 'n-rcd1.large'
      provider.server_name = "es-k-#{ENV['USER']}"
    end
  end

  config.vm.define 'lfr' do |define|
    define.vm.provider :openstack do |provider, override|
      provider.image = 'ubuntu_pan_lfr_20160420000828'
      provider.flavor = 'm4.large'
      provider.server_name = "lfr-#{ENV['USER']}"
    end
  end

  config.vm.provider :openstack do |os, override|
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
    os.floating_ip_pool   = 'ext-net'
    os.security_groups    = ['default', 'remote SSH']
    os.networks           = ['fc77a88d-a9fb-47bb-a65d-39d1be7a7174']
  end
end
