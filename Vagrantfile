
$update_script = <<-SCRIPT 
  apt-get update
  apt-get upgrade -y
SCRIPT


Vagrant.configure("2") do |config|
  #Base for both VMs
  config.vm.box = "bento/ubuntu-24.04"

  # SSH timeout settings to prevent hanging
  config.vm.boot_timeout = 180
  config.ssh.connect_timeout = 30
  config.ssh.forward_agent = true
  config.ssh.forward_x11 = false
  
  # Prevent TTY issues 
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

  #First VM
  config.vm.define "vm1" do |vm1|
    vm1.vm.hostname = "vm1"

    #Host-only netowrk
    vm1.vm.network "private_network", ip: "192.168.56.10"

    vm1.vm.provider "virtualbox" do |vb|
      vb.name = "labra.vm1"
      vb.memory = "2048"
      vb.cpus = 2 

      # VirtualBox specific optimizations
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      vb.customize ["modifyvm", :id, "--uart1", "0x3F8", "4"]
      vb.customize ["modifyvm", :id, "--uartmode1", "file", File::NULL]
    end

    vm1.vm.provision "shell", inline: $update_script
  end  
  #Second VM
  config.vm.define "vm2" do |vm2|
    vm2.vm.hostname = "vm2"

    #Host-only network 
    vm2.vm.network "private_network", ip: "192.168.56.11"

    vm2.vm.provider "virtualbox" do |vb|
      vb.name = "labra.vm2"
      vb.memory = "2048"
      vb.cpus = 2 

      # VirtualBox specific optimizations
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      vb.customize ["modifyvm", :id, "--uart1", "0x3F8", "4"]
      vb.customize ["modifyvm", :id, "--uartmode1", "file", File::NULL]
    end
    vm2.vm.provision "shell", inline:  $update_script
  end
end




