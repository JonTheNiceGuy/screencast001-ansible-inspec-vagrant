Vagrant.configure("2") do |config|
  # This defines the box image we're going to use
  config.vm.box = "ubuntu/bionic64"

  # This defines virtualbox changes to apply to all VMs
  config.vm.provider "virtualbox" do |vb|
    # This asks Virtualbox to use linked clones instead of importing box files each time.
    vb.linked_clone = true
  end

  # Check to see if Vagrant has the "cachier" plugin
  if Vagrant.has_plugin?("vagrant-cachier")
    # If so, ask it to retain all the package caches at a "box" level.
    config.cache.scope = :box
  end

  # This defines the name that Vagrant knows this machine as
  config.vm.define "sc01" do |sc01|
    # This defines what the virtual machine knows itself as
    sc01.vm.hostname = "sc01"
    # Here we set some options for Virtualbox
    sc01.vm.provider "virtualbox" do |vb|
      # This defines what Virtualbox knows this machine as
      vb.name = "sc01"
    end

    sc01.vm.provision "ansible_local" do |a|
      a.playbook = "ansible.yml"
    end
  end
end
