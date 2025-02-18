```bash
root@fax /u/l/s/hylafax-7.0.10# ./configure

Configuring HylaFAX (tm) (aka FlexFAX) 7.0.10.

If configure does the wrong thing, check the file config.log for
information that may help you understand what went wrong.

Reading site-wide parameters from ./config.site.
Gosh, aren't you lucky to have a x86_64-unknown-linux-gnu system!
Using /usr/bin/gcc for a C compiler (set CC to override).
Looks like /usr/bin/gcc supports the -g option.
Using " -g" for C compiler options.
Looks like /usr/bin/gcc has an ANSI C preprocessor.
... but __ANSI_CPP__ is not automatically defined, will compensate.
Looks like /usr/bin/gcc supports the -M option for generating make dependencies.
Using /usr/bin/g++ for a C++ compiler (set CXX to override).
Looks like /usr/bin/g++ supports the -g option.
Using " -g" for C++ compiler options.
Looks like /usr/bin/g++ has an ANSI C preprocessor.
... but __ANSI_CPP__ is not automatically defined, will compensate.
Using /usr/bin/make to configure the software.
Using "include file" syntax for Makefiles.
Looks like make supports "sinclude" for conditional includes.
Using /usr/bin/bash to process command scripts.
Checking for regular expression library support
... found. Using system regular expression support.
Checking for PAM (Pluggable Authentication Module) support
... found. Enabling PAM support
Checking for OpenSSL library support
... found. Enabling OpenSSL library support
Checking for version-flexible OpenSSL library support
... found. Enabling version-flexible OpenSSL library support.
Checking for JBIG library support
... found. Enabling JBIG support
Checking for JPEG library support
... found. Enabling JPEG library support
Checking for Little CMS library support
... not found. Disabling Little CMS support
Checking for LDAP (Lightweight Directory Access Protocol) support
... not found. Disabling LDAP support
Checking for PODOFO library support
... not found. Disabling PODOFO support
Looks like -lcrypt is needed for crypt.
Looks like -lutil is needed for wtmp file logging.
Looks like -lm is the library for math functions.

Creating port.h with necessary definitions.
... using call-by-reference for TIOCMBIS ioctl
... constrain client IDs to be <= 60002
... configure use of <stdint.h>
... configure use of <sys/select.h>
... use (sig_t) for sigaction handler type
... use (sig_t) for signal handler type
... configure use of mmap for memory-mapped files
... configure use of sysconf
... configure use of ulimit
... configure use of getdtablesize
... add #define for howmany
... add function prototype for sigvec
... configure use of fchown
... configure use of fchmod
... configure use of struct tm timezone information
... configure use of <locale.h> (internationalization support)
... configure use of <langinfo.h> (internationalization support)
... configure use of <paths.h>
... configure use of logwtmp (BSD-style wtmp logging)
... configure use of logout (BSD-style utmp support)
... configure use of <utmp.h> (normal utmp interface)
... configure use of extended exit status in utmp
... configure use of POSIX realtime process control interface
... configure use of <crypt.h>
... checking TIFF library version
  Found tiffio.h version 20201219
  Found libtiff version 4.2
... add declaration for tiff_runlen_t and tiff_offset_t
... checking PAM library version
Done creating port.h.

Checking system libraries for functionality to emulate.
Done checking system libraries.

Checking ZLIB support.
Using pre-built ZLIB library -lz
Done checking ZLIB support.

Checking TIFF support.
Using TIFF binary files from /usr/bin
Checking JBIG-in-TIFF conversion support.
JBIG-in-TIFF conversion support found.
Done checking TIFF support.

Checking for Dynamic Shared Object (DSO) support.
Looks like your system supports LINUX-style DSOs.

Selecting programs used during installation and operation.
Looks like /usr/bin/mawk should be used in command scripts.
WARNING, could not locate sendmail on your system.

Beware that the mail notification work done by this software uses
sendmail-specific command line options.  If you do not have a
sendmail-compatible mailer things will break.
Using /usr/lib/sendmail to deliver mail.
Looks like /usr/bin/mkfifo creates FIFO special files.
Looks like /usr/bin/mv supports the -f option to force a move.
Looks like /usr/bin/ln supports the -s option to create a symbolic link.
Looks like a SysV-style init is used, enabling installation of startup code.
Looks like SysV init scripts go in /etc/init.d.
Done selecting programs.

Selecting default HylaFAX configuration parameters.

Using uid uucp and gid uucp for controlling access to fax stuff.
Using uid bin and gid bin for installing programs.
Using MSB2LSB bit order for your x86_64 cpu.
Looks like you need SysV getty support.
Looks like /sbin/agetty is the program to exec for a data call.
WARNING, no vgetty program found to handle a voice call, using /bin/vgetty.
WARNING, no egetty program found, using /bin/egetty.
Looks like you use ascii-style UUCP lock files.
Looks like UUCP lock files go in /var/lock.
Looks like the gs imager package should be used.
Looks like /usr/bin/gs is the PostScript RIP to use.
Setting the Fontmap path to /usr/share/ghostscript/9.53.3/Resource/Init:/usr/share/ghostscript/9.53.3/lib:/usr/share/ghostscript/9.53.3/Resource/Font:/usr/share/ghostscript/fonts:/var/lib/ghostscript/fonts:/usr/share/cups/fonts:/usr/share/ghostscript/fonts:/usr/local/lib/ghostscript/fonts:/usr/share/fonts
Looks like font metric information goes in /usr/share/ghostscript/9.53.3/Resource/Init:/usr/share/ghostscript/9.53.3/lib:/usr/share/ghostscript/9.53.3/Resource/Font:/usr/share/ghostscript/fonts:/var/lib/ghostscript/fonts:/usr/share/cups/fonts:/usr/share/ghostscript/fonts:/usr/local/lib/ghostscript/fonts:/usr/share/fonts.
Looks like manual pages go in /usr/share/man.
Looks like manual pages should be installed with bsd-source-cat.
Press Return to Continue 


HylaFAX configuration parameters (part 1 of 2) are:

[ 1] Directory for applications:        /usr/local/bin
[ 2] Directory for lib data files:      /usr/local/lib/fax
[ 3] Directory for lib executables:     /usr/local/sbin
[ 4] Directory for system apps:  	/usr/local/sbin
[ 5] Directory for manual pages:        /usr/share/man
[ 6] Directory for spooling:            /var/spool/hylafax
[ 7] Directory for uucp lock files:     /var/lock
[ 8] Uucp lock file scheme:             ascii
[ 9] PostScript imager package:         gs
[10] PostScript imager program:         /usr/bin/gs
[11] Manual page installation scheme:   bsd-source-cat
[12] Default page size:                 North American Letter
[13] Default vertical res (lpi):        98

Are these ok [yes]? 12
Default page size [North American Letter]? A4

HylaFAX configuration parameters (part 1 of 2) are:

[ 1] Directory for applications:        /usr/local/bin
[ 2] Directory for lib data files:      /usr/local/lib/fax
[ 3] Directory for lib executables:     /usr/local/sbin
[ 4] Directory for system apps:  	/usr/local/sbin
[ 5] Directory for manual pages:        /usr/share/man
[ 6] Directory for spooling:            /var/spool/hylafax
[ 7] Directory for uucp lock files:     /var/lock
[ 8] Uucp lock file scheme:             ascii
[ 9] PostScript imager package:         gs
[10] PostScript imager program:         /usr/bin/gs
[11] Manual page installation scheme:   bsd-source-cat
[12] Default page size:                 ISO A4
[13] Default vertical res (lpi):        98

Are these ok [yes]? 

HylaFAX configuration parameters (part 2 of 2) are:

[14] Location of getty program:         /sbin/agetty
[15] Location of voice getty program:   /bin/vgetty
[16] Location of sendmail program:      /usr/lib/sendmail
[17] Location of TIFF tools:            /usr/bin
[18] Location of SysV init scripts:	/etc/init.d
[19] Location of SysV start scripts:	../rc2.d ../rc3.d ../rc4.d ../rc5.d
[20] Location of SysV stop scripts:	../rc0.d ../rc1.d ../rc6.d
[21] Name of SysV start script:		S97hylafax
[22] Name of SysV stop script:		K05hylafax
[23] Init script starts faxq:		yes
[24] Init script starts hfaxd		yes
[25] Start paging protocol:		no

WARNING, /usr/lib/sendmail does not seem to be an executable program;
         you may need to correct this before starting up the fax server.
ls: cannot access '/usr/lib/sendmail': No such file or directory

Are these ok [yes]? ^C⏎                                                                                                                                                                                                                                                                                                       root@fax /u/l/s/hylafax-7.0.10 [1]# apt install -y sendmail
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  liblockfile1 lockfile-progs procmail sendmail-base sendmail-bin sendmail-cf sensible-mda
Suggested packages:
  sendmail-doc rmail logcheck resolvconf sasl2-bin
The following NEW packages will be installed:
  liblockfile1 lockfile-progs procmail sendmail sendmail-base sendmail-bin sendmail-cf sensible-mda
0 upgraded, 8 newly installed, 0 to remove and 0 not upgraded.
Need to get 1,963 kB of archives.
After this operation, 4,466 kB of additional disk space will be used.
Get:1 http://deb.debian.org/debian bullseye/main amd64 liblockfile1 amd64 1.17-1+b1 [17.0 kB]
Get:2 http://deb.debian.org/debian bullseye/main amd64 lockfile-progs amd64 0.1.18 [10.4 kB]
Get:3 http://deb.debian.org/debian bullseye/main amd64 sendmail-base all 8.15.2-22+deb11u3 [345 kB]
Get:4 http://deb.debian.org/debian bullseye/main amd64 sendmail-cf all 8.15.2-22+deb11u3 [293 kB]
Get:5 http://deb.debian.org/debian bullseye/main amd64 sendmail-bin amd64 8.15.2-22+deb11u3 [700 kB]
Get:6 http://deb.debian.org/debian bullseye/main amd64 procmail amd64 3.22-26+deb11u1 [144 kB]
Get:7 http://deb.debian.org/debian bullseye/main amd64 sensible-mda amd64 8.15.2-22+deb11u3 [227 kB]
Get:8 http://deb.debian.org/debian bullseye/main amd64 sendmail all 8.15.2-22+deb11u3 [225 kB]
Fetched 1,963 kB in 1s (3,166 kB/s)
Selecting previously unselected package liblockfile1:amd64.
(Reading database ... 47906 files and directories currently installed.)
Preparing to unpack .../0-liblockfile1_1.17-1+b1_amd64.deb ...
Unpacking liblockfile1:amd64 (1.17-1+b1) ...
Selecting previously unselected package lockfile-progs.
Preparing to unpack .../1-lockfile-progs_0.1.18_amd64.deb ...
Unpacking lockfile-progs (0.1.18) ...
Selecting previously unselected package sendmail-base.
Preparing to unpack .../2-sendmail-base_8.15.2-22+deb11u3_all.deb ...
Unpacking sendmail-base (8.15.2-22+deb11u3) ...
Selecting previously unselected package sendmail-cf.
Preparing to unpack .../3-sendmail-cf_8.15.2-22+deb11u3_all.deb ...
Unpacking sendmail-cf (8.15.2-22+deb11u3) ...
Selecting previously unselected package sendmail-bin.
Preparing to unpack .../4-sendmail-bin_8.15.2-22+deb11u3_amd64.deb ...
Unpacking sendmail-bin (8.15.2-22+deb11u3) ...
Selecting previously unselected package procmail.
Preparing to unpack .../5-procmail_3.22-26+deb11u1_amd64.deb ...
Unpacking procmail (3.22-26+deb11u1) ...
Selecting previously unselected package sensible-mda.
Preparing to unpack .../6-sensible-mda_8.15.2-22+deb11u3_amd64.deb ...
Unpacking sensible-mda (8.15.2-22+deb11u3) ...
Selecting previously unselected package sendmail.
Preparing to unpack .../7-sendmail_8.15.2-22+deb11u3_all.deb ...
Unpacking sendmail (8.15.2-22+deb11u3) ...
Setting up sendmail-cf (8.15.2-22+deb11u3) ...
Setting up procmail (3.22-26+deb11u1) ...
Setting up liblockfile1:amd64 (1.17-1+b1) ...
Setting up lockfile-progs (0.1.18) ...
Setting up sendmail-base (8.15.2-22+deb11u3) ...
adduser: Warning: The home directory `/var/lib/sendmail' does not belong to the user you are currently creating.
Setting up sendmail-bin (8.15.2-22+deb11u3) ...
update-alternatives: using /usr/libexec/sendmail/sendmail to provide /usr/sbin/sendmail-mta (sendmail-mta) in auto mode
update-alternatives: using /usr/libexec/sendmail/sendmail to provide /usr/sbin/sendmail-msp (sendmail-msp) in auto mode

