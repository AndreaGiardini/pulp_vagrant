$setup_script = <<EOF
sudo yum install -y git python-mongoengine
git clone https://github.com/AndreaGiardini/pulp
cd pulp/playpen
sudo chmod +x dev-setup.sh
echo 'y' | sudo -u vagrant ./dev-setup.sh
EOF

Vagrant.configure("2") do |config|
#config.ssh.pty= true
  config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "2048"]
  end

  config.vm.box = "fedora_20.box"
  config.vm.box_url = "https://vagrantcloud.com/jwmatthews/fedora_20/version/0.1.0/provider/virtualbox.box"
  #config.vm.synced_folder "/home/andrea/pulp_dev", "/home/vagrant", owner: "vagrant", group: "vagrant"


  config.vm.define "pulpserver" do |pulpserver|
    pulpserver.vm.hostname = "pulpserver.example.com"
    pulpserver.vm.network :private_network, ip: "172.31.2.100"
    pulpserver.vm.provision :shell, :inline => $setup_script
  end

end
