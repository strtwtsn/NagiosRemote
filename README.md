Hello Everyone

This repository contains a chef-solo cookbook that can be used to install nagios-plugins and NRPE on a remote server ready for monitoring.


The installNagiosRemote.sh script if used will install ruby 1.9.3 along with the chef-solo gem, and then go on to checkout and install nagios-plugins together with NRPE.


Should you already have ruby and the chef-solo gem installed then you can do:-

sudo git clone https://github.com/strtwtsn/NagiosRemote.git /var/chef  // This will clone the repository into your /var/chef directory

and then run

sudo chef-solo -c /var/chef/config/chefsolo.rb -j /var/chef/roles/nagios-remote.json // This will run the cookbook and install the relevant packages.


Things installed by the cookbook

Nagios-plugins-1.4.16
NRPE 2.13

It will also create a startup script for the NRPE service and add this to the default runlevels

