Installation
------------



1. Login as root.

2. Enter the following commands to unpack the driver source code.

3. To build the driver in Mac OS X, please install development tools from
   Apple and install libusb. Enter the following commands to install the
 driver.



# ./MacOSX/configure

# make

# make install


Debug smartcard with reader driver:
Debug CCID driver under yosemite

Displaying APDU transfer between reader and card:

1. Activate logging
$ sudo defaults write /Library/Preferences/com.apple.security.smartcard Logging -bool yes


2. Read logging state
$ defaults read /Library/Preferences/com.apple.security.smartcard Logging
1


3. Plug in a USB reader
4. Read logging state again

$ defaults read /Library/Preferences/com.apple.security.smartcard Logging
0




Set debug:
$ ps -Aww | grep com.apple.ifdreader
28775 ??         0:00.74 /System/Library/CryptoTokenKit/com.apple.ifdreader.slotd/Contents/MacOS/com.apple.ifdreader
28803 ttys000    0:00.00 grep com.apple.ifdreader
In my case the PID is 28775. You can see the syslog filter for the process using:
$ syslog -c 28775
Process 28775 syslog filter mask: Off

Change the filter using:
$ sudo syslog -c 28775 -d

-d indicates: set the filter level to cause to log messages from Emergency up to Debug.

And verify the filter has changed:
$ syslog -c 28775 
Process 28775 syslog filter mask: Emergency - Debug

Displaying logs, You can use the Console application to display the logs.

You can also use a command line program with:
$ syslog -w -k Sender com.apple.ifdreader



