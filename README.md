vagrant-nebula
==============

A vagrant configuration backed by NCSA's nebula.

Using vagrant
-------------

Clone this repo. Get your LSST-openrc.sh from [nebula horizon](https://nebula.ncsa.illinois.edu/dashboard/auth/login/?next=/dashboard/) and source it. Run `vagrant up --provider=openstack` command.

```bash
source /path/to/LSST-openrc.sh
# ... put in nebula password
vagrant up --provider=openstack
```