You are doing a new install, or have erased /etc/mail/sendmail.mc.
If you've accidentaly erased /etc/mail/sendmail.mc, check /var/backups.

I am creating a safe, default sendmail.mc for you and you can
run sendmailconfig later if you need to change the defaults.

Updating sendmail environment ...
Validating configuration.
Writing configuration to /etc/mail/sendmail.conf.
Writing /etc/cron.d/sendmail.
Could not open /etc/mail/databases(No such file or directory), creating it.
Could not open /etc/mail/sendmail.mc(No such file or directory)
Reading configuration from /etc/mail/sendmail.conf.
Validating configuration.
Writing configuration to /etc/mail/sendmail.conf.
Writing /etc/cron.d/sendmail.
Turning off Host Status collection
Could not open /etc/mail/databases(No such file or directory), creating it.
Reading configuration from /etc/mail/sendmail.conf.
Validating configuration.
Creating /etc/mail/databases...

Checking filesystem, this may take some time - it will not hang!
  ...   Done.
 
Checking for installed MDAs...
Adding link for newly extant program (mail.local)
Adding link for newly extant program (procmail)
sasl2-bin not installed, not configuring sendmail support.

To enable sendmail SASL2 support at a later date, invoke "/usr/share/sendmail/update_auth"

 
Creating/Updating SSL(for TLS) information
Creating /etc/mail/tls/starttls.m4...
Creating SSL certificates for sendmail.
Generating DSA parameters, 2048 bit long prime
This could take some time
...+...............+..+...+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*
..............+...................+....+..................+......+..+................+......+.+......................+...................+..+...+......+...........+.+..............+.......+..........+............+....+..+.+.+..+.+..+..+.......+...+........+..................+.+................+.....+.......+...+.....
.+................+...+...+..+...+........+......+.+......+.+................+..+....+.+.....+..........................+.......+.............+...+...+....................+...+......+.......................+..................+...+.+.....+...+.........+.+.............+............+.+.......................+...+.......
.......+...........+..............+...............+........+..................+....+................+.+...........+......+...........+.....................+.................+.+..........+.........+.................+..+..............+........+.......+.....+.......+......+...+..............+......+.+......+........+...
..........+.........................+.+..+...+.....+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*
Generating RSA private key, 2048 bit long modulus (2 primes)
.......+++++
...............................+++++
e is 65537 (0x010001)

