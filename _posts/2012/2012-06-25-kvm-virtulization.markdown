---
layout: post
title: KVM- Virtulization
date: 2012-06-25 13:29:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '8916920111899271220'
---
<div dir="ltr" style="text-align:left;"><span>KVM is a part of RHCVA </span><span class="IL_AD" id="IL_AD4">study<span class="IL_AD_ICON"></span></span><span> which is Red Hat Certified Virtualisation Administrator.</span><br /><span>It  is a fully virtualised machine much better than XEN as we can store  UNLIMITED number of virtual machines on a single operating system  whereas only </span><span class="IL_AD" id="IL_AD3">FOUR<span class="IL_AD_ICON"></span></span><span> can be stored in XEN.</span><br /><span>Some </span><span class="IL_AD" id="IL_AD8">more information<span class="IL_AD_ICON"></span></span><span> about KVM.</span><br /><span>KVM is (Kernel-based Virtual Machine) is a full virtualization </span><span class="IL_AD" id="IL_AD6">solution<span class="IL_AD_ICON"></span></span><span> for Linux on x86 hardware containing virtualization extensions (Intel  VT or AMD-V). It consists of a loadable kernel module, kvm.ko, that  provides the core virtualization infrastructure and a processor specific  module, kvm-intel.ko or kvm-amd.ko. KVM also requires a modified QEMU  although work is underway to get the required changes upstream. </span><br /><span>Using KVM, one can run multiple virtual machines running unmodified Linux or </span><span class="IL_AD" id="IL_AD5">Windows<span class="IL_AD_ICON"></span></span><span> </span><span class="IL_AD" id="IL_AD9">images<span class="IL_AD_ICON"></span></span><span>. Each virtual machine has private virtualized hardware: a </span><span class="IL_AD" id="IL_AD7">network<span class="IL_AD_ICON"></span></span><span> card, disk, graphics </span><span class="IL_AD" id="IL_AD10">adapter<span class="IL_AD_ICON"></span></span><span>, etc.</span><br /><span>QEMU  supports two operating modes: user-mode emulation and system-mode  emulation. User-mode emulation allows a process built for one CPU to be  executed on another (performing dynamic translation of the </span><span class="IL_AD" id="IL_AD1">instructions<span class="IL_AD_ICON"></span></span><span> for the host CPU and converting Linux system calls appropriately).  System-mode emulation allows emulation of a full system, including  processor and assorted peripherals.</span></div>
