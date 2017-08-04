# Prompts user for specific choices, the provisions a DevOps VM's using vagrant.
# Params:
# none

#Prompts user to select which Linux Flavor
puts "On which linux Flavor (input option number): 1.ubuntu/xenial64 | 2.centos/7"
input = STDIN.gets.chomp

#Validates user input, if its a small integer then 
if input.to_i.between?(1,2)

Vagrant.configure(2) do |config|
    case input.to_i
    #when "ubuntu/xenial64"
    when 1
	config.vm.define "devops-box" do |devbox|
		devbox.vm.box = "ubuntu/xenial64"
    		#devbox.vm.network "private_network", ip: "192.168.199.9"
    		#devbox.vm.hostname = "devops-box"
      		devbox.vm.provision "shell", path: "scripts/install.sh"
    		devbox.vm.provider "virtualbox" do |v|
    		  v.memory = 4096
    		  v.cpus = 2
    		end
	end
    #when "centos/7"
    when 2
    config.vm.define "devops-box" do |devbox|
        devbox.vm.box = "centos/7"
        #devbox.vm.network "private_network", ip: "192.168.199.9"
            #devbox.vm.hostname = "devops-box"
            devbox.vm.provision "shell", path: "scripts/install.sh"
            devbox.vm.provider "virtualbox" do |v|
              v.memory = 4096
              v.cpus = 2
            end
        end
    else
    puts "Script Cannot continue execution, option not selected or not found."
    exit
end
end
else
   puts "Script Cannot continue execution, option not selected or not found."
   exit
end


