# Introduction
PTP daemon (PTPd) implements the Precision Time Protocol (PTP) (IEEE 1588). This repository is a guide to install it in a Linux system. The commands were tested on a Raspberry Pi 4 running Raspberry Pi OS.

# Steps to install

1. Download PTPD from Sourceforge (https://sourceforge.net/projects/ptpd/). If unavailable, download the included "ptpd-2.3.1.tar.gz" file above or from this [link](https://github.com/nithishkgnani/P4_Projects/tree/main/PTPD).
2. Extract the .tar.gz file to a folder
3. Install the necessary tools (automake, autoconf, libtool) by entering the following commands in a terminal
* `sudo apt install autotools-dev`
* `sudo apt install autoconf`
* `sudo apt install libtool`
* `sudo apt install libpcap-dev`
4. In the terminal, navigate (cd) to the extracted PTPD folder (example- /../folder/subfolder/ptpd-2.3.1) and run the following commands
* `autoreconf -vi`
* `./configure`
* `make`
<br />You may refer to the file named "install" in the same folder for more details about the commands.
5. Edit the configuration file "client-e2e-socket.conf" inside the "test" folder using a suitable editing software. I used gedit.
* `gedit test/client-e2e-socket.conf`
* Add the network interface name at the end of the line: ptpengine:interface = 
* Change the ptpengine:preset to suitable preset among none,	slaveonly, masteronly and masterslave. The details are given in the configuration file itself.
* Change the ptpengine:clock_class to a suitable number as explained in the file.
6. Test it using the command
* `sudo ./src/ptpd2 -c test/client-e2e-socket.conf`
7. Check the log output of the daemon in /var/run/ptpd2.event.log
<br />Check statistics output of the daemon in /var/run/ptpd2.stats.log
<br />Check the status file /var/run/ptpd2.status.log
8. `sudo make install`
9. ptpd2 is now installed. To get help on the commands, type anyof these in terminal:
* `ptpd2 --help`
* `ptpd2 --long-help`
