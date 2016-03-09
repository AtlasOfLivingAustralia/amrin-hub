### amrin-hub   [![Build Status](https://travis-ci.org/AtlasOfLivingAustralia/amrin-hub.svg?branch=master)](https://travis-ci.org/AtlasOfLivingAustralia/amrin-hub)

Deploying a new version of amrin-hub to Nexus
============================================

Before deploying a new version, check that the biocache-hubs dependency version is up to date in grails-app/conf/BuildConfig.groovy.

Travis-CI is used to deploy new versions of amrin-hub to Nexus. This is done automatically by updating the version number in the application.properties file and pushing to GitHub.

Once the new version of amrin-hub is deployed to Nexus, the version number in ansible-inventories needs to change. To do this, the version number must be changed in: 

https://github.com/AtlasOfLivingAustralia/ansible-inventories/blob/master/amrin.ala.org.au

If the biocache_hub_version is commented out then presumably it will use the most recent version it can find.

Deploying the current Nexus deployed version of AMRIN to a virtual machine
=========================================================================

If you have not yet installed Ansible, Vagrant, or VirtualBox, use the instructions at the [ALA Install README.md file](https://github.com/AtlasOfLivingAustralia/ala-install/blob/master/README.md) to install those first for your operating system.

Then, to deploy AMRIN onto a local virtual box install use the following instructions:

```
$ cd gitrepos
$ git clone git@github.com:AtlasOfLivingAustralia/ala-install.git
$ (cd ala-install/vagrant/ubuntu-trusty && vagrant up)
```

Add a line to your /etc/hosts file with the following information, replacing '10.1.1.3' with whatever IP address is assigned to the virtual machine that Vagrant starts up in VirtualBox:

```
10.1.1.3 amrin.ala.org.au
```

Then you can clone the ansible instructions and install it onto the given machine:

```
$ git clone git@github.com:AtlasOfLivingAustralia/ansible-inventories.git
$ ansible-playbook -i ansible-inventories/amrin.ala.org.au ala-install/ansible/amrin-hub-standalone.yml --private-key ~/.vagrant.d/insecure_private_key -vvvv --user vagrant --sudo
```
