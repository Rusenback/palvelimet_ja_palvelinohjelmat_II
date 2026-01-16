
$update_script = <<-SCRIPT 
  apt-get update
  apt-get upgrade -y
SCRIPT


Vagrant.configure("2") do |config|
  #Pohja molemmille koneille
  config.vm.box = "bento/ubuntu-24.04"

  #Ensimmäinen VM
  config.vm.define "server1" do |server1|
    server1.vm.hostname = "server1"

    #Host-only verkko
    server1.vm.network "private_network", ip: "192.168.56.10"

    server1.vm.provider "virtualbox" do |vb|
      vb.name = "labra.server1"
      vb.memory = "2048"
      vb.cpus = 2 
    end

    server1.vm.provision "shell", inline: $update_script
  end  
  #Toinen VM
  config.vm.define "server2" do |server2|
    server2.vm.hostname = "server2"

    #Host-only verkko
    server2.vm.network "private_network", ip: "192.168.56.11"

    server2.vm.provider "virtualbox" do |vb|
      vb.name = "labra.server2"
      vb.memory = "2048"
      vb.cpus = 2 
    end
    server2.vm.provision "shell", inline:  $update_script
  end
end




