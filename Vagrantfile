include_vagrantfile = File.expand_path("../include/_Vagrantfile", __FILE__)
load include_vagrantfile if File.exist?(include_vagrantfile)

Vagrant.configure("2") do |config|
  config.vm.base_mac = "00010020003"
  config.ssh.username = "ubuntu"
  config.ssh.password = ""

  config.vm.network "forwarded_port", guest: 80, host:8080, protocol: "tcp"
  config.vm.network "forwarded_port", guest: 80, host:8080, protocol: "udp"

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--uart1","0x3F8",4]
    vb.customize ["modifyvm", :id, "--uartmode1", "file", File.join(Dir.pwd, "ubuntu-xenial-16.04-cloudimg-console.log")]
  end

end
