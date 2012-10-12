**NRPE and Nagios-Plugins Cookbook**

This cookbook makes the installation of the Nagios Remote Plugin Executor (NRPE) and Nagios-Plugins on remote servers a lot easier.

It installs:-

* NRPE version 2.13
* Nagios plugins version 1.4.16

**Requirments**

This cookbook has been written and tested on a Ubuntu 11.04 system.  It should however work on other Ubuntu releases.

Ruby 1.9.3 and the chef-solo gem.




**How can I execute the cookbook?**

If you are installing on a clean system (i.e one without ruby etc) then the repo contains a batch script installNagiosRemote.sh which will do the following:-


* Install ruby 1.9.3 and it's dependencies
* Install the chef gem
* Clone the NagiosRemote repo to /var/chef
* Execute the nagios-remote recipe which does the following:-
	* Installs libssl-dev
	* Creates a local nagios user
	* Downloads and installs nagios-plugins from http://www.nagios.org
	* Downloads and installs NRPE
	* Adds a startup script for the nagios-nrpe-server service to /etc/init.d/

If the server you wish to install NRPE and the nagios plugins on already has Ruby 1.9.3 installed then you can comment out the lines below from the script.

>apt-get -y update

>apt-get -y install build-essential zlib1g-dev libssl-dev libreadline-dev libyaml-dev git

>cd /usr/local/src

>wget ftp://ftp.ruby-lang.org/pub/ruby/1.9/ruby-1.9.3-p194.tar.gz

>tar -xvzf ruby-1.9.3-p194.tar.gz

> cd ruby-1.9.3-p194/

> ./configure --prefix=/usr/local

> make && make install

>rm /usr/local/src/ruby-1.9.3-p194.tar.gz

and start the script with

> gem install chef ruby-shadow --no-ri --no-rdoc


**How can I check that the installation was successful?**

After the cookbook has finished executing you can check that the install was successful by doing the following:-

 /usr/local/nagios/libexec/check_nrpe -H localhost

If everything has completed  successfully then you should see NRPE v2.13.

**OK, that completed successfuly.....what do I need to do to get the remote server monitored by my Nagios server.**

Before you can monitor your remote server you need to add the ip address or hostname of your Nagios server to the

> allowed_hosts=127.0.0.1 <ip or hostname of nagios server here>

of /usr/local/nagios/etc/nrpe.cfg file 

and then execute /etc/init.d/nagios-nrpe-server to restart the NRPE service.
