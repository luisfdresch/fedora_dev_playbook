Vagrant.configure("2") do |config|
  # Fedora vm
    config.vm.define "fedora_vm" do |app|
        app.vm.box = "fedora/39-cloud-base"
        app.vm.box_version = "39.20231031.1"

        app.ssh.insert_key = false

        app.vm.synced_folder ".", "/vagrant", disabled: true

        app.vm.provider :libvirt do |v|
            v.qemu_use_session = false
            v.memory = 2048
            v.cpus = 2
          end

        app.vm.provision "shell", inline: <<-SHELL
            nmcli conn modify 'Wired connection 2' ipv4.addresses $(cat /etc/sysconfig/network-scripts/ifcfg-eth1 | grep IPADDR | cut -d "=" -f2)
            nmcli conn modify 'Wired connection 2' ipv4.method manual
            service NetworkManager restart
          SHELL
        app.vm.hostname = "fedora-vm.test"
        app.vm.network :'private_network', ip: "192.168.121.4"
    end
end
