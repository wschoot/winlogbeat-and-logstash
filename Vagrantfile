# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.provider :libvirt do |vb|
    vb.memory = 4096
    vb.cpus = 2
  end

  # Q: winrm or requests is not installed: No module named winrm
  # A: pip install "pywinrm>=0.2.2"
  config.vm.define "windows" do |windows|
    windows.vm.box = "peru/windows-10-enterprise-x64-eval"
    windows.vm.hostname = "windows"
    windows.vm.provision :ansible do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.host_vars = {
        "windows" => { "connection" => "winrm",}
      }
      ansible.compatibility_mode = "2.0"
      ansible.limit = "all"
    end
  end

  config.vm.define "linux" do |linux|
    linux.vm.box = "centos/7"
    linux.vm.hostname = "linux"
  end

end
