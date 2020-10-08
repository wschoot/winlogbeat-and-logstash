# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.provider :libvirt do |vb|
    vb.memory = 8192
    vb.cpus = 2
  end

  # Q: winrm or requests is not installed: No module named winrm
  # A: pip install "pywinrm>=0.2.2"
  config.vm.define "win1" do |win1|
    win1.vm.box = "peru/windows-10-enterprise-x64-eval"
    win1.vm.hostname = "win1"
    win1.vm.guest = :windows
    win1.vm.boot_timeout = 60
    win1.windows.halt_timeout = 60
    win1.vm.communicator = "winrm"
  end

  config.vm.define "win2" do |win2|
    win2.vm.box = "peru/windows-10-enterprise-x64-eval"
    win2.vm.hostname = "win2"
    win2.vm.guest = :windows
    win2.vm.boot_timeout = 60
    win2.windows.halt_timeout = 60
    win2.vm.communicator = "winrm"
    win2.vm.provision :ansible do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.host_vars = {
        "win2" => { "connection" => "winrm",}
      }
      ansible.compatibility_mode = "2.0"
      ansible.limit = "all"
    end
  end

  config.vm.define "linux" do |linux|
    linux.vm.box = "centos/7"
    linux.vm.hostname = "linux"
    linux.vm.network "forwarded_port", guest: 5601, host: 5601
  end

end
