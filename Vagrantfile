# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define "ohs1212" , primary: true do |ohs1212|

    ohs1212.vm.box = "centos-7-1511-x86_64"
    ohs1212.vm.box_url = "https://dl.dropboxusercontent.com/s/filvjntyct1wuxe/centos-7-1511-x86_64.box"

    ohs1212.vm.provider :vmware_fusion do |v, override|
      override.vm.box = "centos-7-1511-x86_64-vmware"
      override.vm.box_url = "https://dl.dropboxusercontent.com/s/h5g5kqjrzq5dn53/centos-7-1511-x86_64-vmware.box"
    end

    ohs1212.vm.hostname = "ohs1212.example.com"
    ohs1212.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=777","fmode=777"]
    ohs1212.vm.synced_folder "/Users/edwin/software", "/software", :mount_options => ["dmode=777","fmode=777"]

    ohs1212.vm.network :private_network, ip: "10.10.10.35"

    ohs1212.vm.provider :vmware_fusion do |vb|
      vb.vmx["numvcpus"] = "2"
      vb.vmx["memsize"] = "2048"
    end

    ohs1212.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "2048"]
      vb.customize ["modifyvm", :id, "--name", "ohs1212"]
      vb.customize ["modifyvm", :id, "--cpus"  , 2]
    end

    ohs1212.vm.provision :shell, :inline => "ln -sf /vagrant/puppet/hiera.yaml /etc/puppetlabs/code/hiera.yaml;rm -rf /etc/puppetlabs/code/modules;ln -sf /vagrant/puppet/environments/development/modules /etc/puppetlabs/code/modules"

    # in order to enable this shared folder, execute first the following in the host machine: mkdir log_puppet_weblogic && chmod a+rwx log_puppet_weblogic
    #ohs1212.vm.synced_folder "./log_puppet_weblogic", "/tmp/log_puppet_weblogic", :mount_options => ["dmode=777","fmode=777"]

    ohs1212.vm.provision :puppet do |puppet|
      puppet.environment_path     = "puppet/environments"
      puppet.environment          = "development"

      puppet.manifests_path       = "puppet/environments/development/manifests"
      puppet.manifest_file        = "site.pp"

      puppet.options           = [
                                  '--verbose',
                                  '--report',
                                  '--trace',
#                                  '--debug',
#                                  '--parser future',
                                  '--strict_variables',
                                  '--hiera_config /vagrant/puppet/hiera.yaml'
                                 ]
      puppet.facter = {
        "environment"     => "development",
        "vm_type"         => "vagrant",
      }

    end

  end

  config.vm.define "ohs1221" do |ohs1221|

    ohs1221.vm.box = "centos-7-1511-x86_64"
    ohs1221.vm.box_url = "https://dl.dropboxusercontent.com/s/filvjntyct1wuxe/centos-7-1511-x86_64.box"

    ohs1221.vm.provider :vmware_fusion do |v, override|
      override.vm.box = "centos-7-1511-x86_64-vmware"
      override.vm.box_url = "https://dl.dropboxusercontent.com/s/h5g5kqjrzq5dn53/centos-7-1511-x86_64-vmware.box"
    end

    ohs1221.vm.hostname = "ohs1221.example.com"
    ohs1221.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=777","fmode=777"]
    ohs1221.vm.synced_folder "/Users/edwin/software", "/software"

    ohs1221.vm.network :private_network, ip: "10.10.10.36"

    ohs1221.vm.provider :vmware_fusion do |vb|
      vb.vmx["numvcpus"] = "2"
      vb.vmx["memsize"] = "2048"
    end

    ohs1221.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "2048"]
      vb.customize ["modifyvm", :id, "--name", "ohs1221"]
      vb.customize ["modifyvm", :id, "--cpus"  , 2]
    end

    ohs1221.vm.provision :shell, :inline => "ln -sf /vagrant/puppet/hiera.yaml /etc/puppetlabs/code/hiera.yaml;rm -rf /etc/puppetlabs/code/modules;ln -sf /vagrant/puppet/modules /etc/puppetlabs/code/modules"

    ohs1221.vm.provision :puppet do |puppet|

      puppet.environment_path  = "puppet/environments"
      puppet.environment       = "development"

      puppet.manifests_path    = "puppet/environments/development/manifests"
      puppet.manifest_file     = "site.pp"

      puppet.options           = [
                                  '--verbose',
                                  '--report',
                                  '--trace',
#                                  '--debug',
#                                  '--parser future',
                                  '--strict_variables',
                                  '--hiera_config /vagrant/puppet/hiera.yaml'
                                 ]
      puppet.facter = {
        "environment"     => "development",
        "vm_type"         => "vagrant",
      }

    end

  end
end
