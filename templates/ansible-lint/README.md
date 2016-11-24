# ###-->ZZZ_IMAGE<--###  

[`###-->ZZZ_IMAGE<--###`][1] is a [docker][2] image that bundles the following:  
* **[ansible-lint ###-->ZZZ_ANSIBLE_LINT_VERSION<--###][3]:** Checks [Ansible][4] playbooks for practices and behaviour that could potentially be improved.    

## Details
* The container runs as "dev" user (i.e. UID 1000). *Please keep this in mind as you mount volumes!* 
* The following volumes exist (and are owned by dev):  
  - /data
  - /ops
  - /state
  - /ansible
  - /home/dev/.ssh
* /ansible is your default workdir. *Knowing this will be helpful when you're mounting your playbook for linting.*   
* /home/dev is $HOME
* The entrypoint for this image is ***/usr/bin/ansible-lint***.  This should be sufficient for most use cases.

## Usage 
This image can easily be extended.  But to analyze your Ansible playbooks:

````
docker run -it --rm \
	-v $(PLAYBOOK_DIR):/ansible \
	###-->ZZZ_IMAGE<--###:###-->ZZZ_VERSION<--### site.yml
		
````

## Misc. Info 
* Latest version: ###-->ZZZ_CURRENT_VERSION<--###   
* Built on: ###-->ZZZ_DATE<--###   
* Base image: ###-->ZZZ_BASE_IMAGE<--### ([dockerfile][6])  
* [Dockerfile][7]

[1]: https://hub.docker.com/r/###-->ZZZ_IMAGE<--###/   
[2]: https://docker.com 
[3]: https://github.com/willthames/ansible-lint  
[4]: http://www.ansible.com/  
[6]: https://github.com/nocsigroup/dockerfiles/blob/master/base/alpine
[7]: https://github.com/nocsigroup/dockerfiles/tree/master/ansible-lint
