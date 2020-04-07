# Some Useful, but Unknown, Debian Packages

## See also

   * https://wiki.debian.org/SimplePowerSave
   * https://wiki.debian.org/ReduceDebian
   * https://www.debian.org/doc/manuals/securing-debian-howto/index.en.html#contents

## The List

### adjtimex

actually reduce/stop clock drift, rather than having ntp constantly tweaking the system time

### apt-dater

does apt-get updates (etc) en mass

### apticron

emails you a list of packages to be updated.

configure via `/etc/apt/listchanges.conf`

### automysqlbackup / autopostgresqlbackup

nightly backups or mysql / postgresql made insanely easy. no excuses

### console-log

puts exim and system logs out on tty7 and tty8 so if things crash you can see them

### conserver

Console server software

### cpulimit

control max cpu usage of a process

### dacs

DACS is a light-weight single sign-on and role-based access control system for web servers and server-based software. It is also an authentication and authorization toolkit for programmers. DACS makes secure resource sharing and remote access via the web easier, safer, and more efficient.

 Its not a small thing to install. But it's awesome.

### debian-goodies

   * `checkrestart` - what needs to be restarted since packages were upgradedA
   * `dpigs` - which packages are using the most space
   * `which-pkg-broke` - find which package might have broken another

### deborphan

finds and helps remove 'orphaned' packages and config files

   * `orphaner` with no options looks for anything apt considers a library
   * `orphaner --find-config` looks for left over config files from removed packages
   * `orphaner --help` does what you would imagine

(surprise! apt doesnt remove config files when it removes packages, remove with --purge to clean them. i.e. `apt-get --purge remove foo` )

### debsums

Check MD5's of files against what they were in the .deb file when installed

    * `debsums --changed` - reports only changed files
    * `debsums --changed --config` - reports only changed config files

### dhcpdump

Like tcpdump, but knows all about dhcp

### disktype

convenient way to disk size, partitions, format, uuid etc etc

### dstat

vmstat, iostat and ifstat all in one... with color!

### duc

high-performance disk usage analyzer

also duc-nox for servers

### eatmydata

Disables fsync, so programs that ask to sync data to disk only think they have. Dangerous as important data can be lost, but can improve performance.

### ferm / shorewall

both try to make iptables (and firewall stuff generally) more straight forward

### grepcidr

Like grep, but searches intelligently for ip addresses

### gdebi-core

Useful for installing local packages plus deps (which you would like to draw from repos)

Runs like this...
<pre>
gdebi local-file.deb
</pre>

### haveged

Unless you have a specific reason to not trust any hardware random number generator on your system, you should try to use them with the rng-tools first and if it turns out not to be enough (or if you do not have a hardware random number generator available), then use Haveged.

Run:
`cat /proc/sys/kernel/random/entropy_avail`

Values &lt; 1000 indicate low entropy and cryptographic applications will block until there is enough entropy available, which eg. could result in slow wlan speed (for WAP)

### inxi

A command line system information tool.

Run:
`inxi -v8`

### iptables-persistent

As the name implies.

Use the following to save: <pre>invoke-rc.d iptables-persistent save</pre>

### iputils-clockdiff

Compares local clock to remote

### jq

command like json processing

### lftp

Sophisticated command-line FTP/HTTP/BitTorrent client programs

### libpam-ssh

unlocks your ssh key if the password is the same as your log in

### localepurge

cleans up locales to save space, runs initially then runs after package installs

### mcelog

install if you have ecc memory, so you know if things are going well/badly

### miller

Slice and dice CSV files on the CLI

### molly-guard

wraps reboot and halt, so that you dont run them on ssh accidentally

### mtr

useful alternative to 'traceroute' - keeps updating in real time

### nield

receive notifications from kernel through netlink socket and generate logs related to NIC interfaces

### nethogs

Lists network traffic by process / program

### ostinato

Wireshark in reverse - craft packets using the GUI

### parallel

runs commands in parallel. can do quite insane stuff.

### pigz

Multi-processor gzip

### pv

Like `cat` but gives you a % of how far through the pipe things are

### redir

Probably what you want rather than netcat attached to xinetd

### reptyr

Attaches runnng programs to new terminals, for example in to screen

### rng-tools

Keeps random working well.

Check if your cpu has hardware random function

grep rdrand /proc/cpuinfo

also the /dev/hwrng device should exist

See also haveged

See also https://main.lv/writeup/kernel_dev_hwrng.md

### rssh or rush

Both are shells that allow users to be restricted to perform minimal functions.

### safe-rm

Stops you doing bad stuff like `rm -rf /`

### snmp-mibs-downloader

mibs are 'non-free', dont forget to install them with snmp

### ssldump

Tcpdump with ssl decoding

### ssmtp

Just forwards system emails to a mail hub

Note: doesnt expand from address to fqdn... annoying

### sysdig

system-level exploration and troubleshooting tool

### sxid

keeps track of setuid and setgid files

### tree

simple cli command. very handy

### tshark

wireshark ui in terminal

### unattended-upgrades

see https://wiki.debian.org/UnattendedUpgrades

### usbguard

a USB device whitelisting tool

### watchdog

This is a simple daemon to feed a system watchdog.
In the `/etc/watchdog.conf` but at least...
<pre>watchdog-device = /dev/watchdog
realtime = yes
priority = 1
</pre>

You can also do ICMP pings, regular file changes (use with syslog marks), system load, temperature sensors and others
By default things happen every second, this can be dialed back as needed.

Softdog can be used if no hardware watchdog is available, either way you can have watchdog load the module by setting it in `/etc/default/watchdog`
<pre>watchdog_module="softdog"
</pre>

### xclip

pipe to X windows clipboard

In your `.bashrc` / `.bash_aliases`, put:

<pre>alias setclip='xclip -selection c'
alias getclip='xclip -selection clipboard -o'</pre>

You can now use *setclip* and *getclip*, e.g:

<pre>$ echo foo | setclip
$ getclip
foo</pre>

### zopfli

Gzip, but gzips better

## Stuff to delete

   * mlocate
   * durep

