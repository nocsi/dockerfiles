# roster.nocsi.org/ansible  

[`roster.nocsi.org/ansible`][1] is a [docker][2] image that bundles the following:  
* **[Ansible 2.0.0.2][3]:** A radically simple IT automation system. It handles configuration-management, application deployment, cloud provisioning, ad-hoc task-execution, and multinode orchestration - including trivializing things like zero downtime rolling updates with load balancers. Ansible is written in [Python](https://www.python.org/).    

## Details
* The container runs as "dev" user (i.e. UID 1000). *Please keep this in mind as you mount volumes!* 
* The following volumes exist (and are owned by dev):  
  - /data
  - /ops
  - /state
  - /ansible
  - /home/dev/.ssh
* /ansible is your default workdir. *Knowing this will be helpful when you're mounting your playbooks for execution.*   
* /home/dev is $HOME
* The entrypoint for this image is ***/opt/ansible/bin/ansible-playbook***.  This should be sufficient for most use cases.

## Usage 
This image can easily be extended.  But to run your Ansible playbooks:

````
docker run -it --rm \
	-v $(SSH_DIR):/home/dev/.ssh \
	-v $(CURRENT_DIR):/state:rw \
	-v $(PLAYBOOK_DIR):/ansible:rw \
	roster.nocsi.org/ansible:2.0.0.2 site.yml
		
````

## Misc. Info 
* Latest version: 2.1.0.0   
* Built on: 2016-10-08T08:47:53EDT   
* Base image: roster.nocsi.org/base:alpine ([dockerfile][6])  
* [Dockerfile][7]

[1]: https://hub.docker.com/r/roster.nocsi.org/ansible/   
[2]: https://docker.com 
[3]: http://www.ansible.com/home  
[4]: https://galaxy.ansible.com/list#/roles/464    
[5]: https://github.com/geerlingguy
[6]: https://github.com/nocsigroup/dockerfiles/blob/master/base/alpine
[7]: https://github.com/nocsigroup/dockerfiles/tree/master/ansible
