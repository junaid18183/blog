---
layout: post
title: Linux Mini Mannual
date: 2012-06-26 12:22:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3897127296261767156'
---
<div dir="ltr" style="text-align:left;">
<div>|– FILES/SEARCH/SYSTEM  –|<br />Unique names, <span class="IL_AD" id="IL_AD1">remove duplicate<span class="IL_AD_ICON"></span></span> names:<br /># cat words.txt | sort | uniq &gt; dictionary.txt<br />remove any words not X size, or from X to Y:<br /># cat dictionary.txt | pw-inspector -m 6 -c 2 -n &gt; passlist.txt</p>
<p>LIST ALL <span class="IL_AD" id="IL_AD8">OPEN FILES<span class="IL_AD_ICON"></span></span>:<br /># lsof<br />Only of specific process(for only top 5 use -d0-5):<br /># lsof -a -p 890 </p>
<p>FINIDNG WHERE IS THE CMD:<br /># type ls<br />Find where is the executable<br /># which mysqldump</p>
<p>FINDING A FILE:<br /># find / -name flie.txt<br /># slocate file<br /># locate file<br /># whereis (search mans/bins)</p>
<p>FINDING AN INSTALLED LIBRARY/PACKET:<br /># apt-cache search gd | grep php<br /># dpkg -l | grep radius<br /># ldconfig -p |grep ‘libgd.so’<br /># ldconfig  -v  | grep db<br /># aptitude search snmp | grep perl</p>
<p>FIND A STRING <span class="IL_AD" id="IL_AD9">INSIDE<span class="IL_AD_ICON"></span></span> FILES<br /># grep -R “s1-ws-2960G” /home/comm/nagios/conf/* | less<br /># find / -name | xargs grep </p>
<p>FIND A STRING AND REPLACE<br />$ grep -rl OLDSTRING . | xargs perl -pi~ -e ’s/OLDSTRING/NEWSTRING/’<br />and if you want to do it sorted, files (this will even do unique results too!):<br />$ grep -rl OLDSTRING . | sort -u | xargs perl -pi~ -e ’s/OLDSTRING/NEWSTRING/’<br />and for you old school sed peeps (sed args aren’t as obscure):<br />$ grep -rl OLDSTRING . | xargs sed -i -e ’s/OLDSTRING/NEWSTRING/’</p>
<p>FIND KERNEL DRIVER MODULE CONFIG:<br /># grep -R “bttv” /etc/* | less&lt;<br />The strings Commands</p>
<p>SEARCH INSIDE BINARY FILES FOR TEXT STRING:<br /># strings $(which sshd)| grep libwrap<br /># strings /usr/bin/users</p>
<p>MORE INFO ON A FILE:<br /># ls -l file<br /># stat file<br /># file -b file (reports Txt Type)</p>
<p>CHECKING HD SIZE:<br /># df -k<br /># du -kx / | sort -nr | less</p>
<p>DIRECTORY SIZES:<br />#du –summarize –human-readable</p>
<p>SIZE OF NEW FILES:<br />#du -ah | sort -rn | head</p>
<p>FIND BIG FILES EXCLUDING ANYTHING IN A BIN DIR:<br /># find / -type f -ls | sort -k 7 -r -n | grep -v ‘/bin’ | head<br /># find / -type f -ls | sort -k 25 -r -n | head</p>
<p>EXCLUDE EXECUTABLES:<br /># find / -type f -not -perm -g=x,-o=x -ls | sort -k 7 -r -n | head</p>
<p>CHECK LARGEST EXECUTABLE FILE:<br /># find / -type f -perm -g=x,-o=x -ls | sort -k 7 -r -n | head</p>
<p>|– NETWORK –|</p>
<p>NETWORK ACTIVITY, ports Listening and Established connections:<br /># lsof | egrep “ESTABLISHED|LISTEN” | more</p>
<p>Change ip address:<br /># vim /etc/network/interfaces<br />SET STATIC IP<br />auto eth3<br />iface eth3 inet static<br />address 10.1.0.87<br />netmask 255.255.0.0<br />network 10.1.0.0<br />broadcast 10.1.255.255<br />gateway 10.1.0.1<br />OR, but not persistant<br /># ifconfig -a<br /># netstat -rn<br />Setup Static IP/MASK/Gateway:<br /># ifconfig eth0  mask <br />ifconfig eth1 10.10.10.186 mask 255.255.255.0<br />Route Net:<br /># route add -net 161.116.1.0 netmask 255.255.255.0 eth0<br />Set Gateway:<br /># route add default gw 192.168.3.1<br />Set DNS:<br /># vim  /etc/resolv.conf<br />Or just vim /etc/network/interfaces<br />Restart <span class="IL_AD" id="IL_AD7">the Network<span class="IL_AD_ICON"></span></span>:<br /># /etc/init.d/networking restart</p>
<p>NETWORK CONFIG GUI BASED<br />netconf , linuxconf, netconfig<br />Connexions TCP/IP<br /># netstat -an<br /># lsof -i</p>
<p>SET INTERFACE TO USE A DHCP<br /># vim /etc/network/interfaces<br /># auto eth0<br /># iface eth0 inet dhcp</p>
<p><span class="IL_AD" id="IL_AD5">WIRELESS<span class="IL_AD_ICON"></span></span> INTERFACES<br /># iface wlan0 inet dhcp<br /># wireless_mode managed<br /># wireless_rate 54M auto<br /># wireless_channel 6<br /># wireless_essid XXXXX<br /># wireless_key XXXXXXXXXX</p>
<p>MOUNT WINDOWS SHARE<br />edit /etc/hosts with IP host<br /># mkdir /mnt/music<br /># vim /etc/fstab    //host/share  /mnt/music  smbfs exec,credentials=/etc/cifspw 0 0<br /># vim /etc/cifspw &gt; <span class="IL_AD" id="IL_AD12">username<span class="IL_AD_ICON"></span></span>=Jason /n password=ImNotGonnaTellYouThat<br /># chmod 600 /etc/cifspw<br /># mount -a<br />If smbfs dont work try cifs<br />Or<br /># mount -t smbfs -o username=$NTUSER,password=$NTPASSWD $NTSHARE $MNT<br /># mount -t smbfs -o username=backadmin1,password=backadin1 \\10.10.1.1\bck_linux_oasis \mnt\backup_linux</p>
<p>Get <span class="IL_AD" id="IL_AD4">MAC address<span class="IL_AD_ICON"></span></span>:<br />Get the MAC address in script form:<br /># ifconfig wlan2 | grep HWaddr | awk ‘{print $5}’ | sed -e ’s/-/:/g’  &gt;&gt;/tmp/mac<br />Best way:<br /># cat /sys/class/net//device/net/map /address</p>
<p>NETBIOS INFORMATION, same as Windowze “nbtstat -an”:<br /># nmblookup -A </p>
<p>CHANGE <span class="IL_AD" id="IL_AD3">HOSTNAME<span class="IL_AD_ICON"></span></span><br /># vim /etc/hostname<br /># etc/init.d/hostname.sh start<br />or<br />#hostname myname.local<br />or<br />#sysctl kernel.hostname=</p>
<p>|– HARD DISK –|</p>
<p><span class="IL_AD" id="IL_AD10">PARTITION<span class="IL_AD_ICON"></span></span> DISK<br />Use GUI:<br /># gparted<br />List partition and Disks<br /># fdisk -l<br />Partition<br /># cfdisk /dev/hdc<br />FORMAT<br /># mkfs.ext3 /dev/hdc1<br />MOUNT<br />mkdir /new-disk<br />mount -t ext2 /dev/sdb1 /cache</p>
<p>OGs de SO: Estat HW i SW<br />dmesg<br />more /var/adm/messages<br />more /var/log/syslog</p>
<p>Estat processos<br />#ps -edaf<br />#sudo lsof -p pid</p>
<p>Backup, Compress entire folder:<br />#tar cvf FILE.tar /home/PATH/confs/*.*</p>
<p>Estat de càrrega sistema<br />#top<br />#vmstat</p>
<p>UPDATING DEBIAN/UBUNTU:<br /># apt-get update<br /># apt-get dist-upgrade<br /># apt-get autoclean</p>
<p>|– SQUID PROXY –|<br />nice way to monitor real time<br />#tail -f /var/log/squid/access.log | awk ‘{print$3 ” ” $8 ” ” $4 ” ” $6 ” ” $8 ” ” $9 ” ” $7}’<br />Where number showed on awk option are number of log information per line splited by space.</p>
<p>|– EMAIL SYSTEMS –|<br />MAILSERVER (EXIM4):<br />Config files are at<br />/etc/exim4/<br />Reconfigure:<br />#dpkg-reconfigure exim4-config<br />Restart Exim4 mailserver:<br />#invoke-rc.d exim4 restart</p>
<p>After editing the config file, run:<br />#exim -bV<br />Tip: I also link sendmail to exim via:<br />#ln -s /usr/sbin/exim /usr/sbin/sendmail<br />Now, check a local address:<br />#exim -bt <a href="mailto:local_user@your.domain">local_user@your.domain</a><br />Next check a remote address:<br />#exim -bt <a href="mailto:fferreira@their.domain">fferreira@their.domain</a><br />Test sending an email:<br /># <span class="IL_AD" id="IL_AD11">echo<span class="IL_AD_ICON"></span></span> “TEST EMAIL” | Mail -s “TestSub” <a href="mailto:fferreira@osiatis.es">fferreira@osiatis.es</a><br />OR with Exim4 (fix the quotes!):<br />#exim -v <a href="mailto:fferreira@osiatis.es">fferreira@osiatis.es</a><br />Remove FRONZEN emails.<br /># exiqgrep -zi | xargs exim -Mrm<br />Spool should be here:<br />/var/spool/exim4/<br />Logs Should be here<br />more /var/log/exim4/mainlog</p>
<p>SENDMAIL<br />#apt-get install sendmail<br />#sendmailconfig (just say “Y” to all the questions)<br />ref. http://networking.ringofsaturn.com/Unix/sendmail.php<br />test email<br /># echo “TEST EMAIL” | sendmail -s “TestSub” <a href="mailto:fferreira@osiatis.es">fferreira@osiatis.es</a><br />OR with Exim4 (fix the quotes!):<br /># echo “TEST EMAIL” | Mail -s “TestSub” <a href="mailto:fferreira@osiatis.es">fferreira@osiatis.es</a></p>
<p>Or in Exim<br />#exim4 -bt <a href="mailto:email@test.com">email@test.com</a></p>
<p>Get info about mail:<br /># sendmail -d0.1 -bt &lt; /dev/null<br /># sendmail -bv <br />Stop Sendmail:<br /># /etc/init.d/sendmail stop<br />Start Sendmail:<br /># /usr/lib/sendmail -bd -q1h.</p>
<p>|–  HARDWARE CMDS –|</p>
<p>List all hardware:<br />#lshw</p>
<p>List all network related<br /># lshw -C network</p>
<p>List all USB connected hardware:<br /># lsusb</p>
<p>List all PCI connected hardware:<br /># lspci</p>
<p>Screen Resolution setup:<br />#sudo dpkg-reconfigure -phigh xserver-xorg</p>
<p>START STOP A SERVICE:<br /># /etc/init.d/ start</p>
<p>GET INFO ON RUNNING PROCESS:<br /># ps ax | grep </p>
<p>KEYS:</p>
<p>CRTL-ALT-BACKSPACE will restart X11<br />CRTL-ALT-F1 will go to CMD line</p>
<p>FINDING INFO ABOUT A CMD:<br /># apropos mail<br /># man -k </p>
<p>EDITORS<br /># nano<br /># vim<br /># vi</p>
<p>Make sure MySQL module for php5 is installed:<br /># dpkg –list | grep php5-mysql<br /># ldconfig  -v<br />STARTUP IN TEXT/GUI MODE:<br />Remove GUI from boot up ( better memory):<br />#update-rc.d -f gdm remove<br />To start GUI:<br />#startx<br />To have it GUI startup again:<br /># /usr/sbin/update-rc.d gdm defaults</p>
<p>*Autostart Daemon Ubuntu/Debian<br /># /usr/sbin/update-rc.d mysql defaults<br />/usr/sbin/update-rc.d nagios defaults</p>
<p>SCHEDULLE A TASK<br />Edit the <span class="IL_AD" id="IL_AD2">crontab<span class="IL_AD_ICON"></span></span> schedulle<br /># crontab -e<br />The syntax is:<br />* * * * * Command to be executed<br />- – - – -<br />| | | | |<br />| | | | +—– Day of week (0-6)<br />| | | +——- Month (1 – 12)<br />| | +——— Day of month (1 – 31)<br />| +———– Hour (0 – 23)<br />+————- Min (0 – 59)<br />ex.<br />0 23 * * *  bash /etc/scripts/backupmysql.sh<br />0 10 * * *  perl /scripts/ftpsync.pl -q<br />0 18 * * *  perl /home/felix/Documents/SCRIPTS/ftpsync.pl<br />Every 2 minutes<br /># */2 * * * * * bash /etc/scripts/backupmysql.sh<br />AT Schedulle Tasks, it will prompt for the cmd, + CRTL+D (to save)<br /># at 22:30<br /># /etc/scripts/backupmysql.sh<br /># CRTL D<br />List tasks<br /># atr<br />Deletes tasks. Type:<br />#atrm job .</p>
<p>-Change default language:<br />dpkg-reconfigure -plow locales<br />-Change keyboad layout:<br />dpkg-reconfigure console-data<br />-Reconfigure postfix for your convenience:<br />dpkg-reconfigure postfix</p>
<p>|– MySQL –|<br />Run the Backup Script then<br /># mysql -u root -p<br />mysql&gt; flush logs;<br />will create a brand new mysql-bin.0000xy<br />mysql&gt; purge binary logs to ‘mysql-bin.0000xy’;<br />will purge all your logs files before the last.</p>
<p>Commads on User information::<br />#usermod<br />#id logname whoami groups users who<br />#adduser, addgroup, deluser and delgroup</p>
<p>Setting the Time and Hardware time<br />#date -s “Thu Oct  2 9:30:47 CEST 2008?<br />If you set your clock to UTC rather than local time, issue the command:<br />#hwclock –systohc –utc<br />When  you power down or reboot your system, the system date and time will  revert to the values held in non-volatile (CMOS) memory. To store the  Linux date and time in CMOS, issue the following command:<br />#hwclock –systohc<br />Set the TimeZone:<br />#tzconfig</p>
<p>TImeZones file:<br />vim /etc/default/rcS</p>
<p>RECONFIGURE A PACKAGE<br /># dpkg-reconfigure tzdata</p>
<p>Strange Time problems? Solution Install chrony (uses NTP protocol):<br />#apt-get install chrony<br />Restart chrony:<br />#invoke-rc.d chrony restart</p>
<p>ref. http://www.debian.org/doc/manuals/system-administrator/ch-sysadmin-time.html<br />ref. /usr/share/doc/util-linux/README.Debian.hwclock</p>
<p>VI EDITOR<br />La tecla “x” borra el carácter seleccionado con el cursor.<br />La tecla “d”, puslada dos veces consecutivas, borra una línea.<br />Una vez finalizada la edición, escribimos “:wq”<br />http://faqs.pcbsd.es/index.php?action=artikel&amp;cat=11&amp;id=204&amp;artlang=es</p>
<p>IPTABLES<br />Show all current Nmap rules<br /># iptables -L<br />To use a nice graphic interface download firestarter<br />Allows state INVALID (otherwise nmap wont work and you<br />will get errors type: “Operation not permitted”)</p>
<p>iptables echo 1 &gt; /proc/sys/net/ipv4/ip_forward<br />echo 1 &gt; /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts<br />echo 0 &gt; /proc/sys/net/ipv4/conf/all/accept_source_route<br />echo 1 &gt; /proc/sys/net/ipv4/tcp_syncookies<br />echo 0 &gt; /proc/sys/net/ipv4/conf/all/accept_redirects<br />echo 0 &gt; /proc/sys/net/ipv4/conf/all/send_redirects<br />echo 1 &gt; /proc/sys/net/ipv4/conf/all/rp_filter<br />echo 1 &gt; /proc/sys/net/ipv4/conf/all/log_martians<br />iptables –flush<br />iptables -F INPUT<br />iptables -P INPUT DROP<br />iptables -F OUTPUT<br />iptables -P OUTPUT DROP<br />iptables -F FORWARD<br />iptables -P FORWARD DROP<br />iptables -t nat -F<br />iptables -A INPUT -m state –state ESTABLISHED,RELATED -j ACCEPT<br />iptables -A OUTPUT -m state –state NEW,ESTABLISHED,RELATED,INVALID -j ACCEPT</p>
<p>NAUTILUS<br />Gnome Nice Scripts for its “Explorer” Nautilus.<br />Just copy the files to<br /># ~/.gnome2/nautilus-scripts<br />and<br /># chmod +x -R ~/.gnome2/nautilus-scripts</p>
<p>Here are the scripts:<br />http://g-scripts.sourceforge.net/index.php</p>
<p>route add default gw 192.168.99.254</p></div>
</div>
