# RGMII Toolkit
**ORIGINALLY FOR THE QUECTEL RM520N-GL, However, People are saying this will work on all M.2 RMxxx modems**
#### [JUMP TO COMBO INSTALLER](#installation-automated)
**Currently:** This will install or if already installed, update or remove a Combination of [AT Telnet Daemon](https://github.com/natecarlson/quectel-rgmii-at-command-client/tree/main/at_telnet_daemon)  and; [Simpleadmin](https://github.com/iamromulan/quectel-rgmii-simpleadmin). This will also allow you to set a daily reboot timer and send AT commands easily. 

**My goal** is for this to also include any new useful scripts or software for this modem and others that support RGMII mode.
## Screenshots

![Home Page](https://github.com/iamromulan/quectel-rgmii-configuration-notes/blob/main/images/iamromulansimpleindex.png?raw=true)
![AT Commands](https://github.com/iamromulan/quectel-rgmii-configuration-notes/blob/main/images/iamromulanatcommands.png?raw=true)
![TTL](https://github.com/iamromulan/quectel-rgmii-configuration-notes/blob/main/images/iamromulansimpleTTL.png?raw=true)
![Toolkit](https://github.com/iamromulan/quectel-rgmii-configuration-notes/blob/main/images/iamromulantoolkit.png?raw=true)
## Installation Automated

> :warning: Your modem must already be connected to the internet for this to work


Script will present a list of options:

 1.  Send AT Commands
 2.  Install/Update or remove AT Telnet Daemon
 3. Install/Update or remove Simple Admin
 4. Install/Change or remove Daily Reboot Timer
 5. Exit


The Simple Admin web interface depends on the AT Telnet Daemon so you'll need to install both. 
After that the web interface should be working. 
If you press 4 it will create a daily reboot timer and ask you for the time it should reboot daily in UTC 24-hour format.
If it is already installed and you press 2, 3, or 4 it will prompt to uninstall, update, or change. 
If you press 1 you can send AT commands, sending exit in lower case will return you to the main menu.

You can copy/paste this into a command prompt on a system with adb installed. If you don't have adb follow the directions in my main [RGMII Guide](https://github.com/iamromulan/quectel-rgmii-configuration-notes#using-adb)
```bash
adb shell wget -P /tmp https://raw.githubusercontent.com/iamromulan/quectel-rgmii-toolkit/main/RMxxx_rgmii_toolkit.sh
adb shell chmod +x /tmp/RMxxx_rgmii_toolkit.sh
adb shell sh /tmp/RMxxx_rgmii_toolkit.sh
```
If you have trouble downloading the file make sure your modem is connected to a cellular network.

If you already had all your proper settings set and you just flashed the firmware, more than likely running AT+QMAPWAC=1 and rebooting will fix that. You can do it with adb as well like this:  

    adb shell "echo -e 'AT+QMAPWAC=1 \r' > /dev/smd7"
    adb shell reboot


====================================================

## Acknowledgements
Thanks to the work of [Nate Carlson](https://github.com/natecarlson) (Telnet Deamon, Original RGMII Notes), [aesthernr](https://github.com/aesthernr) (Original simpleadmin), and [rbflurry](https://github.com/rbflurry/) (Fixing simpleadmin not functioning) we can install these! The Telnet Deamon is a Telnet to AT command server. With it, you can connect with a Telenet client like PuTTY on port 5000 to the modems gateway IP (Normally 192.168.225.1) and send AT commands over Telnet! Simpleadmin is a simple web interface you'll be able to access using the modems gateway IP address. You can see some basic signal stats, send AT commands from the browser, and change your TTL directly on the modem. By default this will be on port 8080 so if you didn't change the gateway IP address you'd go to http://192.168.225.1:8080/ and you'd find what you see in the [Screenshots](#screenshots) section.

Simpleadmin heavily uses the AT Command Parsing Scripts (Basically a copy with minor tweaks) of Dairyman's Rooter Source https://github.com/ofmodemsandmen/ROOterSource2203

