Vagrant.configure("2") do |config| 
  config.vm.box = "geerlingguy/ubuntu2004"

 config.vm.provision "ansible" do |ansible|
   ansible.playbook = "playbook.yaml"
   ansible.verbose= "vv"
   end
end
