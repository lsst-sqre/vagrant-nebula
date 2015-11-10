vagrant-nebula
==============

A vagrant configuration backed by NCSA's nebula OpenStack cloud.

Getting Credentials
-------------------

You must have the appropriate credentials if you want to use Vagrant to make queries against the nebula OpenStack cloud. By far, the easiest way to obtain authentication credentials is to use [nebula horizon dashboard](https://nebula.ncsa.illinois.edu/dashboard/project/access_and_security/). Click the API Access tab to display two buttons and click on the Download OpenStack RC File button. This will generate a file that you can `source` in your shell to populate the environment variables that Vagrant require to know where nebula's service endpoints and authentication information are. In the case of the LSST project, the file will be called `LSST-openrc.sh`.

```bash
source /path/to/LSST-openrc.sh
# ... put in your nebula password
```

Using vagrant
-------------

Vagrant-nebula requires OpenStack nebula credentials. Please see the Getting Credentials section above.

Clone this repo. `cd` into the directory. Run the `vagrant up el7` command to create the vagrant machine (nebula instance).

```bash
cd /path/to/vagrant-nebula
vagrant up el7
```

Time outs and errors can be expected while vagrant attempts to make initial contact with the new machine.

```
ssh: connect to host 141.142.209.11 port 22: Operation timed out
Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
```

SSH to the instance
-------------------

To ssh to the vagrant machine (nebulua instance) use the command:

```bash
vagrant ssh el7
```

More Resources
--------------

https://github.com/ggiamarchi/vagrant-openstack-provider - The vagrant plugin that vagrant-nebula uses.

https://github.com/lsst-sqre/asteroid - Use libcloud to interact with nebula.

https://github.com/openstack/python-openstackclient - The OpenStack command-line client.
