TC-C-FAX :

Telecos Crappy Fax 

Very wip... lol 

# TC-C-FAX : Telecos Crappy Fax Gateway
So you want a Fax Gateway ? No ? Do you even know what that is ? Also no? well let me explain.

This project contains all files needed for setting up TC-C-FAX
A fax server that is highly integrated with E-Mail!

What it does ?
It listens for new E-Mails on an E-Mail defined by you. Once one arrives it gives the sender (if unknown) an ID and gives the E-Mail an ID too.
Prints the E-Mail including sender ID and E-Mail ID on your actual Fax machine (can be any fax no matter if Virtual or Real aslong as its a dialable Asterisk Extension)
Now thats all nice and stuff but how do you reply on your fax machine to an E-Mail ? Ah you see thats where the ID system comes in handy!
On you actual fax dial its extension with the E-Mail or Sender ID appended to the extension number and evoila your Fax is sent either as a new E-Mail to the Sender ID you gave or as a reply to E-Mail ID.

Now as of now this is just the concept of how it is supposed to work, this is not actually done yet. Once that all somewhat works there should be a release available.

# Getting Started :

## What you will need :
- An Asterisk Server with an IAX extension set up for the Fax Gateway
- Some way of testing your Fax Gateway (can be a virtual fax or a real one aslong as you can dial it from the IAX extension)
- An E-Mail account without 2FA
- Some Virtualization Platform for the Debian 11 VM needed for this.


### Setting up a Debian 11 VM
You will need Debian 11! Anything newer I was not able to get running and even Debian 11 is a stretch as to how recent it can be. I also don't recommend doing this in a container as of now. If you want to do so your on your own.

As to the Debian VM its nothing special just default no desktop just SSH and standard system utils.

Make sure to have a valid FQDN and preferably have a static IP

### Preparing Debian 11 VM
1. SSH into your VM
```
ssh user@ip-address
```
1. Sign in to root account
```bash
su
```
1. Set Static IP (Optional if fine with DHCP)
Change your primary interface to have static IP `nano /etc/network/interfaces`
```bash
# The primary network interface
allow-hotplug ens18
auto ens18
iface ens18 inet static
    address 10.2.1.123
    netmask 255.255.255.0
    gateway 10.2.1.1

```
CTRL+S to save CTRL+X to exit

1. Set Nameservers (Optional if fine with DHCP)
Check on your nameservers and set them `nano /etc/resolv.conf`
```bash
nameserver 10.2.1.1
nameserver 9.9.9.9
```
CTRL+S to save CTRL+X to exit

1. Restart networking to apply your stuff and sign in on new IP via SSH and sign in to root again

1. Setting up the basics (biased) (replace user with your actual user account username)
```bash
apt update && apt upgrade && apt install -y sudo fish unzip htop screen tmux
/sbin/usermod -s /usr/bin/fish root
/sbin/usermod -s /usr/bin/fish user
/sbin/usermod -aG sudo user
set -U fish_user_paths /sbin /usr/sbin $fish_user_paths
su user
set -U fish_user_paths /sbin /usr/sbin $fish_user_paths
exit
exit
exit
```

### Installing and setting up IAX Modem
Sign in as root
1. Install IAX Modem
```bash
apt install -y iaxmodem
```
1. Configure IAX Modem
```bash
nano /etc/iaxmodem/iaxmodem-cfg.ttyIAX0
```
Paste the following, making sure to fill in example values with your own
```bash
device          /dev/ttyIAX0
owner           uucp:uucp
mode            660
port            4577
server          AsteriskServerIP
refresh         300
peername        157
secret          Password123
cidname         FaxingFaxingFaxingdaCID
cidnumber       157
codec           ulaw
answer          yes
```
CTRL+S to Save CTRL+X to exit
1. Make a service for it
Yes there exists sysv files for it, do we want to use those probably not.
```bash
nano /etc/systemd/system/iaxmodem-fax@.service
```
Paste the following
(yes were running it as root, yes this is stupid)
```bash
[Unit]
Description=IAXModem instance %i
After=network.target

[Service]
Type=simple
ExecStart=/usr/bin/iaxmodem --configfile /etc/iaxmodem/iaxmodem-cfg.%i
Restart=always
User=root
Group=root

[Install]
WantedBy=multi-user.target
```
CTRL+S to save CTRL+X to exit
```bash
systemctl daemon-reload
systemctl enable --now iaxmodem-fax@ttyIAX0
systemctl status iaxmodem-fax@ttyIAX0
```
You should now be able to dial the extension and nolonger get Service Unavailable but just the Ring Tone (we have nothing that responds to an incoming call yet but you could pick up using at commands and screen on /dev/ttyAIX0)

