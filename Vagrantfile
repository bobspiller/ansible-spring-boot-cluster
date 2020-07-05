Vagrant.configure("2") do |config|
    config.vm.provision "shell", inline: "echo before app machines"

    machines = [
        {
            :hostname => "app1.vm",
            :ip => "10.250.0.2"
        },
        {
            :hostname => "app2.vm",
            :ip => "10.250.0.3"
        }
    ]
  
    machines.each do |machine|
      config.vm.define machine[:hostname] do |app|
        app.vm.box = "centos/7"
        app.vm.hostname = machine[:hostname]
        app.vm.network "private_network", ip: machine[:ip]
        app.vm.provision :shell, inline: "/usr/bin/hostname && /usr/sbin/ip addr"
      end
    end

    config.vm.provision "shell", inline: "echo after app machines"
  end