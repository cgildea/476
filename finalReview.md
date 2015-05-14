###Chapter 13

Network Information Systems (13)

–Configuration (yp.conf, defaultdomain, rc.yp)

–Utilties (ypcat, ypmatch, ypwhich)

–Netgroups and nsswitch

2) Describe why nis in today’s world is an insecure accounting system. Then tell me why it is still in use.

NIS allows a root user on any computer that is part of the network to su to any account, giving them control of it.

This can be controled by limiting root access.

NIS makes it easier to change the same file on sever machines.

Still better than rdist.

-----------------
###Chapter 14

Network File System (14)
–How to export (exports)

file: /etc/exports

Purpose: say what is exported and to whom

Each line: A directory and a list of machines permitted to
mount the subtree under that directory
/harddisk lab17.net.cecs.csulb.edu(rw,sync)
/usr/info lab19.net.cecs.csulb.edu(ro) lab20(rw)
/usr/bin *.net.cecs.csulb.edu(ro)
/oops 134.139.136.64/255.255.255.192(rw)

sync: write immediate to keep files in sync
root_squash: root on the client machine doesn’t get root
priviledges
no_subtree_check: ensure file requests are in the exported
subtree
exportfs: A command similar to mount; it causes the
exports file to be reread. Pay attention command to the
options!


–How to import (fstab, mount)

/etc/fstab
lynx.net.cecs.csulb.edu:/u1 /lynx nfs bg,soft 0 0
server machine-name:/directory
Where to attach it locally
nfs: the type of file system
other options include ext2 or msdos
bg: if the mount times out, background it and keep trying
soft: report an error if an NFS operation times out
intr: allow a control C to abort an operation if it has
timed out
nolock: file locking is local to this machine and does not
attempt to lock against other NFS clients.

Caution: booting or a program will hang if you give
options which require an NFS operation to succeed and
the NFS server is down. (i.e. we recommend bg, soft,
intr).



authorize a subnet, what entry in the file?

fstab??

what command do you use to export the filesysytem

	exportfs


1) Give the command to restart the service that automounts NFS shares.


/etc/init.d/autofs restart
autofs  will consult a configuration file /etc/auto.master



22) Your machine hangs forever while booting up trying to mount NFS from a server that is offline. Assume
you can boot to network to fix this.

You boot from the network and set bg in /etc/fstab

bg backgrounds and keeps trying.

vim /etc/fstab
set bg
start debugging mount. Make sure that your server is authorized to boot via the network (IP is in the acceptable range for instacne)



20) You want to make your directory /rootload available to the machine master (read write). The user
root on this system must be able to write to this directory. Give the name of the file you need to modify,
the line you need to add to that file and the command you need to run to activate this.


In /etc/exports:
/rootload/ master (rw, sync)

exportfs -r

------------------------
###Chapter 15

Ftp (15)
–The difference between regular and anonmymous

A) Normal account: privileges = user log in
B) Anonymous: public repository or archive
Allow anyone to login (no password)
Allow them to copy files out.
Allowing anybody to deposit any thing is not a good idea

–The basic anonymous ftp security model (chroot)

Solution (some versions): chroot–change the root
directory
Normally you have access starting at / and going down.
You specify chroot /home/ftp
Unix behaves as if /home/ftp were the top directory.
You have access from there down.
After you chroot, for you that is considered /
For you: nothing outside this subdirectory exists
Our ftpd: if user logs in as anonymous, no password is
required and the ftpd does chroot ~ftp


–How to set up ftp.

/etc/ftpusers contains users that cannot ftp. Remove ftp from list to allow anonymous ftp.

–How to enable/disable the use of ftp by different
accounts.

/etc/ftpusers contains users that cannot ftp. Remove ftp from list to allow anonymous ftp.

–Dynamic libraries.

Statically linked: compiler embeds code into program
Advantage: runs regardless of libraries
Dynamically linked: at run time the library is found and
loaded.
Static advantages:
Never get “library not found”
Never get “wrong version of library”
Dynamic advantages:
Saves disk space (critical for big window handling
libraries)
Fixing library bugs does not require recompile of all
programs that used the old library version.

Dynamic problem:
Two programs need different versions of the same library.

ldd – list the dynamically loaded libraries the program
needs.
gcc – options to build static or dynamic linkage


11) The binaries checkitA and checkitB have the same behavior when run. checkitB is smaller than
checkitA. Why? (Hint: Source code for them is the same)

Dynamic libraries vs Staticily loaded libraries

checkitB is dynamic
CheckitA is staticily

18) You want to prohibit the user andy from using ftp. Give the file name and modification to do this.

/etc/ftpusers:
andy

