## biemond-orawls-vagrant-ohs

The puppet 4.2 Oracle WebTier standalone reference implementation of https://github.com/biemond/biemond-orawls

optimized for linux, Solaris and the use of Hiera

Should work for VMware and Virtualbox

### Details
- CentOS 7.0 Vagrant box
- Puppet 4.2.2
- Vagrant >= 1.8.0
- Oracle Virtualbox >= 5.0
- VMware fusion >= 6

creates a standalone 12.1.2 & 12.2.1 Webtier

Add the all the Oracle binaries to /software

edit Vagrantfile and update the software share
- ohs1212.vm.synced_folder "software", "/software"
- ohs1221.vm.synced_folder "software", "/software"

### Software
- Webtier 12.1.2 or 12.2.1
- JCE Policy 8 [jce_policy-8.zip](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

### Startup the images

- vagrant up ohs1212
- vagrant up ohs1221

