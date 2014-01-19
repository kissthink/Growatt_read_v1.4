Growatt_read_v1.4
=================

test af perl script kopieret fra http://www.snafu.priv.at/mystuff/growatt.html

Growatt/Sungold Inverter: protocol specs and data readout in perl
If you've got a Growatt or Sungold inverter, then you will likely know that it has an RS232 port (9600 8N1, no flow control, and straight through cable) and that the manufacturer only provides hideously horrible and somewhat broken windows software for reading the inverter status.

However, their support isn't bad and they sent me the protocol specification within one day of me asking. Here is the Growatt Serial Comms Protocol as PDF. The comms protocol is a tad odd, and the spec isn't 100% clear in all situations but with a bit of fiddling I got a perl reader to work. The comms implementation isn't very robust; while experimenting I managed to send it into a catatonic state a few times, and it stuffs up the message checksum that it sends every now and then, too.

Without further ado, here's my perl proggie. It doesn't work with the growatt's super-weird dynamic address mode (shows as "MOVE" on the LCD); knock through the menus and set a fixed address value first. The perl proggie also expects a unixy box with /bin/stty because I couldn't be bothered to do the tedious termios fiddling from within perl.

Update (Tue 06.11.2012 21:45):
Michael Wheeler reminded me that the Growatt firmware isn't exactly a paragon of stability and does occasionally send out garbage data. He added a few robustness features to the code, which I've just merged back into the the newest version of read-growatt. In addition to that I've found out that some multi-string Growatt models (4400MTL for example) use a different packet format; unfortunately that means read-growatt doesn't work for these right now - until somebody supplies me a protocol description for those models.


© Alexander Zangerl
