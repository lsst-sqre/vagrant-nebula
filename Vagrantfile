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

  config.vm.define 'vagrant-nebula', primary: true do |define|
    define.vm.box       = 'openstack-vagrant-nebula'
    define.ssh.username = 'ubuntu'

    define.vm.provider :openstack do |os|
      os.openstack_auth_url = ENV['OS_AUTH_URL']
      os.username           = ENV['OS_USERNAME']
      os.password           = ENV['OS_PASSWORD']
      os.tenant_name        = ENV['OS_PROJECT_NAME']
      os.flavor             = ENV['OS_FLAVOR_NAME'] || 'm1.medium'
      os.image              = ENV['OS_IMAGE_NAME'] || 'b1f4bb91-13fb-4e73-b697-3c0ab23d17ec'
      os.floating_ip_pool   = 'ext-net'
      os.security_groups    = ['default', 'remote SSH', 'remote mosh']
      os.networks           = ['fc77a88d-a9fb-47bb-a65d-39d1be7a7174'] # LSST-net
    end
  end
end
