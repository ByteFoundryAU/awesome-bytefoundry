# Some Useful, but Unknown, Debian Packages

# See also 

   * https://wiki.debian.org/SimplePowerSave
# Stuff to add

## apt-dater

does apt-get updates (etc) en mass

## adjtimex

actually reduce/stop clock drift, rather than having ntp constantly tweaking the system time

## apticron

emails you a list of packages to be updated.

configure via =/etc/apt/listchanges.conf=

## console-log

puts exim and system logs out on tty7 and tty8 so if things crash you can see them

## cpulimit

control max cpu usage of a process

## deborphan

finds and helps remove 'orphaned' packages and config files 

   * =orphaner= with no options looks for anything apt considers a library
   * =orphaner --find-config= looks for left over config files from removed packages
   * =orphaner --help= does what you would imagine

(surprise! apt doesnt remove config files when it removes packages, remove with --purge to clean them. i.e. =apt-get --purge remove foo= )



## dhcpdump

Like tcpdump, but knows all about dhcp

## disktype

convenient way to disk size, partitions, format, uuid etc etc

## dstat

vmstat, iostat and ifstat all in one... with color!

## eatmydata

Disables fsync, so programs that ask to sync data to disk only think they have. Dangerous as important data can be lost, but can improve performance.

## ferm / shorewall

both try to make iptables (and firewall stuff generally) more straight forward

## grepcidr

Like grep, but searches intelligently for ip addresses

## gdebi-core

Useful for installing local packages plus deps (which you would like to draw from repos)

Runs like this...
<pre>
gdebi local-file.deb
</pre>

## haveged

Unless you have a specific reason to not trust any hardware random number generator on your system, you should try to use them with the rng-tools first and if it turns out not to be enough (or if you do not have a hardware random number generator available), then use Haveged. 

Run:
<verbatim>cat /proc/sys/kernel/random/entropy_avail</verbatim>

Values &lt; 1000 indicate low entropy and cryptographic applications will block until there is enough entropy available, which eg. could result in slow wlan speed (for WAP)

## iptables-persistent

As the name implies.

Use the following to save: <pre>invoke-rc.d iptables-persistent save</pre> 

## jq 

command like json processing

## libpam-ssh

unlocks your ssh key if the password is the same as your log in

## localepurge

cleans up locales to save space, runs initially then runs after package installs

## molly-guard

wraps reboot and halt, so that you dont run them on ssh accidentally

## mtr

useful alternative to 'traceroute' - keeps updating in real time

## parallel

runs commands in parallel. can do quite insane stuff.

## pv

Like =cat= but gives you a % of how far through the pipe things are

## redir

Probably what you want rather than netcat attached to xinetd

## rng-tools

Keeps random working well. 

## safe-rm

Stops you doing bad stuff like =rm -rf /=

## snmp-mibs-downloader

mibs are 'non-free', dont forget to install them with snmp

## ssmtp

Just forwards system emails to a mail hub

## sysdig

system-level exploration and troubleshooting tool

## sxid

keeps track of setuid and setgid files

## tree

simple cli command. very handy


## unattended-upgrades
see https://wiki.debian.org/UnattendedUpgrades
## watchdog

This is a simple daemon to feed a system watchdog.
In the =/etc/watchdog.conf= but at least...
<pre>watchdog-device = /dev/watchdog
realtime = yes
priority = 1
</pre>

You can also do ICMP pings, regular file changes (use with syslog marks), system load, temperature sensors and others
By default things happen every second, this can be dialed back as needed.

Softdog can be used if no hardware watchdog is available, either way you can have watchdog load the module by setting it in =/etc/default/watchdog=
<pre>watchdog_module="softdog"
</pre>

## zopfli

Gzip, but gzips better

## xclip

pipe to X windows clipboard

In your =.bashrc= / =.bash_aliases=, put:

<pre>alias setclip='xclip -selection c'
alias getclip='xclip -selection clipboard -o'</pre>

You can now use *setclip* and *getclip*, e.g:

<pre>$ echo foo | setclip
$ getclip
foo</pre>


# Stuff to delete 

   * mlocate
   * durep

