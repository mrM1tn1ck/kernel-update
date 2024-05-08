# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'

MACHINES = {
  :"kernel-update" => {
    :box_name => "ubuntu/jammy64",
    :cpus => 1,
    :memory => 4096,
    :ip_addr => "192.168.10.10",
  }
}

$script = <<SCRIPT
sudo su
export DEBIAN_FRONTEND=noninteractive
apt-get update && apt-get upgrade -y
apt-get install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex bison libelf-dev -y
cd /usr/src/
wget -O linux-kernel.tar.xz https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.8.9.tar.xz
tar -xvf linux-kernel.tar.xz
reboot
SCRIPT

Vagrant.configure("2") do |config|
  MACHINES.each do |boxname, boxconfig|

    config.vm.provision "shell", inline: $script
    # config.trigger.after [:provision] do |t|
    #   t.name = "Reboot after provisioning"
    #   t.run = { :inline => "vagrant reload" }
    # end
    config.vm.synced_folder ".", "/vagrant/", disabled: false
    config.vm.define boxname do |srv|
      srv.vm.box = boxconfig[:box_name]
      srv.vm.host_name = boxname.to_s
      srv.vm.network("private_network", ip: boxconfig[:ip_addr])
      srv.vm.provider "virtualbox" do |vb|
        vb.memory = boxconfig[:memory]
        vb.cpus = boxconfig[:cpus]
      end
    end
  end
end
