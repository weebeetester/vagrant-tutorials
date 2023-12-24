# Overview

Vagrant is a source-available software product for building and maintaining portable virtual software development environments; e.g., for VirtualBox, KVM, Hyper-V, Docker containers, VMware, Parallels, and AWS. It tries to simplify the software configuration management of virtualization in order to increase development productivity.


# Installation
These installation steps may vary for different OS. Rest of the sections (apart from installation) will be same regardless of OS.

## Install Vagrant

Download & install vagrant from https://developer.hashicorp.com/vagrant/install. 


## Check installed vagrant version
```bash
>vagrant --version
Vagrant 2.4.0
```

## Install/Select a VM Provider
### Vagrant has direct support for VirtualBox, KVM, Hyper-V, others.
### We will use virtualbox. Download (https://www.virtualbox.org/wiki/Downloads) & Install virtualbox (if not already done),  verify installation.
```bash
>vboxmanage --version
7.0.12r159484
```


# Create Vagrant box for Ubuntu22LTS

### This section describes setting up vagrant box for ubuntu (https://app.vagrantup.com/ubuntu/boxes/jammy64)

## Create dedicated folder for this box (ubuntu22)
```bash
 >mkdir ubuntu22
 >cd ubuntu22
 ubuntu22 
```
## Initialize (will create a Vagrantfile in this folder)
### Vagrant box for ubuntu 22 LTS can be found at https://app.vagrantup.com/ubuntu/boxes/jammy64

```bash
 ubuntu22  vagrant init ubuntu/jammy64
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
```

### Notice there's a Vagrantfile (written in Ruby) created in this folder
#### Property config.vm.box in below file points to the exact vm box we have requested
##### config.vm.box = "ubuntu/jammy64"

##### Here's the full file
```bash
>cat Vagrantfile

# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/jammy64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Disable the default share of the current code directory. Doing this
  # provides improved isolation between the vagrant box and your host
  # by making sure your Vagrantfile isn't accessable to the vagrant box.
  # If you use this you may want to enable additional shared subfolders as
  # shown above.
  # config.vm.synced_folder ".", "/vagrant", disabled: true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end

```

## Start virtual machine using >vagrant up
### This will download (if this is the first time) and start the virtual machine itself.

```bash
ubuntu22 > vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Box 'ubuntu/jammy64' could not be found. Attempting to find and install...
    default: Box Provider: virtualbox
    default: Box Version: >= 0
==> default: Loading metadata for box 'ubuntu/jammy64'
    default: URL: https://vagrantcloud.com/api/v2/vagrant/ubuntu/jammy64
==> default: Adding box 'ubuntu/jammy64' (v20231215.0.0) for provider: virtualbox
    default: Downloading: https://vagrantcloud.com/ubuntu/boxes/jammy64/versions/20231215.0.0/providers/virtualbox/unknown/vagrant.box
Download redirected to host: cloud-images.ubuntu.com
==> default: Successfully added box 'ubuntu/jammy64' (v20231215.0.0) for 'virtualbox'!
==> default: Importing base box 'ubuntu/jammy64'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'ubuntu/jammy64' version '20231215.0.0' is up to date...
==> default: Setting the name of the VM: ubuntu22_default_1703448502614_27267
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: Warning: Connection reset. Retrying...
    default:
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default:
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
    default: The guest additions on this VM do not match the installed version of
    default: VirtualBox! In most cases this is fine, but in rare cases it can
    default: prevent things such as shared folders from working properly. If you see
    default: shared folder errors, please make sure the guest additions within the
    default: virtual machine match the version of VirtualBox you have installed on
    default: your host and reload your VM.
    default:
    default: Guest Additions Version: 6.0.0 r127566
    default: VirtualBox Version: 7.0
==> default: Mounting shared folders...
    default: /vagrant => /Users/weebeetester/workspace/repositories/vagrant/ubuntu22
 ubuntu22 >

```


```bash

```

# List vagrant boxes
```bash
> vagrant box list
ubuntu/jammy64 (virtualbox, 20231215.0.0)
```

## Behind the scene, vagrant stores the boxes (including the downloaded file) at below location:
### MAC/Linux :  ˜/.vagrant.d/boxes
### Windows : C:/Users/USERNAME/.vagrant.d/boxes

## List name of machines(nodes)
### for a simple (single node) setup, the name of machine will be default.
```bash
> vagrant status
Current machine states:

default                   running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
```

# Connect to ubuntu machine using SSH
### https://developer.hashicorp.com/vagrant/docs/cli/ssh
This will SSH into a running Vagrant machine and give you access to a shell inside that machine.

```bash
> vagrant ssh
Welcome to Ubuntu 22.04.3 LTS (GNU/Linux 5.15.0-91-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sun Dec 24 20:23:10 UTC 2023

  System load:  0.0               Processes:               99
  Usage of /:   3.7% of 38.70GB   Users logged in:         0
  Memory usage: 21%               IPv4 address for enp0s3: 10.0.2.15
  Swap usage:   0%


Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

vagrant@ubuntu-jammy:~$
vagrant@ubuntu-jammy:~$ cat /etc/os-release
PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```


Now as you are in the ubuntu VM, you can work on (configure, download software, run apps) it as you would otherwise.

# Cleanup

## vagrant suspend / resume
### Suspends a machine (with all state preserved till that time) which will no longer use CPU &RAM (will still use disk space). You can resume it again at a later stage.A suspend effectively saves the exact point-in-time state of the machine, so that when you resume it later, it begins running immediately from that point, rather than doing a full boot.
### See more at https://developer.hashicorp.com/vagrant/docs/cli/suspend & https://developer.hashicorp.com/vagrant/docs/cli/resume

## vagrant halt
### Fully shuts down the machine
### See more at https://developer.hashicorp.com/vagrant/docs/cli/halt

## vagrant destroy
### This command stops the running machine Vagrant is managing and destroys all resources that were created during the machine creation process. After running this command, your computer should be left at a clean state, as if you never created the guest machine in the first place.
### See more at https://developer.hashicorp.com/vagrant/docs/cli/destroy

## See more at https://developer.hashicorp.com/vagrant/docs/cli

# Remove a box
## See more at https://developer.hashicorp.com/vagrant/docs/cli/box
>vagrant box remove box/name



