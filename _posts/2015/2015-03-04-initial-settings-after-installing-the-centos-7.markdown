---
layout: post
title: Initial Settings after installing the CentOS 7
date: 2015-03-04 12:16:43.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  _publicize_pending: '1'
  is_reblog: '1'
  post_id: '20139'
  blog_id: '34242667'
  reblog_snapshot: "O:8:\"stdClass\":8:{s:5:\"title\";s:46:\"Initial Settings after
    installing the CentOS 7\";s:4:\"type\";s:4:\"post\";s:9:\"mime_type\";s:0:\"\";s:6:\"format\";b:0;s:12:\"modified_gmt\";s:19:\"2014-09-13
    09:45:25\";s:9:\"permalink\";s:86:\"https://rbgeek.wordpress.com/2014/07/15/initial-settings-after-installing-the-centos-7\";s:7:\"content\";s:14109:\"<div
    class=\"reblogged-content\">\n\n<strong>1)</strong> To change the hostname permanently,
    edit the following file:\r\n<pre><span style=\"color:#ff0000;\">sudo vi /etc/hostname</span></pre>\r\n<a
    href=\"https://junaid18183.files.wordpress.com/2015/03/centos7.jpg\"><img class=\"aligncenter
    size-full wp-image-20141\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7.jpg\"
    alt=\"centos7\" width=\"630\" height=\"149\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\nHere you can simply putÂ the name of your system
    (in my case, I have assigned it <span style=\"color:#ff0000;\">CentOS-7</span>):\r\n\r\n<a
    href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-1.jpg\"><img class=\"aligncenter
    size-full wp-image-20142\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-1.jpg\"
    alt=\"centos7 (1)\" width=\"630\" height=\"139\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-1.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\n<!--more-->After that, edit the hosts file:\r\n<pre><span
    style=\"color:#ff0000;\">sudo vi /etc/hosts</span></pre>\r\n<a href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-2.jpg\"><img
    class=\"aligncenter size-full wp-image-20143\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-2.jpg\"
    alt=\"centos7 (2)\" width=\"630\" height=\"97\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-2.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\nHere add the same name, that you have added in
    the <span style=\"color:#ff0000;\">/etc/hostname</span> file, after 127.0.0.1:\r\n\r\n<a
    href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-3.jpg\"><img class=\"aligncenter
    size-full wp-image-20144\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-3.jpg\"
    alt=\"centos7 (3)\" width=\"630\" height=\"88\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-3.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\nAfter reboot, it will display the new hostname.\r\n\r\n<strong>2)</strong>
    After login to the CentOS7 server(minimal installation), you will notice that
    the system doesn't have ifconfig command :\r\n\r\n<a href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-4.jpg\"><img
    class=\"aligncenter size-full wp-image-20147\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-4.jpg\"
    alt=\"centos7 (4)\" width=\"630\" height=\"124\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-4.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\nInstall the net-tools package which will include
    ifconfig:\r\n<pre><span style=\"color:#ff0000;\">sudo yum install net-tools</span></pre>\r\n<a
    href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-5.jpg\"><img class=\"aligncenter
    size-full wp-image-20148\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-5.jpg\"
    alt=\"centos7 (5)\" width=\"630\" height=\"85\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-5.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\nTry the <span style=\"color:#ff0000;\">ifconfig</span>
    command once again:\r\n\r\n<a href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-6.jpg\"><img
    class=\"aligncenter size-full wp-image-20150\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-6.jpg\"
    alt=\"centos7 (6)\" width=\"630\" height=\"173\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-6.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\n<strong>3)</strong> Change the default network
    interface name to \"eth0\"\r\n\r\nCentOS7 has a default nic name as \"en016.....\",
    as we can see in above screenshoot. To change it backÂ to the default network
    device name like \"ethX\", edit the grub file:\r\n<pre><span style=\"color:#ff0000;\">sudoÂ vi
    /etc/default/grub</span></pre>\r\n<a href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-7.jpg\"><img
    class=\"aligncenter size-full wp-image-20152\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-7.jpg\"
    alt=\"centos7 (7)\" width=\"630\" height=\"87\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-7.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\nSearch for the line â\x80\x9C<span style=\"color:#ff0000;\">GRUB_CMDLINE_LINUX</span>â\x80\x9D
    and append the following: â\x80\x9C<strong><span style=\"color:#ff0000;\">net.ifnames=0
    biosdevname=0</span></strong>â\x80³\r\n\r\nWill look like this:\r\n<pre><span
    style=\"color:#ff0000;\">GRUB_CMDLINE_LINUX=\"rd.lvm.lv=rootvg/usrlv rd.lvm.lv=rootvg/swaplv
    crashkernel=auto \r\nvconsole.keymap=usrd.lvm.lv=rootvg/rootlv vconsole.font=latarcyrheb-sun16
    rhgb \r\nquiet <strong><span style=\"color:#0000ff;\">net.ifnames=0 biosdevname=0</span></strong>\"</span></pre>\r\n<a
    href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-8.jpg\"><img class=\"aligncenter
    size-full wp-image-20154\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-8.jpg\"
    alt=\"centos7 (8)\" width=\"630\" height=\"153\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-8.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\nCreate a new configuration based on the currently
    running system using grub2-mkconfig command:\r\n<pre><span style=\"color:#ff0000;\">sudo
    grub2-mkconfig -o /boot/grub2/grub.cfg</span></pre>\r\n<a href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-9.jpg\"><img
    class=\"aligncenter size-full wp-image-20158\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-9.jpg\"
    alt=\"centos7 (9)\" width=\"630\" height=\"199\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-9.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\nRename the interface files by renaming the file
    \"<span style=\"color:#ff0000;\">/etc/sysconfig/network-scripts/ifcfg-en01...</span>\"\r\n<pre><span
    style=\"color:#ff0000;\">sudo mv /etc/sysconfig/network-scripts/ifcfg-eno16777736
    /etc/sysconfig/network-scripts/ifcfg-eth0</span></pre>\r\n<a href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-10.jpg\"><img
    class=\"aligncenter size-full wp-image-20160\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-10.jpg\"
    alt=\"centos7 (10)\" width=\"630\" height=\"73\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-10.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\nReboot the system:\r\n\r\n<a href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-11.jpg\"><img
    class=\"aligncenter size-full wp-image-20164\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-11.jpg\"
    alt=\"centos7 (11)\" width=\"630\" height=\"89\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-11.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\nAfter reboot, check the interface name:\r\n\r\n<a
    href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-12.jpg\"><img class=\"aligncenter
    size-full wp-image-20165\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-12.jpg\"
    alt=\"centos7 (12)\" width=\"630\" height=\"173\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-12.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\n<strong>4)</strong> Configure the static ip on
    the server:\r\n\r\nEdit the interface file underÂ <span style=\"color:#ff0000;\">/etc/sysconfig/network-scripts/</span>
    directory:\r\n<pre><span style=\"color:#ff0000;\">sudo vi /etc/sysconfig/network-scripts/ifcfg-eth0</span></pre>\r\n<a
    href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-13.jpg\"><img class=\"aligncenter
    size-full wp-image-20167\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-13.jpg\"
    alt=\"centos7 (13)\" width=\"630\" height=\"67\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-13.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\nHere is my <span style=\"color:#ff0000;\">ifcfg-eth0</span>
    file as a sample, please change it according to your requirement:\r\n<pre><span
    style=\"color:#ff0000;\">DEVICE=\"eth0\"\r\nONBOOT=yes</span>\r\n<span style=\"color:#ff0000;\">BOOTPROTO=static</span>\r\n<span
    style=\"color:#ff0000;\">IPADDR=192.168.250.50</span>\r\n<span style=\"color:#ff0000;\">NETMASK=255.255.255.0</span>\r\n<span
    style=\"color:#ff0000;\">GATEWAY=192.168.250.2</span>\r\n<span style=\"color:#ff0000;\">DNS1=192.168.250.2</span></pre>\r\n<a
    href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-14.jpg\"><img class=\"aligncenter
    size-full wp-image-20170\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-14.jpg\"
    alt=\"centos7 (14)\" width=\"630\" height=\"189\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-14.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\nStop and disable the NetworkManager service, because
    we don't need it on the server:\r\n<pre><span style=\"color:#ff0000;\">sudo systemctl
    stop NetworkManager </span>\r\n<span style=\"color:#ff0000;\">sudo systemctl disable
    NetworkManager</span></pre>\r\n<a href=\"https://junaid18183.files.wordpress.com/2015/03/centos7-15.jpg\"><img
    class=\"aligncenter size-full wp-image-20173\" src=\"https://junaid18183.files.wordpress.com/2015/03/centos7-15.jpg\"
    alt=\"centos7 (15)\" width=\"630\" height=\"147\" data-originalSrc=\"http://rbgeek.files.wordpress.com/2014/07/centos7-15.jpg\"
    data-rehosted=\"1\"></a>\r\n\r\nRestart the network service(Be careful, if you
    are connecting remotely, because you will be disconnected after issue this command):\r\n<pre><span
    style=\"color:#ff0000;\">sudo service network restart</span></pre>\r\n<a href=\"https://rbgeek.files.wordpress.com/2014/07/centos7-16.jpg\"><img
    class=\"aligncenter size-full wp-image-20175\" src=\"http://rbgeek.files.wordpress.com/2014/07/centos7-16.jpg\"
    alt=\"centos7 (16)\" width=\"630\" height=\"81\"></a>\r\n\r\nCheck the newly assigned
    static ip:\r\n\r\n<a href=\"https://rbgeek.files.wordpress.com/2014/07/centos7-17.jpg\"><img
    class=\"aligncenter size-full wp-image-20177\" src=\"http://rbgeek.files.wordpress.com/2014/07/centos7-17.jpg\"
    alt=\"centos7 (17)\" width=\"630\" height=\"174\"></a>\r\n\r\n<strong>5)</strong>
    Disable IPv6:\r\n\r\nFirst check that IPv6 is enabled or not:\r\n<pre><span style=\"color:#ff0000;\">lsmod
    | grep -i ipv6</span></pre>\r\n<a href=\"https://rbgeek.files.wordpress.com/2014/07/centos7-18.jpg\"><img
    class=\"aligncenter size-full wp-image-20180\" src=\"http://rbgeek.files.wordpress.com/2014/07/centos7-18.jpg\"
    alt=\"centos7 (18)\" width=\"630\" height=\"145\"></a>\r\n\r\nEdit the grub file:\r\n<pre><span
    style=\"color:#ff0000;\">sudo vi /etc/default/grub</span></pre>\r\n<a href=\"https://rbgeek.files.wordpress.com/2014/07/centos7-19.jpg\"><img
    class=\"aligncenter size-full wp-image-20182\" src=\"http://rbgeek.files.wordpress.com/2014/07/centos7-19.jpg\"
    alt=\"centos7 (19)\" width=\"630\" height=\"81\"></a>\r\n\r\nSearch for the line
    â\x80\x9C<span style=\"color:#ff0000;\">GRUB_CMDLINE_LINUX</span>â\x80\x9D and
    add the following at the beginning: â\x80\x9C<span style=\"color:#ff0000;\">ipv6.disable=1</span>â\x80³\r\n\r\nWill
    look like this:\r\n<pre><span style=\"color:#ff0000;\">GRUB_CMDLINE_LINUX=\"<strong><span
    style=\"color:#0000ff;\">ipv6.disable=1</span></strong>Â rd.lvm.lv=rootvg/usrlv...</span></pre>\r\n<a
    href=\"https://rbgeek.files.wordpress.com/2014/07/centos7-20.jpg\"><img class=\"aligncenter
    size-full wp-image-20184\" src=\"http://rbgeek.files.wordpress.com/2014/07/centos7-20.jpg\"
    alt=\"centos7 (20)\" width=\"630\" height=\"192\"></a>\r\n\r\nCreate a new configuration
    based on the currently running system using grub2-mkconfig command:\r\n<pre><span
    style=\"color:#ff0000;\">sudo grub2-mkconfig -o /boot/grub2/grub.cfg</span></pre>\r\n<a
    href=\"https://rbgeek.files.wordpress.com/2014/07/centos7-21.jpg\"><img class=\"aligncenter
    size-full wp-image-20186\" src=\"http://rbgeek.files.wordpress.com/2014/07/centos7-21.jpg\"
    alt=\"centos7 (21)\" width=\"630\" height=\"220\"></a>\r\n\r\nReboot the system:\r\n\r\n<a
    href=\"https://rbgeek.files.wordpress.com/2014/07/centos7-22.jpg\"><img class=\"aligncenter
    size-full wp-image-20188\" src=\"http://rbgeek.files.wordpress.com/2014/07/centos7-22.jpg\"
    alt=\"centos7 (22)\" width=\"630\" height=\"71\"></a>\r\n\r\nOnce again, check
    the IPv6 on the system:\r\n\r\n<a href=\"https://rbgeek.files.wordpress.com/2014/07/centos7-23.jpg\"><img
    class=\"aligncenter size-full wp-image-20189\" src=\"http://rbgeek.files.wordpress.com/2014/07/centos7-23.jpg\"
    alt=\"centos7 (23)\" width=\"630\" height=\"100\"></a>\r\n\r\n<strong>6)</strong>
    EPEL repository on Centos 7\r\n\r\nTo install the EPEL repository, issue the following
    command:\r\n<pre><span style=\"color:#ff0000;\">sudo rpm --import http://mirrors.nayatel.com/epel//RPM-GPG-KEY-EPEL-7</span>\r\n<span
    style=\"color:#ff0000;\">sudo rpm -Uvh http://mirrors.nayatel.com/epel/7/x86_64/e/epel-release-7-1.noarch.rpm</span></pre>\r\n<a
    href=\"https://rbgeek.files.wordpress.com/2014/07/centos7-24.jpg\"><img class=\"aligncenter
    size-full wp-image-20191\" src=\"http://rbgeek.files.wordpress.com/2014/07/centos7-24.jpg\"
    alt=\"centos7 (24)\" width=\"630\" height=\"66\"></a>\r\n\r\nList your new repos:\r\n<pre><span
    style=\"color:#ff0000;\">sudo yum repolist</span></pre>\r\n<a href=\"https://rbgeek.files.wordpress.com/2014/07/centos7-25.jpg\"><img
    class=\"aligncenter size-full wp-image-20193\" src=\"http://rbgeek.files.wordpress.com/2014/07/centos7-25.jpg\"
    alt=\"centos7 (25)\" width=\"630\" height=\"259\"></a>\r\n\r\n7) Enable iptables
    services(instead of firewalld):\r\n\r\nWhen you will try to start/restart the
    iptables on newly install server, will get this error:\r\n\r\n<a href=\"https://rbgeek.files.wordpress.com/2014/07/centos7-26.jpg\"><img
    class=\"aligncenter size-full wp-image-20195\" src=\"http://rbgeek.files.wordpress.com/2014/07/centos7-26.jpg\"
    alt=\"centos7 (26)\" width=\"630\" height=\"96\"></a>\r\n\r\nTo fix this error,
    install the iptables-services package:\r\n<pre><span style=\"color:#ff0000;\">sudoÂ yum
    install iptables-services</span></pre>\r\n<a href=\"https://rbgeek.files.wordpress.com/2014/07/centos7-27.jpg\"><img
    class=\"aligncenter size-full wp-image-20197\" src=\"http://rbgeek.files.wordpress.com/2014/07/centos7-27.jpg\"
    alt=\"centos7 (27)\" width=\"630\" height=\"82\"></a>\r\n\r\nRe-run the command
    to restart the iptables:\r\n<pre><span style=\"color:#ff0000;\">sudo service iptables
    restart</span></pre>\r\n<a href=\"https://rbgeek.files.wordpress.com/2014/07/centos7-28.jpg\"><img
    class=\"aligncenter size-full wp-image-20198\" src=\"http://rbgeek.files.wordpress.com/2014/07/centos7-28.jpg\"
    alt=\"centos7 (28)\" width=\"630\" height=\"69\"></a>\r\n\r\nHope this will help
    you!\r\n\r\nPlease Remember me in your prayers!\r\n\r\nEnjoyÂ <img src=\"http://s0.wp.com/wp-includes/images/smilies/icon_smile.gif?m=1129645325g\"
    alt=\":-)\">\r\n\r\n[contact-form][contact-field label='Name' type='name' required='1'/][contact-field
    label='Email' type='email' required='1'/][contact-field label='Website' type='url'/][contact-field
    label='Comment' type='textarea' required='1'/][/contact-form]\r\n\r\n </div>\";s:15:\"images_mirrored\";i:16;}"
---

