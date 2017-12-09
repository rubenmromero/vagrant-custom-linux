# Vagrant-Custom-Linux

Customizable Vagrantfile to start and provision Debian & CentOS VMs based on VirtualBox provider.

## Prerequisites

* Vagrant 1.7.4+
* VirtualBox 5.0.2+

## Configuration

1. Download the Vagrant-Custom-Linux code into the root folder of your project:

       $ git clone https://github.com/rubenmromero/vagrant-custom-linux.git

2. Create a copy of [config.yml.dist](config.yml.dist) template to `config.yml`, edit the new file and set the Vagrant environment configuration replacing the existing `<tags>` with the appropiate values:

       # From the folder that contains the Vagrantfile
       $ cp -p config.yml.dist config.yml
       $ vi config.yml

## Execution Method

Once configured the Vagrant environment configuration into `config.yml` file, simply run the following command:

    $ vagrant up

If you need some help with the Vagrant utility, you can get it by executing the following command:

    $ vagrant --help

## Related Links

* [Vagrant Documentation](https://www.vagrantup.com/docs/index.html)
* [VirtualBox Documentation](https://www.virtualbox.org/wiki/Documentation)