23) Your machine is not accepting any ssh connections from anywhere even though the ssh service is started.

vim /etc/inetd.conf

vim /etc/rc.d/rc.sshd 
to make sure there are no weird settings

etc/rc.d/rc.sshd restart

iptables -L 
list the rules

------------------------
###Chapter 16

Install prep (16)
–How to examine and change the partitions on your disk.

	fdisk -l


–How to extract packages.

pkgtool
hit R to view installed packages, just dont remove any!

install/doinst.sh.


–The install is organized by themes (network, X11,
development).



–What are the steps in booting from the network.

1) The hardware (ROM BIOS) must support a net boot.
2) The BIOS must be set to allow net boot.
3) For our BIOS you need to hit the F12 key during the
boot sequence to tell the client to try booting from the
network first.


5) You want to partition your disks in preparation for an install. On your machines, you have 2 partitions.
Give the two partition type names and type numbers associated with them. Give the command you would
use to find out.

fdisk -l


-------------------------
###Chapter 17
Install (17)
–What are the steps you need to perform to install Linux.


you have taken down half the room, what did you do wrong?
you put your ip address as the gateway
you forgot to install something? how do you go back and fix it
you get an error on setup and got swap partition not found, you forogt to add swap!

6) When installing, what does disk set D contain? And if you forget to install something, what command
can you use to install something after a system rebuild?

Version control systems
pkgtool 


25) You’ve done something on your machine that caused every machine around you to stop being able to
reach cheetah (and you can’t reach it either).

You set your IP as the gateway.

ifconfig eth0 134.139.248.68 broadcast 134.139.248 netmask 255.255.255.252

----------------------------
###Chapter 18

Syslog and printing (18)
–Format and use of the printcap file.

On jaguar:
lp|jaguar:lp=/dev/lp0:\
:sd=/var/spool/lpd:\
:tr=\f:
the printer is called jaguar or lp or
lp – it is on the parallel port lp0
/var/spool/lp is the spool directory
tr – do a form feed after the job


cecs1|lp|cecs line printer:\
:lp=:rm=cheetah.net.cecs.csulb.edu:\
:rp=cecs1:sd=/var/spool/cecs1:
cecs1 or lp – what we call the printer
lp – no device for this printer
rm – the printer is attached to this remote machine
rp – what the remote machine calls the printer
(need not be the same name we give it)
sd – the spool directory. We have one locally for those
files to be sent to the remote machine. The remote
machine will also have one for those files it has received.


–How to setup access to a remote machine.

SEE ABOVE!

–How to control error logging (syslog.conf)

# Debugging information is logged here.
*.=debug                                                -/var/log/debug

–How to log to a remote machine

syslogd -r — enables remote machines to report log
entries
-h — if you received a remote log entry you are allowed
to forward it


18
how do you turn on syslog?

what does log level debug/error mean?
how do you forward it to a remote server?
full printcap entry from copter to host printer


7) You wish to log information from an application using the local3 facility and send that information to
log files on logsrv.demand.com. Give the name of the file you need to modify and the line you need to add
to that file.

In /etc/syslog.conf:
	local3.* @logsrv.demand.com
/etc/rc.d/rc.syslog restart

8) You want to be able to print to a local printer attached to your machine by default, and optionally be
able to print to a remote printer psvr1. a remote printer. What file should you modify? What lines do you
need in that file?

/etc/printcap:

lp|jaguar:lb=/dev/lp0:\
:sd=/var/spool/lpd:\
:tr=\f:

psvr1|cecs line printer:\
:lp=:rm=psvr1.net.cecs.csulb.edu:\
:rp=psvr1:sd=/var/spool/cecs68:


-----------------------------------
###Chapter 19

Mail (19)
–How does sendmail work (ASCII commands/requests)

sendmail is a smtp delivery program
Its behavior is governed by /etc/mail/sendmail.cf



–How do you control configuration (sendmail.cf).
–Masquerading, forwarding, smart hosts mail hubs.

masquerade:
You may modify the return address so that mail appears
to come from a different place. Usually you modify this
to your domain name or to the name of your mail
exchanger.
MASQUERADE_AS(cecs.csulb.edu)


FORWARD:

:0:otherlock
*
! newaddress@newplace.com
All (*) mail is Forwarded (!) to newaddress. The file
otherlock is used as a lock file


smart host:
You may have your non-local mail handled by a mail
exchanger. All non-local mail is sent to this machine and
relayed from there to the destination machine. (Note: the
exchanger needs to have relaying enabled for the
machines that it expects to relay for.) Useful if you are
behind a firewall and only the mail exchanger has
permission to send mail to external machines.
define(‘SMART_HOST’,‘mailserver.example.com’)



