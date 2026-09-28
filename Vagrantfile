Vagrant.configure("2") do |config|

  # Rocky Linux 8
  config.vm.box = "rockylinux/8"

  # Hostname
  config.vm.hostname = "postgres-vm"

  # Fixed private IP for PuTTY / PostgreSQL access
  config.vm.network "private_network", ip: "192.168.56.10"

  # VMware settings
  config.vm.provider "vmware_workstation" do |v|
    v.gui = true
    v.vmx["memsize"] = "4096"
    v.vmx["numvcpus"] = "2"
  end

  # Provisioning
  config.vm.provision "shell", inline: <<-SHELL

    echo "===== Updating OS ====="
    dnf update -y

    echo "===== Setting root password ====="
    echo 'root:welcome1' | chpasswd

    echo "===== Configuring SSH for PuTTY ====="

    # Remove/replace any existing PasswordAuthentication setting
    sed -i 's/^PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config

    # Ensure root login is enabled
    if grep -q '^PermitRootLogin' /etc/ssh/sshd_config; then
      sed -i 's/^PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config
    else
      echo 'PermitRootLogin yes' >> /etc/ssh/sshd_config
    fi

    # Ensure password authentication exists
    if ! grep -q '^PasswordAuthentication yes' /etc/ssh/sshd_config; then
      echo 'PasswordAuthentication yes' >> /etc/ssh/sshd_config
    fi

    # Validate SSH configuration
    sshd -t

    # Restart SSH
    systemctl restart sshd

    echo "===== Configuration complete ====="

  SHELL
end