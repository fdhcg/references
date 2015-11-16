Vagrant.configure("2") do |config|

        if false
	config.vm.define "web" do |web|
		web.vm.provider "docker" do |d|
			d.image = "scrapybook/web"
			d.name = "web"
			d.ports = ["9312:9312"]
		end
		web.vm.network "forwarded_port", guest: 9312, host: 9312
	end

        config.vm.define "spark" do |spark|
            spark.vm.provider "docker" do |d|
                d.image = "sequenceiq/spark:1.5.1"
                d.cmd = ["-d"]
                d.name = "spark"
                d.create_args = ["-h", "spark"]
                d.ports = ["8088:8088", "8042:8042"]
            end
        end
        end
	
	config.vm.define "dev", primary: true do |dev|
		dev.vm.provider "docker" do |d|
			#d.image = "scrapybook/dev"
                        d.build_dir = "../../scrapybook-docker-dev/trusty/latest/"
			d.name = "dev"
			d.has_ssh = true
			d.ports = ["6800:6800"]
			#d.link("web:web")
			#d.link("spark:spark")
		end
            dev.vm.synced_folder ".", "/root/book"
		
	    dev.ssh.username = 'root'
	    dev.ssh.private_key_path = 'insecure_key'
	
            dev.vm.network "forwarded_port", guest: 6800, host: 6800
    end
end