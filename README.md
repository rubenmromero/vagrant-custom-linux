# Vagrant-Custom-Linux

Customizable Vagrantfile to start and provision Debian & CentOS VMs based on VirtualBox provider.

## Prerequisites

* Vagrant 1.7.4+ => [Download Vagrant](https://www.vagrantup.com/downloads.html)
* VirtualBox 5.0.2+ => [Download VirtualBox](https://www.virtualbox.org/wiki/Downloads)

## Configuration

1. Clone this repo into the root folder of your project and add the resulting `vagrant` folder to your project's `.gitignore` file:

       $ git clone https://github.com/rubenmromero/vagrant-custom-linux.git vagrant
       $ echo '/vagrant/' >>.gitignore
       $ git commit -m "Update '.gitignore' file" .gitignore

2. Change to the `vagrant` folder and install the `vagrant-vbguest` Vagrant plugin:

       $ cd vagrant
       $ vagrant plugin install vagrant-vbguest

2. Create a copy of [`config.yml.dist`](config.yml.dist) template named `config.yml`, edit the new file and set the Vagrant environment configuration replacing the existing `<tags>` by the appropriate values:

       # From the vagrant folder
       $ cp -p config.yml.dist config.yml
       $ vi config.yml

## Execution Method

Once set up the Vagrant environment configuration in the `config.yml` file, simply run the following command from the `vagrant` folder:

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
