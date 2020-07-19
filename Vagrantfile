Vagrant.configure("2") do |config|
    config.vm.provision "shell", inline: "echo before app machines"

    machines = [
        {
          :hostname => "lb.vm",
          :ip => "10.250.0.10"
        },
        {
            :hostname => "app1.vm",
            :ip => "10.250.0.100"
        },
        {
            :hostname => "app2.vm",
            :ip => "10.250.0.101"
        }
    ]
  
    machines.each do |machine|
      config.vm.define machine[:hostname] do |app|
        app.vm.box = "centos/7"
        app.vm.provider "virtualbox" do |v|
          v.memory = 512
          v.cpus = 1
          v.linked_clone = true
        end
        app.vm.hostname = machine[:hostname]
        app.vm.network "private_network", ip: machine[:ip]
        app.vm.provision :shell, inline: "/usr/bin/hostname && /usr/sbin/ip addr"
        if machine[:hostname] == "app2.vm"
          app.vm.provision :ansible do |ansible|
            # Disable default limit to connect to all the machines
            ansible.limit = "all"
            # ansible.verbose = "-v"
            ansible.groups = {
              "loadbalancer" => ["lb.vm"],
              "demoapp" => ["app1.vm","app2.vm"]
            }
            ansible.playbook = "target/playbooks/main-play.yml"
          end
        end
      end
    end

    config.vm.provision "shell", inline: "echo after app machines"
  end