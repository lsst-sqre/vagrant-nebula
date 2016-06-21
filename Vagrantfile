required_plugins = %w{
  vagrant-openstack-provider
}

plugins_to_install = required_plugins.select { |plugin| not Vagrant.has_plugin? plugin }
if not plugins_to_install.empty?
  puts "Installing plugins: #{plugins_to_install.join(' ')}"
  system "vagrant plugin install #{plugins_to_install.join(' ')}"
  exec "vagrant #{ARGV.join(' ')}"
end

def sname(host)
  "#{ENV['USER']}-#{host}"
end

Vagrant.configure('2') do |config|
  config.ssh.username = 'vagrant'

  config.vm.define 'el6' do |define|
    define.vm.provider :openstack do |provider, override|
      # centos-6-stack-lsst_distrib-v12_0-20160621152742
      provider.image = 'eb1f5e9a-d531-488a-8106-a7973af3acf3'
      provider.server_name = sname('el6')
    end
  end

  config.vm.define 'el7' do |define|
    define.vm.provider :openstack do |provider, override|
      # centos-7-stack-lsst_distrib-v12_0-20160621152742
      provider.image = '0e0185c9-aaf6-4f1e-954d-c5a68fd99325'
      provider.server_name = sname('el7')
    end
  end

  config.vm.define 'el7-docker' do |define|
    define.vm.provider :openstack do |provider, override|
      provider.image       = '59a2a478-11ab-41c5-affc-29706d38d65a'
      provider.server_name = sname('el7-docker')
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
