# -*- mode: ruby -*-
# # vi: set ft=ruby :
# A script to install docker.
$script = <<SCRIPT
# The username to add to the docker group will be passed as the first argument
# to the script.  If nothing is passed, default to "vagrant".
user="$1"
if [ -z "$user" ]; then
    user=vagrant
fi

touch /etc/default/docker

if ! grep -q 'DOCKER_OPTS' "/etc/default/docker" ; then
  echo 'DOCKER_OPTS="-H=unix:///var/run/docker.sock -H tcp://0.0.0.0:5555"' >> "/etc/default/docker"
fi

# Adding an apt gpg key is idempotent.
wget -q -O - https://get.docker.io/gpg | apt-key add -

# Creating the docker.list file is idempotent, but it may overwrite desired
# settings if it already exists.  This could be solved with md5sum but it
# doesn't seem worth it.
echo 'deb http://get.docker.io/ubuntu docker main' > \
    /etc/apt/sources.list.d/docker.list

# Update remote package metadata.  'apt-get update' is idempotent.
apt-get update -q

# Install docker.  'apt-get install' is idempotent.
apt-get install -q -y lxc-docker

usermod -a -G docker "$user"

SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "https://oss-binaries.phusionpassenger.com/vagrant/boxes/ubuntu-12.04.3-amd64-vbox.box"

  config.ssh.forward_agent = true
  config.vm.network :forwarded_port, guest: 5555, host: 5555
  config.vm.network :forwarded_port, guest: 8000, host: 8000
  config.vm.provision :shell, :inline => $script

  config.vm.provider :virtualbox do |vb|
    vb.customize ['modifyvm', :id, '--memory', ENV['VM_MEMORY'] || 1024]
    vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
    vb.customize ['modifyvm', :id, '--natdnsproxy1', 'on']
  end
end
