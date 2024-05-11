MACHINES = {
  :"kernel-ubuntu" => {
              :box_name => "ubuntu/focal64",
              :box_version => "1.0.0",
              :cpus => 1,
              :memory => 2048,
            }
}

ENV['VAGRANT_SERVER_URL'] = 'http://vagrant.elab.pro'
Vagrant.configure("2") do |config|
  MACHINES.each do |boxname, boxconfig|
    config.vm.synced_folder ".", "/vagrant", disabled: true
    config.vm.define boxname do |box|
      box.vm.box = boxconfig[:box_name]
      box.vm.box_version = boxconfig[:box_version]
      box.vm.host_name = boxname.to_s
      box.vm.provider "virtualbox" do |v|
        v.memory = boxconfig[:memory]
        v.cpus = boxconfig[:cpus]
      end
      config.vm.network "forwarded_port",guest:80,host:8080
      config.vm.provision "shell",inline:<<-SHELL
        sudo apt-get update
        sudo apt-get install -y apache2
      SHELL
    end
  end
end
