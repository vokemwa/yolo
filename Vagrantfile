Vagrant.configure("2") do |config| 
  config.vm.box = "ubuntu/jammy64"

 config.vm.provision "ansible" do |ansible|
   ansible.playbook = "playbook.yaml"
   end
end
