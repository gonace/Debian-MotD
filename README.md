# Debian-MotD
My goal here was to have something that could quickly tell me which machine I was using and some specifics of it, an understanding of the current state and any actions that should be taken. But, at the same time it should be as concise as is practical and, importantly be fast to execute.

Another addition I’ll make soon is to add configuration manager status, so in my case it will show the Chef last run, environment and roles applied. (This will also help remind me which boxes are using Chef before I change things which will automatically be reverted.)

The following is broadly based upon the version provided by Canonical in Ubuntu 12.04, which is Copyright 2009-2010 Canonical Ltd. and licensed under the GPL. And so this lot is also1.

#### Header (00-header)
The first part is the header. This comprises of the ASCII art hostname and the “Welcome…” text. I’m dynamically generating the ASCII art using the short version of the hostname, but you may wish to hard code it (obviously, this will need figlet installed.)


#### System Information (10-sysinfo)
This is slightly more complicated. Using a mix of standard utilities, /proc and some text parsing, it’s quite easy to assemble the system information section. As I’m only targetting Debian/Ubuntu, it’s quite easy to get this working.

In the original implementation, Canonical use their “Landscape” product to generate the statistics which provides a bit more functionality than this does.


#### Network Information (20-network)
Using a mix of standard utilities, /proc/net, /inet and some text parsing, it’s quite easy to assemble the network information section. As I’m only targetting Debian/Ubuntu, it’s quite easy to get this working.


#### Updates (30-updates)
This is much more complicated than the other sections. Canonical achieves this in Ubuntu by using the same mechanism the GUI software updater works (the notifer, not synaptic). This implements the same requirement, but using the upstream dependency that — python-apt — which allows us to interact with apt’s internals.


#### Footer (99-footer)
The default behaviour of motd is to present a combination of /etc/motd (which is regenerated on reboot) and /etc/motd.tail which is designed to append a sys admin message or similar.



## Installation
------------
1.
  - sudo apt-get update
  - sudo apt-get install figlet python-dev python-apt git
2. go to /etc/
  - Create a folder named "update-motd.d"
  - sudo chmod a+x update-motd.d
  - sudo git clone https://github.com/gonace/Debian-MotD.git . 
  - sudo git checkout jessie
  - sudo chmod +x *-*
3. go to /etc/
  - sudo rm motd
  - sudo rm /var/run/motd*
  - sudo ln -s /var/run/motd motd


## Result
------
	Linux obscured-mysql02 3.2.0-4-amd64 #1 SMP Debian 3.2.60-1+deb7u1 x86_64
           _                                 _                                 _ 
	  ___ | |__  ___  ___ _   _ _ __ ___  __| |      _ __ ___  _   _ ___  __ _| |
	 / _ \| '_ \/ __|/ __| | | | '__/ _ \/ _` |_____| '_ ` _ \| | | / __|/ _` | |
	| (_) | |_) \__ \ (__| |_| | | |  __/ (_| |_____| | | | | | |_| \__ \ (_| | |
	 \___/|_.__/|___/\___|\__,_|_|  \___|\__,_|     |_| |_| |_|\__, |___/\__, |_|
	                                                           |___/        |_|  	            

	Welcome to Debian GNU/Linux 7.5 (wheezy) (3.2.0-4-amd64).

	System information as of: Tue Dec 16 09:26:18 CET 2014

	System load:	0.05	Memory usage:	82.2% (free: 705Mb)
	Usage on /:	13%	Swap usage:	0.0%
	Local users:	1	Processes:	99
	System uptime:	70 days, 16h 47m 51s

	Network information:
	System IP:	10.0.5.101
	Traffic in:	27Gb	Traffic out:	65Gb

	Updates:
	71 updates to install.
	0 are security updates.

	Last login: Mon Dec 15 12:48:44 2014 from 10.0.2.13
