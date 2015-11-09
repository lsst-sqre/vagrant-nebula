vagrant-nebula
==============

A vagrant configuration backed by NCSA's nebula.

Using vagrant
-------------

Clone this repo. Get your LSST-openrc.sh from [nebula horizon](https://nebula.ncsa.illinois.edu/dashboard/auth/login/?next=/dashboard/) and source it. Run `vagrant up el7` command to create the vagrant machine (nebula instance).

```bash
source /path/to/LSST-openrc.sh
# ... put in your nebula password
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
