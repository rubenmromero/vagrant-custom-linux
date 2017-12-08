# Customizable Vagrantfile to start and provision Debian & CentOS VMs based on VirtualBox provider

# Environment Import
require 'yaml'
env_config = YAML::load_file("./config.yml")

project = env_config['project']
linux_distro = env_config['linux_distro']
ip_addr = env_config['ip_addr']
vm_cpus = env_config['vm_cpus']
vm_memory = env_config['vm_memory']
hostname_suffix = env_config['hostname_suffix']

# Linux Boxes
box_debian = 'gigigo-debian-jessie-x64.box'
box_debian_url = 'http://box.gigigo.com/gigigo-debian-jessie-x64.box'
box_centos = 'gigigo-centos7-x64.box'
box_centos_url = 'http://box.gigigo.com/gigigo-centos7-x64.box'

Vagrant.configure('2') do |config|
    # Enable/Disable auto update of virtualbox guest additions
    if Vagrant.has_plugin?("vagrant-vbguest")
        config.vbguest.auto_update = false
    end

    # Project
    config.vm.define :"#{project}" do |node_conf|
        if linux_distro == 'debian'
            node_conf.vm.box = box_debian
            node_conf.vm.box_url = box_debian_url
        else
            node_conf.vm.box = box_centos
            node_conf.vm.box_url = box_centos_url
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
        end

        # Shared folders
        node_conf.vm.synced_folder "../", "/var/www/#{project}", owner: "www-data", group: "www-data"

        # Package list initial update for Debian distros
        if linux_distro == 'debian' 
            apt_update = 'apt-get update'
            node_conf.vm.provision "shell", inline: apt_update
        end

        # Update www-data user shell to /bin/bash for Debian distros
        if linux_distro == 'debian' 
            update_user_shell = "usermod -s /bin/bash www-data"
            node_conf.vm.provision "shell", inline: update_user_shell
        end
    end
end
