vagrant-nebula
==============

A robust Vagrant configuration backed by NCSA's Nebula OpenStack cloud to provide the [LSST Software Stack](http://ls.st/ug).

Getting Nebula Credentials
--------------------------

You must have the appropriate credentials if you want to use Vagrant to make queries against the nebula OpenStack cloud. By far, the easiest way to obtain authentication credentials is to use the [Nebula Horizon dashboard](https://nebula.ncsa.illinois.edu):

1. Open the Access and Security page of the [Nebula Horizon dashboard](https://nebula.ncsa.illinois.edu).
2. Click the API Access tab
3. Click on the Download OpenStack RC File button.

This will generate a file that you can source in your shell to populate the environment variables that Vagrant require to know where Nebula's service endpoints and authentication information are. In the case of the LSST project, the file will be called LSST-openrc.sh.

```bash
source /path/to/LSST-openrc.sh
# ... put in your nebula password
```

Getting Vagrant
---------------

[Download and install Vagrant](https://www.vagrantup.com/downloads.html) for your platform.

If you are using [Homebrew](http://brew.sh/) you may use the related [Cask](https://github.com/caskroom/homebrew-cask).

```bash
# Install cask, if it's not already installed.
brew install caskroom/cask/brew-cask
# Install the Vagrant cask.
brew cask install vagrant
```

Create your Vagrant machine
---------------------------

Vagrant-nebula requires Nebula OpenStack credentials and Vagrant. Please see the Getting Nebula Credentials and Getting Vagrant sections above.

To get started, clone the repo, `cd` into the directory and execute the `vagrant up el7` command.

```bash
git clone https://github.com/lsst-sqre/vagrant-nebula.git
cd vagrant-nebula
vagrant up el7
```

Time outs and errors can be expected while `vagrant` attempts to make initial contact with the new machine.

```
ssh: connect to host 141.142.209.11 port 22: Operation timed out
Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
```

SSH to your Vagrant machine
---------------------------

By default the [vagrant-openstack-provider](https://github.com/ggiamarchi/vagrant-openstack-provider) will provision and associate an SSH key-pair. To ssh to the Vagrant machine (Nebula instance) use the command:

```bash
vagrant ssh el7
```

Destroy your Vagrant machine
----------------------------

Your Vagrant machine is provisioned through the Nebula OpenStack cloud. Resources are limited so it's important that you release those resources when you are not using them. To terminate, or destroy your Vagrant machine use the `vagrant destroy el7`.

```bash
vagrant destroy el7
```

Available Vagrant Machines
--------------------------

By default this Vagrant configuration provides stable [LSST Software Stack](http://ls.st/ug) builds for CentOS 6 and CentOS 7. The following Vagrant machines are available:

* `el6` The current CentOS 6 LSST Software Stack build.
* `el7` The current CentOS 7 LSST Software Stack build.

Internals
---------

Your Vagrant machine is provisioned on Nebula's OpenStack cloud through the OpenStack API. Your machine will be named `el7-user` where user is your username when you run the `vagrant` command. The [vagrant-openstack-provider](https://github.com/ggiamarchi/vagrant-openstack-provider) will create and associate an SSH key-pair for your Vagrant machine. If you log into the Nebula Horizon dashboard you'll be able to find your OpenStack instance in the the [Instances list](https://nebula.ncsa.illinois.edu/dashboard/project/instances/) and your key pair in the [Key Pairs tab](https://nebula.ncsa.illinois.edu/dashboard/project/access_and_security/?tab=access_security_tabs__keypairs_tab).

Your exact machine configuration can be changed through editing the `Vagrantfile`, using the Nebula Horizon dashboard or using the OpenStack API.

More Resources
--------------

https://www.vagrantup.com/ - The Vagrant homepage.

https://nebula.ncsa.illinois.edu - The NCSA Nebula OpenStack Horizon dashboard.

https://github.com/ggiamarchi/vagrant-openstack-provider - The Vagrant plugin that vagrant-nebula uses.

http://ls.st/ug - LSST Software Stack documentation.

https://github.com/lsst-sqre/asteroid - Use libcloud to interact with Nebula.

https://github.com/openstack/python-openstackclient - The OpenStack command-line client.
