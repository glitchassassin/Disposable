Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
  v.gui = true
  end
  config.vm.define "disposable"
  config.vm.box = "jck/disposable"
  config.vm.box_version = "1.0"
  config.vm.provision "shell", path: "script.sh"
  config.vm.synced_folder "./", "/synced"


end
