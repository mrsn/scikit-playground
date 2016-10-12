# -*- mode: ruby -*-
# vi: set ft=ruby :

$install_scikit = <<SCRIPT

yum install yum-utils -y
yum install groupinstall development -y

yum install https://centos7.iuscommunity.org/ius-release.rpm -y 
yum install python35u-3.5.2 -y

yum install python35u-pip -y

SCRIPT

Vagrant.configure('2') do |config|
  config.ssh.insert_key = false

  box_name = 'opscode_centos-7.2_chef-provisionerless'
  config.vm.box = box_name
  config.vm.box_url = 'https://opscode-vm-bento.s3.amazonaws.com/' \
  "vagrant/virtualbox/#{box_name}.box"

  config.vm.define 'server_1' do |server_1|
    server_1.vm.network :private_network, ip: '192.168.33.100'

    server_1.vm.provider :virtualbox do |vb|
      vb.customize ['modifyvm', :id, '--memory', '4096']
      vb.customize ["modifyvm", :id, "--cpus", 4] 
    end

    server_1.vm.provision 'shell', inline: $install_scikit
  end
end
