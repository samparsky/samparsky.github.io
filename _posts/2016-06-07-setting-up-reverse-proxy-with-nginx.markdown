---
published: false
title: Setting up Reverse Proxy with NGINX
layout: post
---
##### What is a Reverse Proxy?

A reverse proxy is an intermediate between a client server and a response server. It basically like a

##### Setting up NGINX
We would be setting up demo server with Vagrant. You can always read up later about Vagrant.. We will be making use of three vagrant box instances, one vagrant box will be acting as our proxy server while the other two vagrant boxes will be acting as our mainstream servers.

##### Installing Vagrant
To install vagrant on windows or linux or mac based systems. The instructions can be found here
---- link ----- . 

##### Setting up Vagrant
We will be creating three separate vagrant files and 
For the Proxy Server box the following content should be stored in the vagrant file
``` ruby
Vagrant.configure(2) do |config|
	config.vm.define "proxyserver" do |proxyserver|
		proxyserver.vm.box = "ubuntu/trusty64"
		proxyserver.vm.hostname = "proxyserver"
		proxyserver.vm.network "private_network", ip:"192.168.33.20"
		proxyserver.vm.network "forwarded_port",guest: 80,   host: 4000
	end
end
```
For the other two vagrant boxes will be just be making a few changes to the Vagrantfile we have above.
We will be changing the ip address and port number to avoid collision.

For mainstream server one
```
Vagrant.configure(2) do |config|
	config.vm.define "mainone" do |mainone|
		mainone.vm.box = "ubuntu/trusty64"
		mainone.vm.hostname = "mainone"
		mainone.vm.network "private_network", ip:"192.168.33.10"
		mainone.vm.network "forwarded_port",guest: 80,   host: 4100
	end
end
```
For mainstream server two

```
Vagrant.configure(2) do |config|
	config.vm.define "maintwo" do |maintwo|
		maintwo.vm.box = "ubuntu/trusty64"
		maintwo.vm.hostname = "maintwo"
		maintwo.vm.network "private_network", ip:"192.168.33.30"
		maintwo.vm.network "forwarded_port",guest: 80,   host: 4200
	end
end
```
#### After setting up vagrant

We would go into the proxy server directory and run ` vagrant up `. This would make vagrant to either download the base box from the repo or if it exists locally use the ubuntu base box to setup our proxy server. We would then connect to the vagrant box instance by ssh. 

We would connect to it by executing `vagrant ssh proxy_server` in the terminal. 
After that  
The instruction details on setting up nginx 
To be able to see this in action we would have to install nginx. The instructions to install nginx can be found here 

The nginx configuration file can be found at ` /etc/nginx/ ` directory on debian operating systems. 

To setup our w