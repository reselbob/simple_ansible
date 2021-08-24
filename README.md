
# `simple_ansible`
A project that demonstrates how to create a virtual machine under [VirtualBox](https://www.virtualbox.org/) using [Vagrant](https://www.vagrantup.com/intro) and then provision that virtual machine using [Ansible](https://www.ansible.com/).


- [`simple_ansible`](#simple_ansible)
- [Prerequisites](#prerequisites)
  - [Installing VirtualBox](#installing-virtualbox)
    - [Linux Installation](#linux-installation)
    - [MACOS  and Windows Installation](#macos--and-windows-installation)
  - [Installing Vagrant](#installing-vagrant)
  - [Installing Ansible](#installing-ansible)
- [Creating and provisioning the virtual machine](#creating-and-provisioning-the-virtual-machine)
- [Accessing the Virtual Machine](#accessing-the-virtual-machine)
- [Destroying the Virtual Machine](#destroying-the-virtual-machine)

# Prerequisites

In order to get the code up and running you need have Ansible, Vagrant, VirtualBox installed on your working machine.

## Installing VirtualBox

If you don't have VirtualBox installed on your local system, install it using the instructions listed below.

### Linux Installation

To install VirtualBox on a Linux host, execute the following commands in a terminal window:

`sudo apt-get update`

`sudo apt-get install virtualbox -y`

`sudo apt-get install virtualbox—ext–pack -y`

### MACOS  and Windows Installation

To install VirtualBox on MacOS or Windows, download the operating specific installer from the VirtualBox site found [here](https://www.virtualbox.org/wiki/Downloads).

## Installing Vagrant

You'll find the instruction for installing Vagrant on a host machine at the Vagrant web site, [here](https://www.vagrantup.com/docs/installation).

## Installing Ansible

You can find the instructions for installing Ansible on a Linux or MacOS machine on the Ansible web site, [here](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

Ansible is not supported as a controller under Windows.
# Creating and provisioning the virtual machine

Once you have all the prerequisites installed on the host system to run Vagrant and Ansible, in order to get the project up and running you need to clone this code onto the host system. 

To clone this code onto the host system, execute the following commands from a terminal window:

`git clone https://github.com/reselbob/simple_ansible.git`

Then, navigate tot he working directory:

`cd simple_ansible`

Finally, invoke the code in the Vagrantfile by executing the following command:

`vagrant up`

The command set, `vagrant up` will create a `RHEL 8` virtual machine as defined in the Vagrant file. In turn the Vagrantfile will call the accompanying Ansible Playbook, [`simple_rhel.yaml`](simple_rhel.yml) to provision the newly created virtual machine with the utilities, [`bash-completion`](https://github.com/scop/bash-completion), [`vim`](https://www.vim.org/) and [`nmon`](http://nmon.sourceforge.net/pmwiki.php). Also, the Ansible Playbook will create the user, `cooluser` on the VM and assign that user the password, `Password1`.

The VM you'll create supports bridged networking and will be assigned an IP address dynamically using the your network's DHCP server.

Depending on how you configured your installation of Vagrant, you might have to use `sudo` when executing the command set shown above.

# Accessing the Virtual Machine

To access the virtual machine, execute the following command:

`vagrant ssh`

You'll be taken into a terminal window within the virtual machine you've just created.

Once in the VM you can execute the following command get the current IP address assigned by the DHCP server,

`ipconfig`

You'll get output similar to the following:

```

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.2.15  netmask 255.255.255.0  broadcast 10.0.2.255
        ether 08:00:27:c3:d3:03  txqueuelen 1000  (Ethernet)
        RX packets 10701  bytes 13712477 (13.0 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 4148  bytes 380142 (371.2 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.86.42  netmask 255.255.255.0  broadcast 192.168.86.255
        inet6 fe80::a00:27ff:fe07:524f  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:07:52:4f  txqueuelen 1000  (Ethernet)
        RX packets 16884  bytes 4810905 (4.5 MiB)
        RX errors 0  dropped 2  overruns 0  frame 0
        TX packets 308  bytes 20352 (19.8 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```

**WHERE** in this case, `inet 192.168.86.42` indicates the IP address of the virtual machine

You can `ping` the VM from an external machine within your network by using the IP address you've just discovered, like so:

`ping 192.168.86.42`

You'll get output similar to the following

```
PING 192.168.86.42 (192.168.86.42): 56 data bytes
64 bytes from 192.168.86.42: icmp_seq=0 ttl=64 time=1.251 ms
64 bytes from 192.168.86.42: icmp_seq=1 ttl=64 time=0.777 ms
64 bytes from 192.168.86.42: icmp_seq=2 ttl=64 time=0.826 ms
64 bytes from 192.168.86.42: icmp_seq=3 ttl=64 time=0.807 ms
64 bytes from 192.168.86.42: icmp_seq=4 ttl=64 time=0.761 ms
64 bytes from 192.168.86.42: icmp_seq=5 ttl=64 time=0.708 ms
64 bytes from 192.168.86.42: icmp_seq=6 ttl=64 time=0.640 ms

```
# Destroying the Virtual Machine

After you've run the VM created and provisioned by Vagrant and Ansible, you can destroy it by executing the following command.

`vagrant destroy`

Again, depending on how you configured your installation of Vagrant, you might have to use `sudo` when executing the command set shown above.

**Make sure you execute**, `vagrant destroy` from within the same directory that contains the Vagrantfile that you cloned down onto the host computer.





