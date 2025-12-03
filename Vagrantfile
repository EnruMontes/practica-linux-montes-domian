# Vagrantfile para VirtualBox
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"
  config.vm.hostname = "linux-practice"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
    
    # Agregar disco adicional de 2GB para ejercicios de LVM
    unless File.exist?('./disk1.vdi')
      vb.customize ['createhd', '--filename', './disk1.vdi', '--size', 2048]
    end
    # Nota: El puerto 2 device 0 suele ser el secundario en el controlador SATA por defecto en Vagrant
    vb.customize ['storageattach', :id, '--storagectl', 'SCSI', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', './disk1.vdi']
  end

  config.vm.network "public_network"

  config.vm.provision "shell", inline: <<-SHELL
    # 1. Agregamos el repositorio para poder descargar fastfetch
    apt-get update
    apt-get install -y software-properties-common
    add-apt-repository -y ppa:zhangsongcui3371/fastfetch
    apt-get update

    # 2. Ahora sí instalamos todo
    apt-get install -y fastfetch git docker.io docker-compose lvm2

    # 3. Configuramos permisos de Docker
    usermod -aG docker vagrant
    systemctl enable docker
    systemctl start docker
  SHELL
end