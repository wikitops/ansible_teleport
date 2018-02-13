# Ansible : Playbook Teleport
The aim of this project is to deploy a simple [Teleport](https://gravitational.com/teleport/) instance on Vagrant with some basic configuration and three nodes to test the functionalities.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

What things you need to run this Ansible playbook :

* [Vagrant](https://www.vagrantup.com/docs/installation/) must be installed on your computer
* Update the Vagrant file based on your computer (CPU, memory), if needed
* You must have download the ubuntu Xenial64 vagrant box :

```
vagrant box add https://app.vagrantup.com/ubuntu/boxes/xenial64
```

### Usage

A good point with Vagrant is that you can create, update and destroy all architecture easily with some commands.

Be aware that you need to be in the Vagrant directory to be able to run the commands.

#### Build Environment

Vagrant needs to init the project to run and build it :

```
vagrant up
```

After build, you can check which virtual machine Vagrant has created :

```
vagrant status
```

If all run like it is expected, you should see something like this :

```
$ vagrant status

Current machine states:

teleport01                   running (virtualbox)
node01                       running (virtualbox)
node02                       running (virtualbox)
node03                       running (virtualbox)
```

#### Deployment

To deploy the Teleport cluster, you just have to run the Ansible playbook teleport.yml with this command :

```
ansible-playbook teleport.yml
```

If all run like it is expected, you should access the Teleport login interface : http://10.0.0.151:3080/

The playbook should create a temporary token to create a login for a vagrant user. The link to configure the password should appear at the end of the playbook execution like this one :

```
[...]

ok: [10.0.0.151] => {
    "msg": [
        "Signup token has been created and is valid for 1 hours. Share this URL with the user:",
        "https://teleport01:3080/web/newuser/9d30b790a926c7bf3470a8e3ba00d114",
        "",
        "NOTE: make sure 'teleport01' is accessible!"
    ]
}
```

Just follow the link provided, register the user and you should access the Teleport Web interface.

#### Destroy

To destroy on what Vagrant has created, just run this command :

```
vagrant destroy
```

## Author

Member of Wikitops : https://www.wikitops.io/
