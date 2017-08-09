# Prompts user for specific choices, the provisions a DevOps VM's using vagrant.
# Params:
# none

#Prompts user to select which Linux Flavor
puts "On which linux Flavor (input option number): 1.ubuntu/xenial64 | 2.centos/7"
input = STDIN.gets.chomp

#Validates user input, if its a small integer then 
if input.to_i.between?(1,2)

Vagrant.configure(2) do |config|
#    config.ssh.username = 'DevOps'
    #config.ssh.private_key_path = "~/.ssh/DevOps"
#    config.ssh.insert_key = false
#    config.ssh.forward_agent = true
     config.vm.network "public_network", bridge: [
     "eno1: Wired Connection 1"
     ]
       
  
    case input.to_i
    #when "ubuntu/xenial64"
    when 1
    config.vm.define "devops-box-ubuntu" do |devbox|
        devbox.vm.box = "ubuntu/xenial64"
            #devbox.vm.network "private_network", ip: "192.168.199.9"
            #devbox.vm.hostname = "devops-box"
            devbox.vm.provision "shell", path: "scripts/install.sh", args: "flavor=#{input.to_i}"
                        devbox.vm.provider "virtualbox" do |v|
              v.memory = 2048
              v.cpus = 1
            end
    end
    #when "centos/7"

    when 2
    config.vm.define "devops-box-centos" do |devbox|
        devbox.vm.box = "centos/7"
        #devbox.vm.network "private_network", ip: "192.168.199.9"
            devbox.vm.hostname = "devops-box"
            devbox.vm.provider "virtualbox" do |v|
              v.memory = 2048
              v.cpus = 1
            end
            puts "Username PWD:"
            PASSW = STDIN.gets.chomp
            devbox.vm.provision "shell", inline: <<-EOC, env: {"PASSW" => PASSW}
                 #Add DevOps User
              sudo adduser DevOps
                #Add DevOp0s to sudo
              sudo sh -c "echo 'DevOps  ALL=(ALL:ALL) ALL' >> /etc/sudoers"
              echo "DevOps:${PASSW}" | chpasswd    
            #Generate Public/Private Keys
              cd /home/DevOps
              mkdir .ssh
              chown DevOps:DevOps .ssh
              chmod 700 .ssh
              cd .ssh
              ssh-keygen -b 4096 -f DevOps -t rsa -N ''
              cat DevOps.pub >> authorized_keys
              chmod 600 authorized_keys
              chown DevOps authorized_keys
              openssl rsa -in DevOps -outform pem > DevOps.pem
              rsync -avz DevOps.pem en@192.168.15.110/:~/.ssh   
              EOC
            devbox.vm.provision "shell", path: "scripts/install.sh", args: input.to_i
            

  end

    else
    puts "Script Cannot continue execution, option not selected or not found."
    exit
end
end
end
