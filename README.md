# simple_ansible
A project the demonstrates how to create a virtual machine under VirtualBox using Vagrant and then provision that virtual machine using Ansible.

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


# Destroying the Virtual Machine

After you've run the VM created and provisioned by Vagrant and Ansible, you can destroy it by executing the following command.

`vagrant destroy`

Again, depending on how you configured your installation of Vagrant, you might have to use `sudo` when executing the command set shown above.

**Make sure you execute**, `vagrant destroy` from within the same directory that contains the Vagrantfile that you cloned down onto the host computer.