1. If installing IAX modem didnt create UUCP group and user for some reason run the following but should exist
```bash
groupadd --system uucp
useradd --system --no-create-home --gid uucp --shell /usr/sbin/nologin uucp

```
### Installing HylaFax Plus (aka simply version 7.0.10)


# Installing HylaFax (Make sure to have a will to live and to not loose it while installing this crap)
Again use Debian 11, I've had no luck on Debian 12 for some reason... (5 hours wasted troubleshooting)

Sign in as root
1. Add Contrib to Debian APT Sources
```bash
sudo sed -i '/^deb /s/main/main contrib non-free/' /etc/apt/sources.list && sudo apt update
```
1. Install dependencies and stuff
```bash
apt install -y build-essential libtiff-dev libjpeg-dev zlib1g-dev libpam0g-dev ghostscript gsfonts libgs-dev flex bison libncurses5-dev texinfo libssl-dev libc-client-dev uuid-dev libtool automake autoconf tcl8.6-dev libtiff-tools libjpeg-progs iaxmodem ghostscript gsfonts gsfonts-other gsfonts-x11 imagemagick ttf-mscorefonts-installer wget sendmail
```
1. Download and Extract HylaFax Plus sources
If that download for whatever reason disapears theres a copy in this repo too.
```bash
cd /usr/local/src
wget -O hylafax-7.0.10.tar.gz "http://prdownloads.sourceforge.net/hylafax/hylafax-7.0.10.tar.gz?download"
tar -xvzf hylafax-7.0.10.tar.gz
cd hylafax-7.0.10
```
1. Configure it (my example [output](examples/outputs/hylafaxconfig.md)), build it and install it. (and pray alot)
```bash
./configure
make
make install
```
(I have changed default page size to A4 as thats the norm here)

1. Preconfiguring Hylafax and making systemd files.
```bash
nano /etc/systemd/system/hylafax-faxq.service
```
```bash
[Unit]
Description=HylaFAX fax queue manager
After=network.target

[Service]
ExecStart=/usr/local/sbin/faxq
Restart=always
User=root
Group=root
Type=forking

[Install]
WantedBy=multi-user.target
```
```bash
nano /etc/systemd/system/hylafax-hfaxd.service
```
```bash
[Unit]
Description=HylaFAX hfaxd server
After=network.target

[Service]
ExecStart=/usr/local/sbin/hfaxd -i hylafax
Restart=always
User=root
Group=root
Type=forking

[Install]
WantedBy=multi-user.target
```
```bash
nano /etc/systemd/system/hylafax-faxgetty@.service
```
```bash
[Unit]
Description=HylaFAX faxgetty on %I
After=network.target

[Service]
ExecStart=/usr/local/sbin/faxgetty /dev/%I
Restart=always
User=root
Group=root
Type=simple

[Install]
WantedBy=multi-user.target
```
```bash
systemctl daemon-reload
systemctl enable --now hylafax-faxq
systemctl enable --now hylafax-hfaxd
systemctl enable --now hylafax-faxgetty@ttyIAX0

systemctl status hylafax-faxq
systemctl status hylafax-hfaxd
systemctl status hylafax-faxgetty@ttyIAX0
```
```bash
/usr/local/sbin/faxstat -s
```










1. Install build and hyla deps :
```
apt update && apt install -y build-essential libtiff-dev libjpeg-dev \
zlib1g-dev libpam0g-dev ghostscript gsfonts libgs-dev flex bison \
libncurses5-dev texinfo libssl-dev libc-client-dev uuid-dev libtool \
automake autoconf tcl8.6-dev libtiff-tools libjpeg-progs iaxmodem ghostscript gsfonts gsfonts-other gsfonts-x11 imagemagick
apt update && apt install -y ttf-mscorefonts-installer
```
1. Download and Extract HylaFax Plus (7) sources
```
cd /usr/local/src
wget -O hylafax-7.0.10.tar.gz "http://prdownloads.sourceforge.net/hylafax/hylafax-7.0.10.tar.gz?download"
tar -xvzf hylafax-7.0.10.tar.gz
cd hylafax-7.0.10
```

1. Configure it and Build it (pray)
```
./configure
make
make install
```

1. Configure IAX Modem (unless you have a physical modem)
``` nano kill youself or some shit idk figure it out ```
paste this shit and adjust for ur stuff
```
device          /dev/ttyIAX0
owner           uucp:uucp
mode            660
port            4577
server          AsteriskServer
refresh         300
peername        157
secret          YourPassowrd
cidname         Fax
cidnumber       157
codec           ulaw
answer          yes
```
enable iaxmodem and see if it works on ur stupid asterisk you dumbass
```
systemctl enable --now iaxmodem
```

