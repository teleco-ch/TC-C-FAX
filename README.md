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
- A barebones Hylafax Server (see here [Setting up a Debian 11 VM for our Hylafax and TC-C-FAX host](HYLAFAX-SETUP.md) )

Todo :  Make a tiny Image of the vm and offer it [ ]
        Automate the setup process with like a bash script [ ]
        Make it work by magic OOOoooOOOoooo [ ]
