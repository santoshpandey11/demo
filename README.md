### Required API output

Calling the API returns:

- The application version.
- The latest git commit SHA.
- A description of the application.

Sending a GET request to http://localhost:8000/version should return similar to the following:

```json
"myapplication": [
  {
    "version": "1.0.0",
    "lastcommitsha": "abc57858585",
    "description" : "pre-interview technical test"
  } ]
```

### Solution Implementation
## Infrastructure for kubernetes
spin up VM with centos with At least 8 GB of RAM and 15 GB of free hard disk space for the virtual machines. ensure port 22, 8080 and 8080 is available for traffic
Software Installations and commands:
update  hosts: PIP in file setup-Python-Vagrant-Vbox.yaml
yum install  wget ;
yum install curl ;
script setup-Python-Vagrant-Vbox.yml will install:
-Vagrant 2.2.6
-VirtualBox 6.1.6 
-Python
-Ansible 2.9.6
 configure virtual machine to start automatically
define below variables at /etc/default/virtualbox
 VBOXAUTOSTART_DB=/etc/vbox
 VBOXAUTOSTART_CONFIG=/etc/vbox/vbox.cfg
 content of vbox.cfg:
 # Default policy is to deny starting a VM, the other option is "allow".
 default_policy = deny
 # Create an entry for each user allowed to run autostart
 myuserid = {
 allow = true
 }
- restart VM


cd ansible-vbox-vagrant-kubernetes
command- vagrant up 
This command spins up  2 slave node with a single master
K8S-M-1 at eth1: 192.168.50.11
K8S-N-1 at eth1: 192.168.50.12
K8S-N-2 at eth1: 192.168.50.13
vboxnet0 virtual iface: 192.168.50.1



Calling the API returns:
A minimal API built with Express JS and run with Docker (distroless/nodejs) that exposes a HTTP API server.

### CI Builds

The Travis CI build is configured in `.travis.yml`

Travis:
- Writes the current git rev SHA (short) to a file that is baked into the image.
- Builds the application-in Docker.
- Runs some basic tests.
- Deploys the docker image to dockerhub
- trigger Ansible playbook to provision kubernetes and deploy application 

 need to set the `DOCKER_USERNAME` , `DOCKER_PASSWORD` , `KUBERNETESENDPOINT` , `KUBERNETESCERTIFICATE` `KUBERNETESTOKEN` variables in the Travis UI.

### Requirements

To use the provided Makefile the following are required:

- `make`
- `jq`
- `docker`
- `git`

And if you want to run the tests manually you'll need