1. configure hylaficknig
```
nano /etc/systemd/system/hylafax-faxq.service

[Unit]
Description=HylaFAX fax queue manager
After=network.target

[Service]
ExecStart=/usr/local/sbin/faxq
Restart=always
User=root
Group=root
Type=forking

[Install]
WantedBy=multi-user.target

nano /etc/systemd/system/hylafax-hfaxd.service

[Unit]
Description=HylaFAX hfaxd server
After=network.target

[Service]
ExecStart=/usr/local/sbin/hfaxd -i hylafax
Restart=always
User=root
Group=root
Type=forking

[Install]
WantedBy=multi-user.target

nano /etc/systemd/system/hylafax-faxgetty@.service

[Unit]
Description=HylaFAX faxgetty on %I
After=network.target

[Service]
ExecStart=/usr/local/sbin/faxgetty /dev/%I
Restart=always
User=root
Group=root
Type=simple

[Install]
WantedBy=multi-user.target

systemctl daemon-reload
systemctl enable --now hylafax-faxq
systemctl enable --now hylafax-hfaxd
systemctl enable --now hylafax-faxgetty@ttyIAX0

systemctl status hylafax-faxq
systemctl status hylafax-hfaxd
systemctl status hylafax-faxgetty@ttyIAX0

/usr/local/sbin/faxstat -s
```
rape your modem
/var/spool/hylafax/etc/config.ttyIAX0

# $Id: iaxmodem 692 2007-11-06 18:44:20Z faxguy $

#
# prototype config for the IAXmodem softmodem which uses
# the spandsp soft-DSP library
#

#
CountryCode:		41
AreaCode:		044
FAXNumber:		+41445457486
LongDistancePrefix:	0
InternationalPrefix:	00
DialStringRules:	etc/dialrules
ServerTracing:		1
SessionTracing:		0xFFF
RecvFileMode:		0600
LogFileMode:		0600
DeviceMode:		0666
RingsBeforeAnswer:	1
SpeakerVolume:		off
GettyArgs:		"-h %l dx_%s"
LocalIdentifier:	"Teleco Group"
TagLineFont:		etc/LiberationSans-25.pcf
TagLineFormat:		"From Teleco Group Switzerland | %c | Page %%P of %%T""
MaxRecvPages:		25
#

#
#
# Modem-related stuff: should reflect modem command interface
# and hardware connection/cabling (e.g. flow control).
#
ModemType:		Class1		# use this to supply a hint

#
#             *** Caller-ID settings ***
#
# Enabling this will use the hfaxd-protocol to set Caller*ID
#
#ModemSetOriginCmd:	"AT+VSID=\"%s\",\"%d\""
#
# If "glare" during initialization becomes a problem then take
# the modem off-hook during initialization, and then place it
# back on-hook when done.
#
#ModemResetCmds:	"ATH1\nAT+VCID=1"	# enables CallID display
#ModemReadyCmds:	ATH0
#
# However, glare is mostly avoided by iaxmodem's 5-second internal
# busy-out that occurs after hangups and resets.  These two settings
# will help ensure that our reset and initialization periods don't 
# go beyond that 5-second period.
#
ModemResetDelay: 0				# DTR isn't handled, anyway
ModemSoftResetCmdDelay: 0			# modem reset is complete at "OK"

#
# You'll likely want Caller*ID display (also displays DID) enabled.
#
ModemResetCmds:		AT+VCID=1	# enables CallID display
#
# If you are "missing" Caller*ID data on some calls (but not all)
# and if you do not have adequate glare protection you may want to
# not answer based on RINGs, but rather enable the CallIDAnswerLength
# for NDID, disable AT+VCID=1 and do this:
#
#RingsBeforeAnswer: 0
#ModemRingResponse: AT+VRID=1

# The pty apparently does not support changing parity.
PagerTTYParity:		none

Class1AdaptRecvCmd:	AT+FAR=1
Class1TMConnectDelay:	400		# counteract quick CONNECT response

#
# Older iaxmodem versions didn't support V.17 very well.  It can be
# disabled in this fashion:
#
#Class1RMQueryCmd:	"!24,48,72,96"	# V.17 fast-train recv doesn't work well
#Class1TMQueryCmd:	"!24,48,72,96"	# V.17 fast-train recv doesn't work well

CallIDPattern:          "NMBR="
CallIDPattern:          "NAME="
CallIDPattern:		"ANID="
CallIDPattern:          "NDID="
#CallIDAnswerLength:	4
# Uncomment these if you really want them, but you probably don't.
#CallIDPattern:          "DATE="
#CallIDPattern:          "TIME="


/usr/local/sbin/faxsetup
