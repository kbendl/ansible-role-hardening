Vagrant.configure("2") do |ubuxen|
  ubuxen.vm.box = "ubuntu/xenial64"

  ubuxen.vm.provider "virtualbox" do |uvb|
    uvb.memory = "2048"
    uvb.name = "ubuxen"
  end

  ubuxen.vm.define "ubuxen" do |ubuxen|
    ubuxen.ssh.insert_key = true
    ubuxen.vm.network "private_network", ip:"10.2.3.41"
    ubuxen.vm.hostname = "ubuxen"
    ubuxen.vm.provision "shell",
      inline: "apt-get update && apt-get -y install ansible aptitude python --no-install-recommends"
    ubuxen.vm.provision "ansible" do |p|
      p.verbose = "v"
      p.limit = "all"
      p.playbook = "hardening-test.yml"
      p.extra_vars = {
        "sshd_admin_net" => "0.0.0.0/0"
      }
    end
  end
end

Vagrant.configure("2") do |censev|
  censev.vm.box = "centos/7"

  censev.vm.provider "virtualbox" do |cvb|
    cvb.memory = "2048"
    cvb.name = "censev"
  end

  censev.vm.define "censev" do |censev|
    censev.ssh.insert_key = true
    censev.vm.network "private_network", ip:"10.2.3.42"
    censev.vm.hostname = "censev"
    censev.vm.provision "ansible" do |p|
      p.verbose = "v"
      p.limit = "all"
      p.playbook = "hardening-test.yml"
      p.extra_vars = {
        "sshd_admin_net" => "0.0.0.0/0",
        "ssh_allow_groups" => "vagrant"
      }
    end
  end
end
