# roster.nocsi.org/consul  

[`roster.nocsi.org/consul`][1] is a [docker][2] image that bundles the following:  
* **[Consul v0.6.4][3]:** A distributed, highly available tool for service discovery, configuration, etc.  

## Details
* The container currently runs as root, BUT this is subject to change.
* The following volumes exist (and are owned by dev):  
  - /consul/data
  - /consul/config
* / is your default workdir.   

## Usage 
This image can easily be extended.  But to run Consul:

````
docker run -it --rm \
	-v /var/lib/data:/consul/data:rw \
	-v $(CONSUL_CONFIG_DIR):/consul/config:rw \
	roster.nocsi.org/consul:0.6.4 agent -config-dir=/consul/config  
		
````

## Misc. Info 
* Latest version: 0.6.4  
* Built on: 2016-10-08T08:47:53EDT   
* Base image: roster.nocsi.org/base:alpine   


[1]: https://hub.docker.com/r/roster.nocsi.org/consul/   
[2]: https://docker.com 
[3]: https://consul.io/  
