---
layout: post
title: Xen Virtual Machine -Quick-Start Guide
date: 2012-06-26 12:23:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7130093303208594581'
---
<div dir="ltr" style="text-align:left;">
<div>#################################<br /> __  __            _  _    ___  <br /> \ \/ /___ _ __   | || |  / _ \ <br />  \  // _ \ '_ \  | || |_| | | |<br />  /  \  __/ | | | |__   _| |_| |<br /> /_/\_\___|_| |_|    |_|(_)___/ </p>
<p>#################################</p>
<p>http://www.xen.org/</p>
<p>What is Xen?<br />============</p>
<p>Xen is a Virtual Machine Monitor (VMM) originally developed by the<br />Systems Research Group of the <span class="IL_AD" id="IL_AD2">University<span class="IL_AD_ICON"></span></span> of Cambridge Computer<br /><span class="IL_AD" id="IL_AD6">Laboratory<span class="IL_AD_ICON"></span></span>, as part of the UK-EPSRC funded XenoServers project.  Xen<br />is freely-distributable Open Source software, released under the GNU<br />GPL. Since its <span class="IL_AD" id="IL_AD8">initial<span class="IL_AD_ICON"></span></span> public release, Xen has grown a large<br />development community, spearheaded by xen.org (http://www.xen.org).</p>
<p>The 4.0 release offers excellent performance, hardware support and<br />enterprise-grade features such as x86_32-PAE, x86_64, SMP guests and<br />live relocation of VMs. Ports to Linux, NetBSD, FreeBSD and Solaris<br />are available from the community.</p>
<p>This file contains some quick-start instructions to <span class="IL_AD" id="IL_AD12">install<span class="IL_AD_ICON"></span></span> Xen on<br />your system. For full <span class="IL_AD" id="IL_AD4">documentation<span class="IL_AD_ICON"></span></span>, see the Xen <span class="IL_AD" id="IL_AD1">User Manual<span class="IL_AD_ICON"></span></span>. If this<br />is a pre-built release then you can find the manual at:<br /> <span class="IL_AD" id="IL_AD10">dist<span class="IL_AD_ICON"></span></span>/install/usr/share/doc/xen/pdf/user.pdf<br />If you have a source release, then 'make -C docs' will build the<br />manual at docs/pdf/user.pdf.</p>
<p>Quick-Start Guide<br />=================</p>
<p>First, there are a number of prerequisites for building a Xen source<br />release. Make sure you have all the following installed, either by<br />visiting the project webpage or installing a pre-built package<br />provided by your Linux distributor:<br />    * GCC v3.4 or later<br />    * GNU Make<br />    * GNU Binutils<br />    * Development install of zlib (e.g., zlib-dev)<br />    * Development install of Python v2.3 or later (e.g., python-dev)<br />    * Development install of curses (e.g., libncurses-dev)<br />    * Development install of openssl (e.g., openssl-dev)<br />    * Development install of x11 (e.g. xorg-x11-dev)<br />    * bridge-utils package (/sbin/brctl)<br />    * iproute package (/sbin/ip)<br />    * hotplug or udev<br />    * GNU bison and GNU flex</p>
<p>[NB. Unless noted otherwise, all the following steps should be<br />performed with root privileges.]</p>
<p>1. Download and untar the source tarball file. This will be a<br />   file named xen-unstable-src.tgz, or xen-$version-src.tgz.<br />   You can also pull the current version from the mercurial<br />   repository at http://xenbits.xensource.com/</p>
<p>    # tar xzf xen-unstable-src.tgz</p>
<p>   Assuming you are using the unstable tree, this will<br />   untar into xen-unstable. The rest of the instructions<br />   use the unstable tree as an example, substitute the<br />   version for unstable.</p>
<p>2. cd to xen-unstable (or whatever you sensibly rename it to).</p>
<p>On Linux:</p>
<p>3. For the very first build, or if you want to destroy existing<br />   .configs and build trees, perform the following steps:</p>
<p>    # make world<br />    # make install</p>
<p>   This will create and install onto the local machine. It will build<br />   the xen binary (xen.gz), and a linux kernel and modules that can be<br />   used in both dom0 and an unprivileged guest kernel (vmlinuz-2.6.x-xen),<br />   the tools and the documentation.</p>
<p>   You can override the destination for make install by setting DESTDIR<br />   to some value.</p>
<p>   The make command line defaults to building the kernel vmlinuz-2.6.x-xen.<br />   You can override this default by specifying KERNELS=kernelname. For<br />   example, you can make two kernels - linux-2.6-xen0<br />   and linux-2.6-xenU - which are smaller builds containing only selected<br />   modules, intended primarily for developers that don't like to wait<br />   for a full -xen kernel to build. The -xenU kernel is particularly small,<br />   as it does not contain any physical <span class="IL_AD" id="IL_AD9">device drivers<span class="IL_AD_ICON"></span></span>, and hence is<br />   only useful for guest domains.</p>
<p>   To make these two kernels, simply specify</p>
<p>   KERNELS="linux-2.6-xen0 linux-2.6-xenU"</p>
<p>   in the make command line.</p>
<p>4. To rebuild an existing tree without modifying the config:<br />    # make dist</p>
<p>   This will build and install xen, kernels, tools, and<br />   docs into the local dist/ directory.</p>
<p>   You can override the destination for make install by setting DISTDIR<br />   to some value.</p>
<p>   make install and make dist differ in that make install does the<br />   right things for your local machine (installing the appropriate<br />   version of hotplug or udev scripts, for example), but make dist<br />   includes all versions of those scripts, so that you can copy the dist<br />   directory to another machine and install from that distribution.</p>
<p>5. To rebuild a kernel with a modified config:</p>
<p>    # make linux-2.6-xen-config CONFIGMODE=menuconfig     (or xconfig)<br />    # make linux-2.6-xen-build<br />    # make linux-2.6-xen-install</p>
<p>   Depending on your config, you may need to use 'mkinitrd' to create<br />   an initial ram disk, just like a native system e.g.<br />    # depmod 2.6.18-xen<br />    # mkinitrd -v -f --with=aacraid --with=sd_mod --with=scsi_mod initrd-2.6.18-xen.img 2.6.18-xen</p>
<p>   Other systems may requires the use of 'mkinitramfs' to create the<br />   ram disk.<br />    # depmod 2.6.18-xen<br />    # mkinitramfs -o initrd-2.6.18-xen.img 2.6.18-xen</p>
<p>Python Runtime Libraries<br />========================</p>
<p>Xend (the Xen daemon) has the following runtime dependencies:</p>
<p>    * Python 2.3 or later.<br />      In many distros, the XML-aspects to the standard library<br />      (xml.dom.minidom etc) are broken out into a separate python-xml package.<br />      This is also required.</p>
<p>          URL:    http://www.python.org/<br />          Debian: python, python-xml</p>
<p>    * For optional SSL support, pyOpenSSL:<br />          URL:    http://pyopenssl.sourceforge.net/<br />          Debian: python-pyopenssl</p>
<p>    * For optional PAM support, PyPAM:<br />          URL:    http://www.pangalactic.org/PyPAM/<br />          Debian: python-pam</p>
<p>    * For optional XenAPI support in XM, PyXML:<br />          URL:    http://pyxml.sourceforge.net<br />          YUM:    PyXML</p>
<p>Intel(R) Trusted Execution Technology Support<br />=============================================</p>
<p>Intel's technology for safer computing, Intel(R) Trusted Execution Technology<br />(Intel(R) TXT), defines platform-level enhancements that provide the building<br />blocks for creating trusted platforms.  For <span class="IL_AD" id="IL_AD7">more information<span class="IL_AD_ICON"></span></span>, see<br />http://www.intel.com/technology/security/.</p>
<p>Intel(R) TXT support is provided by the Trusted Boot (tboot) module in<br />conjunction with minimal logic in the Xen hypervisor.</p>
<p>Tboot is an open source, pre- kernel/VMM module that uses Intel(R) TXT to<br />perform a measured and verified launch of an OS kernel/VMM.</p>
<p>The Trusted Boot module is available from<br />http://sourceforge.net/projects/tboot.  This project hosts <span class="IL_AD" id="IL_AD5">the code<span class="IL_AD_ICON"></span></span> in a<br />mercurial repo at http://tboot.sourceforge.net/hg/tboot.hg and contains<br />tarballs of the source.  Instructions in the tboot README describe how<br />to modify grub.conf to use tboot to launch Xen.</p>
<p>There are optional targets as part of Xen's top-level makefile that will<br />download and build tboot: install-tboot, build-tboot, dist-tboot, clean-tboot.<br />These will download the latest tar file from the SourceForge site using wget,<br />then build/install/dist according to Xen's settings.</div>
</div>
