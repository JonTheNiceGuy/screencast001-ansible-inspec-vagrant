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


  # This starts the ansible privisioner inside the virtual machine
  config.vm.provision "ansible_local" do |a|
    # This defines the Ansible playbook to run
    a.playbook = "ansible.yml"
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

    # This starts a shell provisioner inside the virtual machine
    sc01.vm.provision "shell" do |shell|
      # This defines the commands we will run
      shell.inline = <<-EOF
        if [ -z "$(which inspec)" ]
        then
          curl https://omnitruck.chef.io/install.sh | bash -s -- -P inspec # Consider using wget and confirming the script does what you want!
          inspec --chef-license=accept-silent nothing >/dev/null 2>/dev/null # This is for personal use only. ACCEPT EULA FOR YOURSELF FIRST
        fi
      EOF
    end

    # This starts a shell provisioner on every boot inside the virtual machine
    sc01.vm.provision "shell", run: "always" do |shell|
      # This is the command to run
      shell.inline = "inspec exec /vagrant/inspec.rb"
    end
  end
end
