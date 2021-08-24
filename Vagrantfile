Vagrant.configure(2) do |config|
  config.vm.box = "generic/rhel8"
  config.vm.hostname = "simplerhel"
  config.vm.provision "ansible" do |a|
    a.playbook = "simple_rhel.yml"
    a.verbose = "v"
  end
  # Grab the name of the default interface
  $default_network_interface = `ip route | awk '/^default/ {printf "%s", $5; exit 0}'`
  config.vm.network "public_network", bridge: "#$default_network_interface",
    use_dhcp_assigned_default_route: true
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end
end 
