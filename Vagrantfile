Vagrant.configure("2") do |config|

	config.vm.define "testnode" do |define|
  	define.ssh.insert_key = false
  	define.vm.box = "ubuntu/bionic64"
  	define.vm.hostname = "testnode"
  	define.vm.network :private_network, ip: "192.168.56.11"
  	# if you would like to use port forwarding, uncomment the line below
  	# define.vm.network :forwarded_port, guest: 5432, host: "543#{n}"
 
  	define.vm.provider :virtualbox do |v|
    	v.cpus = 1
    	v.memory = 1024
    	v.name = "testnode"
  	end
 
    define.vm.provision :ansible do |ansible|
      ansible.limit = "all"
      ansible.playbook = "playbook.yaml"
 
      ansible.host_vars = {
        "testnode" => {:connection_host => "192.168.56.11",
                    	:node_id => 1,
                    	:role => "primary" },
      	}
  	end
 
	end
end