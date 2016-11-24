# roster.nocsi.org/jinja2  

[`roster.nocsi.org/jinja2`][1] is a [docker][2] image that bundles the following:  
* **[jinja2][3]:**  A modern and designer-friendly templating language for Python, modelled after Django’s templates.  

## Usage  
As an example, say I want to generate some json from the following jinja2 template:

```sh
{
{%- if do_for_fun %}
    "extra_token": "{{ extra_token | default('dummy_value') }}",
{%- endif %}
    "datacenter": "{{ datacenter }}",
    "acl_ttl": "{{ acl_ttl }}"
}
```


If I run my jinja2 container to render my some.json file:     

```sh
docker run -i \
    -v ${MY_TEMPLATE_DIR}:/data \
	-e TEMPLATE=some.json.j2 \
	-e "PGID=$(id -g)" -e "PUID=$(id -u)" \
	roster.nocsi.org/jinja2:0.0.1 datacenter='msp' acl_ttl='30m' > ${PWD}/some.json
```


The rendered output would be:
```json
{
    "datacenter": "msp",
    "acl_ttl": "30m"
}
```


Additionally, if you want to write your rendered output to the same directory as your template, just specify the file name by setting the OUT_FILE environment variable:

```sh
docker run -i \
    -v ${MY_TEMPLATE_DIR}:/data \
    -v ${MY_OUTPUT_DIR}:/out \
	-e TEMPLATE=some.json.j2 \
	-e OUT_FILE=/out/some.json \
	-e "PGID=$(id -g)" -e "PUID=$(id -u)" \
	roster.nocsi.org/jinja2:0.0.1 datacenter='msp' acl_ttl='30m'
```


The key things to remember are:   
* Mount the directory containing your template(s) to the container's /data directory
* Set the container's environment variable *TEMPLATE* to the name of your template file
* The template values are passed in as space delimited *name=value* pairs 
* Loaded extensions: jinja2.ext.autoescape, jinja2.ext.do, jinja2.ext.loopcontrols, jinja2.ext.with_
* autoescape is set to *True*
* **YMMV!!!**

## Misc. Info 
* Latest version: 0.0.1   
* Built on: 2016-10-08T08:47:53EDT   
* Base image: roster.nocsi.org/base:alpine ([dockerfile][6])  
* [Dockerfile][7]

[1]: https://hub.docker.com/r/roster.nocsi.org/jinja2/   
[2]: https://docker.com 
[3]: http://jinja.pocoo.org/docs/dev/
[6]: https://github.com/nocsigroup/dockerfiles/blob/master/base/alpine
[7]: https://github.com/nocsigroup/dockerfiles/tree/master/jinja2