–How to use .procmailrc to filter mail.

mail filter:
INPUT_MAIL_FILTER(‘mimedefang’,
‘S=unix:/var/spool/mimedefang/mimedfang.sock,
F=T,T+S:5m;R:5m’)dnl
The filter name, the socket to talk to the filter on,
parameters for using the filter.
You start the filter as a separate daemon.


–How to use the .mc files to configure mail.

Ubuntu:
Makefile: causes the make command to rebuild the .cf
files from the .mc configurations.
1) Edit sendmail.mc and/or submit.mc.
2) make; make install-cf other cf’s will be built (but not
installed).
Slackware:
Configuration directory: /usr/share/sendmail/cf/cf
contains .mc files for lots sites (as examples).
Pick one or make one (use cp), edit it (say xx.mc)
Use the Build command to create the cf.
Build xx creates xx.cf from xx.mc
Then use cp to copy it into the /etc/mail (may also be
called /etc/sendmail) directory, giving it the correct name
(sendmail.cf or submit.cf)
In general:
when adding a FEATURE
add it at the end of the existing features
when adding a MAILER
add it at the end of the existing mailers
and so forth.
In some cases order matters in the .mc file.



10) You want to put all mail with the word Paycheck in its subject into a file called /home/charley/paychecks.
What file do you need to create, in what directory is that file created and what does that file need to contain?

In .procmailrc:
:0:PayCheck
* ^Subject.*Paycheck*
$/home/charley/paychecks


14) What is the difference between a mail transport agent and a mail user agent?

Mail User Agent:(Create/Edit)
edit messages
when you send it hands them to the MSA
the MSA then hands it to the MTA for transmission

Mail Transport Agent (Movement/flow)
Gets mail from a MSA or MTA and:
1) places it in a local file (users mail spool)
2) forwards it to another MTA (forwarded mail)
(watch out for SPAM)

-----------------------------
###Chapter 20 

SUID (20)
–How an SUID program works.
–How to set up an SUID program.

In addition to the rwx permissions there are permissions
to set the user and group ID.
-rws--x--x john student jpriv
-rw------- john student times
jpriv does a set user id to john.
When anyone runs jpriv the program has the priviledges
of john (not of them).
# jpriv
date >> times
Users cannot access times, but when they run jpriv the
program can access times (and it probably cannot write
into the user’s home directory).
chmod 4711 jpriv
You can also do a group set id (chmod 2711)
You switch to the group to which the file belongs


9) You wish to enable logging of successful logins. Give the file you need to change and the line needed to
enable this


In /etc/login.defs

#
# Enable logging of successful logins
#
LOG_OK_LOGINS           yes

#
# Enable logging and display of /var/log/lastlog login time info.
#
LASTLOG_ENAB            yes


19) You want force anyone running the buildit program to become part of the builders group. Describe
how you would set up a program to allow users to do this.

Set UID
chmod 4711 buildit

Set GID
chmod 2711 buildit



-----------------------------------
###Chatper 21

WWW (httpd) (21)
–How to set up a web server.
–What is in the configuration files.
–How to configure various web capabilities.


–How is the access (.htaccess) file used.

In .htaccess:
AuthName "MyCluster"
AuthType Basic
AuthUserFile /home/bob/public_html/limited/.htpasswd
require valid-user


4) How do you enable tilde home directories for use with Apache HTTPD? How do you restrict max’s home directory to not show? 

vim /etc/httpd/httpd.conf
Uncomment the Include /etc/httpd/extra/httpd-userdir.conf
	<Directory "/home/ftp/">
    Options FollowSymLinks
    AllowOverride None
    Order allow,deny
    Deny from all
</Directory>


15)	You want no CGIs allowed to /var/www/thru, but you do want CGI allowed inside /var/www/thru/cgi. Give the httpd.conf entries to do this. 
<Directory "/var/www/thru">
    AllowOverride None
    Options None
    Order allow,deny
    Allow from all
</Directory>
<Directory "/var/www/thru/cgi">
    AllowOverride FileInfo AuthConfig Limit Indexes
    Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec ExecCGI Includes
    AddHandler cgi-script .cgi
    AddType text/html .shtml
    AddOutputFilter INCLUDE .shtml
    <Limit GET POST OPTIONS>
        Order allow,deny
        Allow from all
    </Limit>
</Directory>


-----------------------------------
###Chapter 22

DNS service (22)
–How DNS servers work.

SEE LECTURE

–Configuration files and contents.

SEE HOMEWORK

–How to use nslookup to test a particular server.

