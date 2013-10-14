#Chef Blueprint: rightscale_server

##Description

A Chef blueprint for a RightScale Server. Only the rightscale cookbook is used to provide configuration for usage of RightScale-managed node.

##Requirements

* Chef 0.10.10 or higher (earlier versions may work with some cookbooks/recipes)
* A Linux host or guest environment
* Vagrant 1.2 or higher (if using Vagrant)
* Git (if checking out the source from GitHub)

##Usage

See the Quick Start below to get started.

###Cookbooks

The following core cookbooks are used:

* rightscale

The following additional/depends cookbooks:

* apache2
* collectd
* rest_connection

See the `Cheffile.lock` for details on their upstream sources.

###Chef Attributes

See the `share/chef` folder for examples on attribute usage using a `node.json`.

TODO: guide on main attributes and their usage

##Quick Start

###VirtualBox with Vagrant

####Install VirtualBox

Follow the VirtualBox (or your OS/distribution) documentation to install VirtualBox if not already installed, see https://www.virtualbox.org/wiki/Documentation

####Install Vagrant

Follow the Vagrant (or your OS/distribution) documentation to install Vagrant (latest version recommended), see http://docs.vagrantup.com/v2/installation/index.html

####Install Librarian for Chef

	$ gem install librarian-chef --no-rdoc --no-ri

####Clone the rightscale_server Chef Blueprint

	$ mkdir -p ~/src/github/chef-blueprints
	$ cd ~/src/github/chef-blueprints
	$ git clone https://github.com/chef-blueprints/rightscale_server.git
	$ cd rightscale_server

Or alternatively, download and extract the zip https://github.com/chef-blueprints/rightscale_server/archive/master.zip

####Fetch the cookbooks with Librarian

	$ librarian-chef install
  
####Setup a Vagrantfile

Copy the default Vagrantfile from `share/vagrant`:

	$ cp -v share/vagrant/Vagrantfile.default Vagrantfile

####Setup node.json

Copy the default node.json from `share/chef` to get started using a basic `run_list` and set of node attributes.

	$ cp -v share/chef/node.json.default node.json

####Run with Vagrant

Already up'd a rightscale_server?

	#vagrant status                             # check vm status
	#vagrant reload                             # reload the vm
	#vagrant provision                          # (re-)provision the vm
	#vagrant suspend                            # suspend the vm
	#vagrant halt                               # power down the vm
	#vagrant destroy                            # destroy the vm
	#vagrant box remove rightscale_server       # remove the box

#####Run the virtual machine

Add a new box and up it (default in `Vagrantfile` is Debian 7.10, Ubuntu 12.04 is also tested and supported).

Vagrant will automatically add a new box per the Vagrantfile if not already created (including download).

	$ vagrant up

Need debug?

	$ VAGRANT_LOG=debug vagrant up
	
This uses the `Vagrantfile` and `node.json` (for the Chef Solo provisioning) residing in the root of the repository, copied above.

###Chef Solo

Using the Vagrant/VirtualBox process above is recommended for desktop/workstations users and will provide an operational Linux box, out-of-box.
The instructions below demonstrate usage with Chef Solo standalone. Commands are relative the root of the repository.

	# chef-solo -c share/chef/solo.rb
	
By default this uses the `node.json`. You can easily switch the JSON attributes used with another example:

	# chef-solo -c share/chef/solo.rb -j /etc/chef/node.json
	
Its also possible to run with the cookbooks source as remote. This is handy because no Git checkout is needed:

	# chef-solo -r https://github.com/chef-blueprints/rightscale_server/tarball/master
	
And with a specific tag such as `0.0.1`:

	# chef-solo -r https://github.com/rightscale-blueprints/rightscale_server/tarball/0.0.1

For more information on using Chef Solo, see http://wiki.opscode.com/display/chef/Chef+Solo

###RightScale

Import and use the latest revision of the ServerTemplate, 'Apache 2'.
Published and maintained in the MultiCloud Marketplace, http://www.rightscale.com/library/server_templates/Apache-2/lineage/14213.

##Using Librarian

###Updating cookbooks

Set this environment variable to strip `.git` from each cookbook checkout:

	$ export LIBRARIAN_CHEF_INSTALL__STRIP_DOT_GIT=1

To update a cookbook, for example, sudo:
	
	$ librarian-chef update sudo

To cleanly re-fetch all the cookbooks in `cookbooks/` per the `Cheffile`, run the following:

	$ rm Cheffile.lock; librarian-chef install --clean

For more information on usage, see https://github.com/applicationsonline/librarian-chef

##Errata

TODO: MANIFEST file.

##License and Author

Author:: Chris Fordham (<chris [at] fordham [hyphon] nagy [dot] id [dot] au>)

Copyright 2013, Chris Fordham

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
