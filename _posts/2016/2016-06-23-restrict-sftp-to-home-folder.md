---
layout: post
title: Restrict SFTP to Home Folder
author: juned
categories: [Linux]
tags: [Linux, SFTP]
image: assets/images/linux.jpg
featured: true
hidden: false
comments: false
---
# Restrict SFTP to Home Folder
I had created a chrooted sftp account on centos 6 , but faced an issue that the user's were not able put/delete as the sftp requires root:root ownership of chrooted directory. I fixed it by changing the chrooted direcotry to one step above of user's home and set user's home set to `/.`

Below are the exact steps.

# Prerequisites:  openssh version 5.2
## Notes :

chroot home directory is: /mnt/home
User home directory is 'junedm' relative to chroot home, i.e. /mnt/home
The chrooting is done based on Group
The chrooting group is sftponly , and all user's should have that as group ( secondary group will also work)

Steps :

A] Add user , create chroot directory structure and fix permissions

Create the chroot directory and make sure the permissions of each directory from / till chroot is 755 and owned by root:root

```
[root@ggvaapp07 ~]# mkdir -p /mnt/home
[root@tiber~]# ls -ld /mnt ; ls -ld /mnt/home<br />
drwxr-xr-x. 3 root root 4096 Jun 23 03:31 /mnt<br />
drwxr-xr-x 2 root root 4096 Jun 23 03:31 /mnt/home
```

Add sftponly group.

```
[root@tiber ~]# groupadd sftponly
```

Add user , with secondary group as sftponly

```
[root@tiber /]# useradd junedm -G sftponly
[root@tiber /]# id junedm
uid=503(junedm) gid=505(junedm) groups=505(junedm),504(sftponly)
```

Change user’s home directory to `/username` ( this is very important otherwise you will not have put/delete permissions if you set that as /mnt/home/username) also set its shell to nologin so that he cannot ssh, only sftp

```
[root@tiber /]# usermod -d /junedm -s /sbin/nologin junedm
[root@tiber /]# cat /etc/passwd | grep juned
junedm:x:503:505::/junedm:/sbin/nologin
```

Add users chrooted home directory and set the ownership is user:chrootgroup , also change permission to be 775

```
[root@tiber home]# chmod 775 /mnt/home/junedm ; chown junedm:sftponly /mnt/home/junedm -R
[root@tiber home]# ls -ld /mnt/home/junedm
drwxrwxr-x 2 junedm sftponly 4096 Jun 23 03:44 /mnt/home/junedm
```

Create/change password for user

```
[root@ggvaapp07 /]# passwd junedm
Changing password for user junedm.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```
B] Create sshd configuration for sftp setup. 

Backup existing sshd_configuration
```
[root@tiber /]# cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
```

comment out the Subsystem line in the configuration line
```
[root@tiber /]# grep Subsystem /etc/ssh/sshd_config
#Subsystem      sftp    /usr/libexec/openssh/sftp-server
```

Add following block at the bottom of sshd_configuration file
```
###Added By Juned for chrooted sftp setup ##############
Subsystem sftp internal-sftp
Match Group sftponly
    ChrootDirectory        /mnt/home
    ForceCommand           internal-sftp -l VERBOSE
    GSSAPIAuthentication   no
    PasswordAuthentication yes
    PubkeyAuthentication   yes
     AllowAgentForwarding no
     AllowTcpForwarding no
     X11Forwarding no
#END
########################################################
```
Restart sshd
```
[root@tiber /]# /etc/init.d/sshd restart
Stopping sshd:                                             [  OK  ]
Starting sshd:                                             [  OK  ]
[root@tiber /]#
```
check log's ( in case if you want to find whats happening )
```
[root@tiber /]# tail -f /var/log/secure
```
Now connect from different machine using sftp and do get/put/delete operations,
```
[prod@james tmp]$ sftp junedm@tiber
Connecting to tiber...
junedm@tiber's password:
sftp&gt; put test.txt
Uploading test.txt to /junedm/test.txt
test.txt                                                                                                                             100%    0     0.0KB/s   00:00
sftp&gt; ls -l
-rw-r--r--    1 503      505             0 Jun 23 10:57 test.txt
sftp&gt; rm test.txt
Removing /junedm/test.txt
sftp&gt; cd /
sftp&gt; ls -l
drwxrwxr-x    2 503      504          4096 Jun 23 10:57 junedm
```

Confirm ssh is not working
```
[prod@ggvaapp03 tmp]$ ssh junedm@tiber
junedm@tiber's password:
This service allows sftp connections only.
Connection to tiber closed.
```
