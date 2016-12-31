Vagrant.configure(2) do |config|
  config.vm.box = "centos71"
  config.vm.box_url = "https://github.com/holms/vagrant-centos7-box/releases/download/7.1.1503.001/CentOS-7.1.1503-x86_64-netboot.box"

  # Please set arbitrary ip
  config.vm.network "private_network", ip: "192.168.100.111"

  # provision by shell
  config.vm.provision "shell", inline: <<-SHELL
    # key import
    sudo rpm --import http://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7

    # install rpm
    sudo rpm -Uvh http://ftp.iij.ad.jp/pub/linux/fedora/epel/7/x86_64/e/epel-release-7-8.noarch.rpm

    # install ansible
    sudo yum -y install ansible

    # ansible for local
    sudo echo 'localhost ansible_connection=local' >> /etc/ansible/hosts

    # ansible not create retry file
    sudo sed -i 's/#retry_files_enabled = False/retry_files_enabled = False/g' /etc/ansible/ansible.cfg

    # ansible playbook
    sudo ansible-playbook /vagrant/ansible/playbook.yml
  SHELL
end
