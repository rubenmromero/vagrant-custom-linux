# Customizable Vagrantfile to start and provision Debian & CentOS VMs based on VirtualBox provider

# Environment Import
require 'yaml'
env_config = YAML::load_file('./config.yml')
boxes_config = YAML::load_file('./boxes.yml')

project = env_config['project']
linux_distro = env_config['linux_distro']
ip_addr = env_config['ip_addr']
vm_cpus = env_config['vm_cpus']
vm_memory = env_config['vm_memory']
hostname_suffix = env_config['hostname_suffix']

Vagrant.configure('2') do |config|
    # Enable/Disable auto update of virtualbox guest additions
    if Vagrant.has_plugin?('vagrant-vbguest')
        config.vbguest.auto_update = true
    end

    # Project
    config.vm.define :"#{project}" do |node_conf|
        if linux_distro == 'debian'
            node_conf.vm.box = boxes_config['debian_box']
            node_conf.vm.box_url = boxes_config['debian_box_url'] if boxes_config['debian_box_url']
        else
            node_conf.vm.box = boxes_config['centos_box']
            node_conf.vm.box_url = boxes_config['centos_box_url'] if boxes_config['centos_box_url']
        end
        node_conf.vm.network :private_network, ip: ip_addr
        node_conf.vm.hostname = "#{project}.#{hostname_suffix}"

        node_conf.vm.provider 'virtualbox' do |v|
            v.customize ['modifyvm', :id, '--groups', "/#{project}-#{linux_distro}"]
            v.customize ['modifyvm', :id, '--name', "#{project}-#{linux_distro}"]
            v.customize ['modifyvm', :id, '--cpus', vm_cpus]
            v.customize ['modifyvm', :id, '--memory', vm_memory]
            v.customize ['modifyvm', :id, '--ioapic', 'on']
            v.customize ['modifyvm', :id, '--natdnshostresolver1', 'off']
            v.customize ['modifyvm', :id, '--nictype1', 'virtio']
            v.customize ['modifyvm', :id, '--nictype2', 'virtio']
            v.customize ["modifyvm", :id, '--graphicscontroller', 'vmsvga']
        end

        # Shared folders
        node_conf.vm.synced_folder "../", "/opt/#{project}", owner: 'vagrant', group: 'vagrant'

        # Package list initial update for Debian distros
        if linux_distro == 'debian'
            apt_update = "apt-get update"
            node_conf.vm.provision 'shell', inline: apt_update
        end
    end
end
