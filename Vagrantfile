# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "coreos-stable"

  # config.vm.box_check_update = false

  config.vm.network "private_network", type: "dhcp"
  config.landrush.enabled = true
  config.landrush.tld = 'vagrant.local'

    component2port = {
      "apiserver" => 80,
      "etcd" => 2379,
      "vault" => 8001
    }

      component = "apiserver"

      port = component2port[component]

      config.vm.define "%s-lb" % component do |lb|
            lb.vm.hostname = "%s-lb.vagrant.local" % component
            lb.vm.provision "file", source: "%s/nginx.conf" % component, destination: "/tmp/nginx.conf"
            # lb.provision "shell",
            #   inline "echo CONFIG | base64 -d | gzip -d > /tmp/nginx.conf"
            lb.vm.provision "shell", inline: ( "docker run -d -p %{port}:%{port} --net=host --privileged --name nginx --restart always -v /tmp/nginx.conf:/etc/nginx/nginx.conf nginx" % {:port => port})
            lb.vm.provider "virtualbox" do |v|
                v.memory = 256
                v.cpus = 1
            end
      end

      (1..3).each do |i|
        config.vm.define "%{c}-%{i}" % {:c => component, :i => i} do |target|
            target.vm.hostname = "%{c}-%{i}.vagrant.local" % {:c => component, :i => i}
            target.vm.provision "shell", inline: ( "docker run -d -p %{port}:%{port} --name nginx --restart always nginx" % {:port => port})
            target.vm.provider "virtualbox" do |v|
                v.memory = 512
                v.cpus = 1
            end
        end
      end

end
