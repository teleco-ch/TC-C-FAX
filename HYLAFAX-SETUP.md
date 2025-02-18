# Setting up a Debian 11 VM for our Hylafax and TC-C-FAX host.
You will need Debian 11! Anything newer I was not able to get running and even Debian 11 is a stretch as to how recent it can be. I also don't recommend doing this in a container as of now. If you want to do so your on your own.

As to the Debian VM its nothing special just default no desktop just SSH and standard system utils.

Make sure to have a valid FQDN and preferably have a static IP

## Preparing Debian 11 VM
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
apt update && apt upgrade && apt install -y sudo fish unzip htop screen tmux psmisc
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
Type=forking
PIDFile=/var/run/iaxmodem-%i.pid
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
If that download for whatever reason disapears theres a copy in this repo too in the archive folder.
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

Crashes for faxq are okay missing some config.

1. Remove SysV Init Files for Hylafax since we replaced them with proper ones
```
systemctl mask hylafax.service
rm -f /etc/init.d/hylafax
sudo update-rc.d -f hylafax remove

```

1. Preconfigure HylaFax for your modem
```
nano /var/spool/hylafax/etc/config.ttyIAX0
```
Now paste the following and make changed where needed

```conf
# prototype config for the IAXmodem softmodem which uses
# the spandsp soft-DSP library

CountryCode:		41
AreaCode:		044
FAXNumber:		+41444444444
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
LocalIdentifier:	"Your Fax CID"
TagLineFont:		etc/LiberationSans-25.pcf
TagLineFormat:		"From Your Fax | %c | Page %%P of %%T""
MaxRecvPages:		25
ModemType:		Class1		# use this to supply a hint
#ModemSetOriginCmd:	"AT+VSID=\"%s\",\"%d\""
#ModemResetCmds:	"ATH1\nAT+VCID=1"	# enables CallID display
#ModemReadyCmds:	ATH0
ModemResetDelay: 0				# DTR isn't handled, anyway
ModemSoftResetCmdDelay: 0			# modem reset is complete at "OK"
ModemResetCmds:		AT+VCID=1	# enables CallID display
PagerTTYParity:		none
Class1AdaptRecvCmd:	AT+FAR=1
Class1TMConnectDelay:	400		# counteract quick CONNECT response
# For old iaxmodem versions
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
```
1. Run Fax Setup and answer questions. (Minified example below)
```
/usr/local/sbin/faxsetup

Should an entry be added for the FaxMaster to /etc/aliases [yes]? 
Users to receive fax-related mail [root]? 
Generate etc/ssl.pem for SSL Fax [yes]? no
Country code [1]? 41 
Area code [000]? 044
Long distance dialing prefix [1]? 0
International dialing prefix [011]? 00
Dial string rules file (relative to /var/spool/hylafax) ["etc/dialrules"]? 
Tracing during normal server operation [1]? 
Default tracing during send and receive sessions [0xFFF]? 
Continuation cover page (relative to /var/spool/hylafax) []? 
Timeout when converting PostScript documents (secs) [180]? 
Maximum number of concurrent jobs to a destination [1]? 
Define a group of modems []? 
Time of day restrictions for outbound jobs ["Any"]? 
Timeout before purging a stale UUCP lock file (secs) [30]? 
Max number of pages to permit in an outbound job [0xffffffff]? 
Syslog facility name for ServerTracing messages [daemon]? 
Is it ok to send a QUIT command to each process [yes]? 
/usr/local/sbin/faxquit ttyIAX0
Done verifying system setup.

root@fax /u/l/s/hylafax-7.0.10# /usr/local/bin/faxstat -s
HylaFAX scheduler on fax.teleco.local: Running
Modem ttyIAX0 (+41444444444): Waiting for modem to come ready
```
If modem doesnt come online make sure its all happy happy on asterisk and stuff otherwise idk ask an ai or something this was enough of a pain to figure out ... and btw chatppt will give you wrong answers about hylafax... and that like alot so dont rely on it