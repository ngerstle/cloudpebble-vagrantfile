include_vagrantfile = File.expand_path("../include/_Vagrantfile", __FILE__)
load include_vagrantfile if File.exist?(include_vagrantfile)

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.network "forwarded_port", guest: 80, host:8080, protocol: "tcp"
  config.vm.network "forwarded_port", guest: 80, host:8080, protocol: "udp"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "cloudpebble"
    vb.memory = 2048
    vb.cpus = 2
  end






  # provision the vagrantbox!!

  $provisioningscript = <<SCRIPT
cd /home/ubuntu/
sudo apt-get remove docker docker-engine docker.io
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce
sudo docker run hello-world
sudo apt-get install docker-compose -y
sudo apt remove nodejs npm
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs

git clone https://github.com/ltpitt/vagrant-cloudpebble-composed.git cloudpebble-composed
cd cloudpebble-composed
git clone https://github.com/ltpitt/cloudpebble.git
git clone https://github.com/ltpitt/cloudpebble-qemu-controller.git
git clone https://github.com/ltpitt/cloudpebble-ycmd-proxy.git
cd cloudpebble/ext
git clone https://github.com/pebble/pebblejs.git


cd /home/ubuntu/cloudpebble-composed
# Change in cloudpebble-composed\docker-compose.yml IP addess to address of your Docker install by default 172.17.0.1
sed -i 's/10.0.2.15/172.17.0.1/g' docker-compose.yml
# Change in cloudpebble-qemu-controller\Dockerfile ENV FIRMWARE_VERSION 3.11 replace with ENV FIRMWARE_VERSION 4.3
sed -i 's/ENV FIRMWARE_VERSION 3.11/ENV FIRMWARE_VERSION 4.3/g' cloudpebble-qemu-controller
# Then open a terminal and cd to cloudpebble-composed dir.

#TODO need to update node version, nodejs gpg keys?
sudo ./dev_setup.sh
SCRIPT



  # Always run docker-compose up on vagrant up
  config.vm.provision "shell", run: "always" do |s|
    s.inline = "sudo docker-compose -f /home/ubuntu/pebblecloud/docker-compose.yml up -d"
  end



end