nslookup test01.net68.cecs.csulb.edu lab68
Server:		lab68
Address:	134.139.248.68#53

Name:	test01.net68.cecs.csulb.edu
Address: 192.168.1.1


12)	There are two machines for which dns1.lbcc.edu (130.1.1.2) supplies name service: hop1.lbsu.edu (151.34.22.10) and hop2.lbsu.edu (151.34.22.11). Give the entire reverse zone file for lbsu.edu. 
$TTL  86400
@       IN      SOA     lbsu.edu. root.lbsu.edu.  (
                                      2011032500 ; Serial
                                      28800      ; Refresh
                                      14400      ; Retry
                                      3600000    ; Expire
                                      86400 )    ; Minimum
              IN      NS      dns1.lbcc.edu.

IN PTR hop1.lbsu.edu
IN PTR hop2.lbsu.edu
13)	Give the top line in the forward zone file for dns1.lbcc.edu. 
$TTL  86400
@       IN      SOA     lbsu.edu. root.lbsu.edu.  (
                                      2011032500 ; Serial
                                      28800      ; Refresh
                                      14400      ; Retry
                                      3600000    ; Expire
                                      86400 )    ; Minimum
              IN      NS      dns1.lbcc.edu.
        IN      A       130.1.1.2
hop1 IN A 151.34.22.10
hop2 IN A 151.34.22.11




-----------------------------------
###Chapter 23

Rdist (23)
–How remote distribution works.

rdist: remote file distribution program
From a designated management machine:
distribute files to a list of machines
run install programs on those machines
rdist [-f distfile] [-m host] [name ...]
Run this program on the management machine
defaults to a file called distfile in the local directory of
the management machine.
usually: rdist -f mydistfile
Action: update all files and directories listed in distfile
Administrator: plan your update, place command in
mydistfile run with mydistfile.

–How to use the .rhosts and distfiles.

You can not rdist to a machine unless you have
permission.
operates off rlogin/rcp permission (.rhosts)
rdist requires rshd to be enabled in inetd.conf

To install files to root@unix70
using the root login on jaguar:
.rhosts (for root on unix70)
jaguar.net.cecs.csulb.edu root
To install files to www@lab30
using the css476zz login on jaguar:
.rhosts (for www on lab30)
jaguar.net.cecs.csulb.edu css476zz
Client machines must have rshd enabled
(uncommented in inetd.conf)


Side note:
if your management machine gets compromised,
all machines are compromised


16) You wish to install an updated version of the command /bin/ping on the remote machine monitor12.
You then need to change ownership of it to root and enable setuid on it. Give the commands/files necessary
to do this.

This is my dist file
/bin/ping -> monitor12
        install /bin/ping ;
        special "chown root.0 /bin/ping" ;
        special "chmod 4711 /bin/ping" ;


-------------------------------------
###Chapter 24

Samba (24)
–How to configure samba.

SEE LECTURE

–How to protect directories.

browsable = no
— the home directories do not appear in the Windows
networking panel

hosts allow = 134.139.
— can restrict access

security = user
— username and password required (or = share)



17) You want to make a directory called /data/disks/ on your Linux machine available to all machines
running Microsoft Windows as disks. What file do you need to change? What lines do you need to add to
that file?

In /etc/samba/smb.conf:
[diskshare]
   comment = disk stuff
   path = /data/disks
   valid users = 134.139.
   public = yes
   readonly = yes
   writable = no
   printable = no
   create mask = 0765


24) A windows machine gets a permission denied error when trying to map to a share on your machine

vim /etc/samba/smb.conf:

check that the valid users is correct.


-------------------------------------
###Chapter 25


3) You wish to give user andy a soft quota of 500MB. How do you do this?

quotacheck -a -m

in /etc/fstab:
/dev/sda1        /                ext2        usrquota         1   1

equota -u andy
skipping 4 old session files
reading /tmp//EdP.abnzZwh
Read /tmp//EdP.abnzZwh, 3 lines, 216 chars
                                          Disk quotas for user andy (uid 13101):
  Filesystem                   blocks       soft       hard     inodes     soft     hard
  /dev/root                       104        500       	  0         22        0        0




-------------------------------------
###Chatper 26

DHCP/network boot(26)
–What is in the dhcp configuration file?
–How to set IP numbers, netmasks, and gateways.
–How to set up tftp.
–How to configure a network boot server.
–How to start in.tftpd
–How do you configure a PXE

% Project 26 --
21) When the machine 01:02:03:04:05:06 boots from the network it is to be assigned the name twist33
and the IP address 180.45.23.9 and boot /tftpboot/syslinux. What entries must be in what file on the
dhcpd server for this to happen?









