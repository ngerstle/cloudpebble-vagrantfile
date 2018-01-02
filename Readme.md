# What is this:
A vagrant file and script to set up cloudpebble per https://github.com/ltpitt/vagrant-cloudpebble-composed.

# Intro

I have no interest in maintaining this, nor do I have a pebble or intend to run the server. Putting a complete vagrant file
with inline provisioning is done as a learning exercise and a favor to my mother.

# To use:
- install vagrant
- clone this repo
- run `$ vagrant up`
- go to `localhost:8080` in a browser.

# Changing/info

The port forwarding and VM allocations (memory, CPU, etc) are done in `config.vm.provider "virtualbox"` section. This will need to be redone for providers other than virtualbox.

Note: the whole process can take quite a while to built. It may randomly fail due to different repositories timing out. I have no idea what is being compiled and done in each of the docker containers running in the vagrant box. Use at your own risk, and don't expost to the internet as a whole.