*** *** *** WARNING *** WARNING *** WARNING *** WARNING *** *** ***

Everything you need to support STARTTLS (encrypted mail transmission
and user authentication via certificates) is installed and configured
but is *NOT* being used.

To enable sendmail to use STARTTLS, you need to:
1) Add this line to /etc/mail/sendmail.mc and optionally
   to /etc/mail/submit.mc:
  include(`/etc/mail/tls/starttls.m4')dnl
2) Run sendmailconfig
3) Restart sendmail


Updating /etc/hosts.allow, adding "sendmail: all".

Please edit /etc/hosts.allow and check the rules location to
make sure your security measures have not been overridden -
it is common to move the sendmail:all line to the *end* of
the file, so your more selective rules take precedence.
Checking {sendmail,submit}.mc and related databases...
Reading configuration from /etc/mail/sendmail.conf.
Validating configuration.
Creating /etc/mail/databases...
Reading configuration from /etc/mail/sendmail.conf.
Validating configuration.
Creating /etc/mail/databases...
Reading configuration from /etc/mail/sendmail.conf.
Validating configuration.
Creating /etc/mail/Makefile...
Reading configuration from /etc/mail/sendmail.conf.
Validating configuration.
Writing configuration to /etc/mail/sendmail.conf.
Writing /etc/cron.d/sendmail.
Disabling HOST statistics file(/var/lib/sendmail/host_status).
Creating /etc/mail/sendmail.cf...
Creating /etc/mail/submit.cf...
Informational: confCR_FILE file empty: /etc/mail/relay-domains
Warning: confCT_FILE source file not found: /etc/mail/trusted-users
 it was created
Informational: confCT_FILE file empty: /etc/mail/trusted-users
Warning: confCW_FILE source file not found: /etc/mail/local-host-names
 it was created
Warning: access_db source file not found: /etc/mail/access
 it was created
Updating /etc/mail/access...
Linking /etc/aliases to /etc/mail/aliases
Informational: ALIAS_FILE file empty: /etc/mail/aliases
Updating /etc/mail/aliases...
/etc/mail/aliases: 0 aliases, longest 0 bytes, 0 bytes total
 
Warning: 3 database(s) sources
	were not found, (but were created)
	please investigate.
Setting up sensible-mda (8.15.2-22+deb11u3) ...
Setting up sendmail (8.15.2-22+deb11u3) ...
Processing triggers for libc-bin (2.31-13+deb11u11) ...
Processing triggers for man-db (2.9.4-2) ...
root@fax /u/l/s/hylafax-7.0.10# ./configure

Configuring HylaFAX (tm) (aka FlexFAX) 7.0.10.

If configure does the wrong thing, check the file config.log for
information that may help you understand what went wrong.

Reading site-wide parameters from ./config.site.
Do they really still make x86_64-unknown-linux-gnu systems?!
Using /usr/bin/gcc for a C compiler (set CC to override).
Looks like /usr/bin/gcc supports the -g option.
Using " -g" for C compiler options.
Looks like /usr/bin/gcc has an ANSI C preprocessor.
... but __ANSI_CPP__ is not automatically defined, will compensate.
Looks like /usr/bin/gcc supports the -M option for generating make dependencies.
Using /usr/bin/g++ for a C++ compiler (set CXX to override).
Looks like /usr/bin/g++ supports the -g option.
Using " -g" for C++ compiler options.
Looks like /usr/bin/g++ has an ANSI C preprocessor.
... but __ANSI_CPP__ is not automatically defined, will compensate.
Using /usr/bin/make to configure the software.
Using "include file" syntax for Makefiles.
Looks like make supports "sinclude" for conditional includes.
Using /usr/bin/bash to process command scripts.
Checking for regular expression library support
... found. Using system regular expression support.
Checking for PAM (Pluggable Authentication Module) support
... found. Enabling PAM support
Checking for OpenSSL library support
... found. Enabling OpenSSL library support
Checking for version-flexible OpenSSL library support
... found. Enabling version-flexible OpenSSL library support.
Checking for JBIG library support
... found. Enabling JBIG support
Checking for JPEG library support
... found. Enabling JPEG library support
Checking for Little CMS library support
... not found. Disabling Little CMS support
Checking for LDAP (Lightweight Directory Access Protocol) support
... not found. Disabling LDAP support
Checking for PODOFO library support
... not found. Disabling PODOFO support
Looks like -lcrypt is needed for crypt.
Looks like -lutil is needed for wtmp file logging.
Looks like -lm is the library for math functions.

Using previously created port.h.

Checking system libraries for functionality to emulate.
Done checking system libraries.

Checking ZLIB support.
Using pre-built ZLIB library -lz
Done checking ZLIB support.

Checking TIFF support.
Using TIFF binary files from /usr/bin
Checking JBIG-in-TIFF conversion support.
JBIG-in-TIFF conversion support found.
Done checking TIFF support.

Checking for Dynamic Shared Object (DSO) support.
Looks like your system supports LINUX-style DSOs.

Selecting programs used during installation and operation.
Looks like /usr/bin/mawk should be used in command scripts.
Looks like /sbin/sendmail should be used to deliver mail.
Looks like /usr/bin/mkfifo creates FIFO special files.
Looks like /usr/bin/mv supports the -f option to force a move.
Looks like /usr/bin/ln supports the -s option to create a symbolic link.
Looks like a SysV-style init is used, enabling installation of startup code.
Looks like SysV init scripts go in /etc/init.d.
Done selecting programs.

Selecting default HylaFAX configuration parameters.

Using uid uucp and gid uucp for controlling access to fax stuff.
Using uid bin and gid bin for installing programs.
Using MSB2LSB bit order for your x86_64 cpu.
Looks like you need SysV getty support.
Looks like /sbin/agetty is the program to exec for a data call.
WARNING, no vgetty program found to handle a voice call, using /bin/vgetty.
WARNING, no egetty program found, using /bin/egetty.
Looks like you use ascii-style UUCP lock files.
Looks like UUCP lock files go in /var/lock.
Looks like the gs imager package should be used.
Looks like /usr/bin/gs is the PostScript RIP to use.
Setting the Fontmap path to /usr/share/ghostscript/9.53.3/Resource/Init:/usr/share/ghostscript/9.53.3/lib:/usr/share/ghostscript/9.53.3/Resource/Font:/usr/share/ghostscript/fonts:/var/lib/ghostscript/fonts:/usr/share/cups/fonts:/usr/share/ghostscript/fonts:/usr/local/lib/ghostscript/fonts:/usr/share/fonts
Looks like font metric information goes in /usr/share/ghostscript/9.53.3/Resource/Init:/usr/share/ghostscript/9.53.3/lib:/usr/share/ghostscript/9.53.3/Resource/Font:/usr/share/ghostscript/fonts:/var/lib/ghostscript/fonts:/usr/share/cups/fonts:/usr/share/ghostscript/fonts:/usr/local/lib/ghostscript/fonts:/usr/share/fonts.
Looks like manual pages go in /usr/share/man.
Looks like manual pages should be installed with bsd-source-cat.
Press Return to Continue 


HylaFAX configuration parameters (part 1 of 2) are:

[ 1] Directory for applications:        /usr/local/bin
[ 2] Directory for lib data files:      /usr/local/lib/fax
[ 3] Directory for lib executables:     /usr/local/sbin
[ 4] Directory for system apps:  	/usr/local/sbin
[ 5] Directory for manual pages:        /usr/share/man
[ 6] Directory for spooling:            /var/spool/hylafax
[ 7] Directory for uucp lock files:     /var/lock
[ 8] Uucp lock file scheme:             ascii
[ 9] PostScript imager package:         gs
[10] PostScript imager program:         /usr/bin/gs
[11] Manual page installation scheme:   bsd-source-cat
[12] Default page size:                 North American Letter
[13] Default vertical res (lpi):        98

Are these ok [yes]? 12
Default page size [North American Letter]? A4

HylaFAX configuration parameters (part 1 of 2) are:

[ 1] Directory for applications:        /usr/local/bin
[ 2] Directory for lib data files:      /usr/local/lib/fax
[ 3] Directory for lib executables:     /usr/local/sbin
[ 4] Directory for system apps:  	/usr/local/sbin
[ 5] Directory for manual pages:        /usr/share/man
[ 6] Directory for spooling:            /var/spool/hylafax
[ 7] Directory for uucp lock files:     /var/lock
[ 8] Uucp lock file scheme:             ascii
[ 9] PostScript imager package:         gs
[10] PostScript imager program:         /usr/bin/gs
[11] Manual page installation scheme:   bsd-source-cat
[12] Default page size:                 ISO A4
[13] Default vertical res (lpi):        98

Are these ok [yes]? 

HylaFAX configuration parameters (part 2 of 2) are:

[14] Location of getty program:         /sbin/agetty
[15] Location of voice getty program:   /bin/vgetty
[16] Location of sendmail program:      /sbin/sendmail
[17] Location of TIFF tools:            /usr/bin
[18] Location of SysV init scripts:	/etc/init.d
[19] Location of SysV start scripts:	../rc2.d ../rc3.d ../rc4.d ../rc5.d
[20] Location of SysV stop scripts:	../rc0.d ../rc1.d ../rc6.d
[21] Name of SysV start script:		S97hylafax
[22] Name of SysV stop script:		K05hylafax
[23] Init script starts faxq:		yes
[24] Init script starts hfaxd		yes
[25] Start paging protocol:		no
Are these ok [yes]? 

Creating defs from ./defs.in
Creating config.h from ./config.h.in
Creating rules from ./rules.in
Creating Makefile from ./Makefile.in
Creating config/Makefile from ./config/Makefile.in
Creating etc/Makefile from ./etc/Makefile.in
Creating faxalter/Makefile from ./faxalter/Makefile.in
Creating faxcover/Makefile from ./faxcover/Makefile.in
Creating faxd/Makefile from ./faxd/Makefile.in
Creating faxmail/Makefile from ./faxmail/Makefile.in
Creating faxrm/Makefile from ./faxrm/Makefile.in
Creating faxstat/Makefile from ./faxstat/Makefile.in
Creating hfaxd/Makefile from ./hfaxd/Makefile.in
Creating man/Makefile from ./man/Makefile.in
Creating sendfax/Makefile from ./sendfax/Makefile.in
Creating sendpage/Makefile from ./sendpage/Makefile.in
Creating util/Makefile from ./util/Makefile.in
Creating faxcover/edit-faxcover.sh from ./faxcover/edit-faxcover.sh.in
Creating faxmail/application-pdf.sh from ./faxmail/application-pdf.sh.in
Creating faxmail/application-octet-stream.sh from ./faxmail/application-octet-stream.sh.in
Creating faxmail/application-binary.sh from ./faxmail/application-binary.sh.in
Creating faxmail/image-tiff.sh from ./faxmail/image-tiff.sh.in
Creating port/Makefile from ./port/Makefile.in
Creating port/install.sh from ./port/install.sh.in
Creating port/version.c from ./port/version.c.in
Creating etc/faxsetup.sh from ./etc/faxsetup.sh.in
Creating etc/faxsetup.linux from ./etc/faxsetup.linux.in
Creating etc/faxaddmodem.sh from ./etc/faxaddmodem.sh.in
Creating etc/probemodem.sh from ./etc/probemodem.sh.in
Creating etc/hylafax from ./etc/hylafax.in
Creating util/xferfaxstats.sh from ./util/xferfaxstats.sh.in
Creating util/recvstats.sh from ./util/recvstats.sh.in
Creating util/faxcron.sh from ./util/faxcron.sh.in
Creating util/pagesizes from ./util/pagesizes.in
Creating util/archive.sh from ./util/archive.sh.in
Creating util/dictionary.sh from ./util/dictionary.sh.in
Creating util/common-functions.sh from ./util/common-functions.sh.in
Creating util/faxrcvd.sh from ./util/faxrcvd.sh.in
Creating util/mkcover.sh from ./util/mkcover.sh.in
Creating util/notify.sh from ./util/notify.sh.in
Creating util/pcl2fax.sh from ./util/pcl2fax.sh.in
Creating util/pollrcvd.sh from ./util/pollrcvd.sh.in
Creating util/ps2fax.dps.sh from ./util/ps2fax.dps.sh.in
Creating util/ps2fax.gs.sh from ./util/ps2fax.gs.sh.in
Creating util/pdf2fax.gs.sh from ./util/pdf2fax.gs.sh.in
Creating util/ps2fax.imp.sh from ./util/ps2fax.imp.sh.in
Creating util/tiff2fax.sh from ./util/tiff2fax.sh.in
Creating util/wedged.sh from ./util/wedged.sh.in
Creating util/tiff2pdf.sh from ./util/tiff2pdf.sh.in
Creating util/qp-encode.awk from ./util/qp-encode.awk.in
Creating util/rfc2047-encode.awk from ./util/rfc2047-encode.awk.in
Creating util/dict-de from ./util/dict-de.in
Creating util/dict-en from ./util/dict-en.in
Creating util/dict-es from ./util/dict-es.in
Creating util/dict-he from ./util/dict-he.in
Creating util/dict-it from ./util/dict-it.in
Creating util/dict-fr from ./util/dict-fr.in
Creating util/dict-nl_BE from ./util/dict-nl_BE.in
Creating util/dict-pl from ./util/dict-pl.in
Creating util/dict-pt from ./util/dict-pt.in
Creating util/dict-pt_BR from ./util/dict-pt_BR.in
Creating util/dict-ro from ./util/dict-ro.in
Creating util/dict-ru from ./util/dict-ru.in
Creating util/dict-sr from ./util/dict-sr.in
Creating util/dict-tr from ./util/dict-tr.in
Creating util/dict-uk from ./util/dict-uk.in
Creating util/dict-zh from ./util/dict-zh.in
Creating pkg/Makefile from ./pkg/Makefile.in
Creating pkg/cpkginfo from ./pkg/cpkginfo.in
Creating pkg/cproto.stub from ./pkg/cproto.stub.in
Creating pkg/crequest from ./pkg/crequest.in
Creating pkg/make_proto.sh from ./pkg/make_proto.sh.in
Creating pkg/postinstall from ./pkg/postinstall.in
Creating pkg/postremove from ./pkg/postremove.in
Creating pkg/spkginfo from ./pkg/spkginfo.in
Creating pkg/sproto.stub from ./pkg/sproto.stub.in
Creating pkg/srequest from ./pkg/srequest.in
Creating port/mkdepend from ./port/mkdepend.in
Done.
root@fax /u/l/s/hylafax-7.0.10# 
```