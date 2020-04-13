# Vagrant-Custom-Linux

Customizable Vagrantfile to start and provision Debian & CentOS VMs based on VirtualBox provider.

## Prerequisites

* Vagrant 1.7.4+ => [Download Vagrant](https://www.vagrantup.com/downloads.html)
* VirtualBox 5.0.2+ => [Download VirtualBox](https://www.virtualbox.org/wiki/Downloads)

## Configuration

1. Download the Vagrant-Custom-Linux code into the root folder of your project:

       $ git clone https://github.com/rubenmromero/vagrant-custom-linux.git

2. Install the `vagrant-vbguest` Vagrant plugin:

       $ vagrant plugin install vagrant-vbguest

2. Create a copy of [config.yml.dist](config.yml.dist) template to `config.yml`, edit the new file and set the Vagrant environment configuration replacing the existing `<tags>` with the appropiate values:

       # From the folder that contains the Vagrantfile
       $ cp -p config.yml.dist config.yml
       $ vi config.yml

## Execution Method

Once configured the Vagrant environment configuration into `config.yml` file, simply run the following command:

    $ vagrant up

If you need some help with the Vagrant utility, you can get it by executing the following command:

    $ vagrant --help

## Troubleshooting

* [Fix network problem in CentOS](https://unix.stackexchange.com/questions/315591/centos-7-disable-predictable-network-interface-names-with-packer-vagrant)

## Related Links

* [dotless-de/vagrant-vbguest - GitHub](https://github.com/dotless-de/vagrant-vbguest)
* [Discover Vagrant Boxes](https://app.vagrantup.com/boxes/search)
* [Vagrant Documentation](https://www.vagrantup.com/docs/index.html)
* [VirtualBox Documentation](https://www.virtualbox.org/wiki/Documentation)
