Vagrant.configure("2") do |config|
    config.vm.provision "shell", inline: "echo before app machines"
  
    (1..2).each do |i|
      config.vm.define "app#{i}" do |app|
        app.vm.box = "centos/7"
        app.vm.hostname = "app#{i}.vm"
        app.vm.network "private_network", type: "dhcp"
        app.vm.provision :shell, inline: "/usr/bin/hostname && /usr/sbin/ip addr"
      end
    end

    # config.vm.define "app1" do |app1|
    #   app1.vm.box = "centos/7"
    #   app1.vm.network "private_network", type: "dhcp"
    #   app1.vm.provision :shell, inline: "/usr/bin/hostname && /usr/sbin/ip addr"
    # end
  
    # config.vm.define "app2" do |app2|
    #   app2.vm.box = "centos/7"
    #   app2.vm.network "private_network", type: "dhcp"
    #   app2.vm.provision :shell, inline: "/usr/bin/hostname && /usr/sbin/ip addr"
    # end

    config.vm.provision "shell", inline: "echo after app machines"
  end