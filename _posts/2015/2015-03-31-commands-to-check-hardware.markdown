---
layout: post
title: Commands to check hardware
date: 2015-03-31 09:32:57.000000000 +05:30
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
  post_id: '38'
  blog_id: '11361731'
  reblog_snapshot: "O:8:\"stdClass\":7:{s:5:\"title\";s:26:\"Commands to check hardware\";s:4:\"type\";s:4:\"post\";s:9:\"mime_type\";s:0:\"\";s:6:\"format\";b:0;s:12:\"modified_gmt\";s:19:\"2011-04-07
    10:10:33\";s:9:\"permalink\";s:68:\"https://imranceh.wordpress.com/2011/04/07/commands-to-check-hardware\";s:7:\"content\";s:2891:\"<div
    class=\"reblogged-content\">\n\nThe cool thing about linux is, everything in linux
    is a file. Hard disk, compact disk, memory, virtually anything is a file.\r\n\r\nDig
    the right files and you will get right info\r\n\r\n<strong>dmidecode</strong>
    gives a detailed list of hardware info ( one awesome command). If you are looking
    something specific try grep.\r\n\r\nYou can find out your hardware such as:\r\n*
    IPMI Device\r\n* Type of memory and speed\r\n* Chassis Information\r\n* Temperature
    Probe\r\n* Cooling Device\r\n* Electrical Current Probe\r\n* Processor and Memory
    Information\r\n* Serial numbers\r\n* BIOS version\r\n* PCI / PCIe Slots and Speed\r\n*
    Much more\r\n\r\nGeneral syntax is:\r\n<blockquote><strong><em>dmidecode --type
    {KEYWORD/NUMBER}</em></strong></blockquote>\r\nKeyword and numbers can be:\r\n\r\nKeyword                  
    \    Number\r\n\r\n──────────────────────────────\r\n\r\nbios                
                  0, 13\r\n\r\nsystem                      1, 12, 15, 23, 32\r\n\r\nbaseboard         
    \  2, 10, 41\r\n\r\nchassis                      3\r\n\r\nprocessor          
    \   4\r\n\r\nmemory                   5, 6, 16, 17\r\n\r\ncache                
    \         7\r\n\r\nconnector              8\r\n\r\nslot                                 9\r\n\r\n<strong>For
    BIOS info type</strong>\r\n<blockquote>dmidecode --type bios</blockquote>\r\n<blockquote>dmidecode
    --type 0</blockquote>\r\n<strong>For Motherboard info type</strong>\r\n<blockquote>dmidecode
    --type baseboard</blockquote>\r\n<strong>For processor related info type</strong>\r\n<blockquote>dmidecode
    --type processor</blockquote>\r\n<strong>For Manufacturer,Model and serial number
    </strong>\r\n<blockquote>dmidecode --type  system</blockquote>\r\n<p dir=\"ltr\"><strong>For
    more info  dig into man page</strong></p>\r\n<p dir=\"ltr\">man dmidecode</p>\r\n<strong>Specific
    commands</strong>\r\n\r\n0. CPU specifications\r\n<blockquote>cat /proc/cpuinfo</blockquote>\r\n1.
    kernel info\r\n<blockquote>uname -a</blockquote>\r\nkernel version\r\n<blockquote>uname
    -r</blockquote>\r\n3. pci cards\r\n<blockquote>cat /proc/pci</blockquote>\r\n4.
    Memory(RAM)  and swap information\r\n<blockquote>cat /proc/meminfo</blockquote>\r\n<blockquote>free
    -m</blockquote>\r\n5.Hard drives partitions\r\n<blockquote>fdisk -l</blockquote>\r\n6.
    free/used drive space\r\n<blockquote>df -h</blockquote>\r\n7. Disk usage by current
    directory and all subdirectories\r\n<blockquote>du | less</blockquote>\r\nanother
    command is <strong>du -sh /*</strong> to see top level directory wise disk usage\r\n\r\n8.
    dmesg to view the kernel ring buffer (error messages)\r\n<blockquote>dmesg | less</blockquote>\r\n<blockquote>dmesg
    | egrep ‘(SCSI|scsi0|ide0|hda|sda|serio|mice|eth0|eth1)’</blockquote>\r\n9.some
    other commands\r\n<blockquote>lspci ( lists pci device)\r\nlsusb ( lists usb device)</blockquote>\n</div>\";}"
---

