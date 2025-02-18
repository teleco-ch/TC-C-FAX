TC-C-FAX :

Telecos Crappy Fax 

Very wip... lol 


# Installing HylaFax (Make sure to have a will to live and to not loose it while installing this crap)
Done on Debian 11 because 12 is even more broken, use root user to save yourself some pain


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
