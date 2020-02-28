Vagrant.configure("2") do |config|
  # This defines the box image we're going to use
  config.vm.box = "ubuntu/bionic64"

  # This defines the name that Vagrant knows this machine as
  config.vm.define "sc01" do |sc01|
    # This defines what the virtual machine knows itself as
    sc01.vm.hostname = "sc01"
    # Here we set some options for Virtualbox
    sc01.vm.provider "virtualbox" do |vb|
      # This defines what Virtualbox knows this machine as
      vb.name = "sc01"
    end
  end
end
