SDRecord
====

Tool for audio recording with SDR, tested to work with Gqrx: https://github.com/csete/gqrx or http://gqrx.dk

**SDRecord is able to reduce network traffic, disk space needed for records and in plus can record for X specified minutes and/or for X specified MBs of data.**

SDRecord drops UDP packets coming from Gqrx that do not contain any relevant data ( data payload is 0 ) and sends in output ( on stdout or to a file and/or to a remote host ) only packets containing info.

Usage and Options
-----------------

***Usage:***

```
usage: java SDRecord [options]
 -d <arg>   Remote port, to use with -r option
 -f <arg>   Output file where to save the recording
 -h         Help
 -l <arg>   Bind to a specific local address, default is 0.0.0.0 (all)
 -m <arg>   Minutes to record, default is no limit
 -p <arg>   Local port to use, default is 7355
 -r <arg>   Remote address where to send data
 -s <arg>   Stop recording when reaching specified MBs
 -v         Print SDRecord version and exit

```
**NOTE: When is not specified an output file or a remote host, data is written on stdout.**

Putting all together
--------------------

1) Clone the repository using git or download it manually

2) Unzip the repository and compile the java code: ```andrea@Workstation:~/Downloads/SDRecord-master$javac SDRecord.java```

3) Launch Gqrx enabling stream audio over UDP (default port 7355)

4) In a terminal window, execute SDRecord: ```andrea@Workstation:~/Downloads/SDRecord-master$java SDRecord [options]```

Gqrx audio spec
---------------

The streamed audio has the following specifications:

Channels: 1 (left)

Sample rate: 48 kHz

Sample format: 16 bit signed, little endian (S16LE)

## Examples

Recording in a file:
```bash
andrea@Workstation:~/Downloads/SDRecord-master$ java SDRecord -f audiofile
Listening /0.0.0.0 on port 7355
345.9 KB transferred	 Press Ctrl+c to terminate
```
Recording in a file and sending data to a remote host for a max of 10 MB:
```bash
andrea@Workstation:~/Downloads/SDRecord-master$ java SDRecord -s 10 -f audiofile -r 192.168.1.105 -d 7356
Listening /0.0.0.0 on port 7355
345.9 KB / 10.00 MB transferred	 Press Ctrl+c to terminate
```
Recording for 30 minutes and sending max 50 MB of data to a remote host:
```bash
andrea@Workstation:~/Downloads/SDRecord-master$ java SDRecord -m 30 -s 50 -r 192.168.1.105 -d 7356
Listening /0.0.0.0 on port 7355
1782 seconds remaining
345.9 KB / 50.00 MB transferred	 Press Ctrl+c to terminate
```

License and Donations
-------

Written by Andrea Dari and licensed under GNU GPL v2.0

If you have found this tool useful I gladly accept donations, also symbolic through Paypal:

<a href="https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=andreadari91%40gmail%2ecom&lc=IT&item_name=Andrea%20Dari%20IT%20independent%20researcher&currency_code=EUR&bn=PP%2dDonationsBF%3abtn_donateCC_LG%2egif%3aNonHostedGuest"><img src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" alt="[paypal]" /></a> or Bitcoin: 1B2KqKm4CgzRfSsXv7VmbmXD9XNQzzLaTW
