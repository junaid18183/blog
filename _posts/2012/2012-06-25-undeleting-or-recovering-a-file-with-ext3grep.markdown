---
layout: post
title: Undeleting or recovering a file with ext3grep
date: 2012-06-25 13:35:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '8312099810325709675'
---
<div dir="ltr" style="text-align:left;">
<div>I would like to say thank you to ext3grep.</p>
<p>It helped me to <span class="IL_AD" id="IL_AD5">restore<span class="IL_AD_ICON"></span></span> all my files, as expected some <span class="IL_AD" id="IL_AD1">manual<span class="IL_AD_ICON"></span></span><br />intervention was required, but I managed to restore all without a<br />single dd invocation <br /><span class="IL_AD" id="IL_AD12">I am<span class="IL_AD_ICON"></span></span> appending the story here, maybe it will be useful to others.</p>
<p>How I deleted part of my thesis work:</p>
<p>  $ rm -rf ps3/</p>
<p>and how ext3grep saved my bum <br />Background:</p>
<p>I had just adjusted the backup scripts, so I thought: "OK, I am safe, the<br />script replicates the data on another machine and also copy a tarball on the<br /><span class="IL_AD" id="IL_AD2">university<span class="IL_AD_ICON"></span></span> machine; I can _clean_up_ this old location..."</p>
<p>...wonder what?</p>
<p>Stupid me, I forgot to RUN the backup script!<br />And the last backup was two months old.</p>
<p>Time of the disaster:<br />After  June 25 2008 19:00<br />Before June 25 2008 20:30</p>
<p>I promptly umounted the partition after a couple of errors, because I was<br />messing with "mount --bind" on the precious data <span class="IL_AD" id="IL_AD10">directory<span class="IL_AD_ICON"></span></span>: I also had the<br />data exported on a nfs share and I wanted to show an "alias" to the <span class="IL_AD" id="IL_AD11">clients<span class="IL_AD_ICON"></span></span>.<br />(Yes, I was playing fool with precious data...)</p>
<p>Let's see what I can recover.</p>
<p>  $ export <span class="IL_AD" id="IL_AD9">IMAGE<span class="IL_AD_ICON"></span></span>=/dev/sda7<br />  $ ./ext3grep $IMAGE --dump-names</p>
<p>It shows files which I did NOT delete, they were accessible before I umounted<br />the partition.<br />Hmm, the files I am searching for do not appear at all, not even as DELETED, argh!<br />And even if the ps3/ dir is there, it is empty when I "--ls --inode" it.<br />Was it because of the "mount --bind" mess?</p>
<p>Let's search for a directory name which we know was in ps3/</p>
<p>  $ ./ext3grep $IMAGE --search 00_hello_spe<br />  Running ext3grep version 0.7.0<br />  Number of <span class="IL_AD" id="IL_AD4">groups<span class="IL_AD_ICON"></span></span>: 820<br />  Minimum / maximum journal block: 1545 / 35886<br />  Loading journal descriptors... sorting... done<br />  Journal transaction 408734 wraps around, some data blocks might have been lost of this transaction.<br />  Number of descriptors in journal: 25996; min / max sequence numbers: 404956 / 450124<br />  Blocks containing "00_hello_spe": 11708416</p>
<p>Good, there's a block of HOPE <br />Show the content of the block:</p>
<p>  $ ./ext3grep $IMAGE --ls --block 11708416<br />  Running ext3grep version 0.7.0<br />  Number of groups: 820<br />  Minimum / maximum journal block: 1545 / 35886<br />  Loading journal descriptors... sorting... done<br />  Journal transaction 408734 wraps around, some data blocks might have been lost of this transaction.<br />  Number of descriptors in journal: 25996; min / max sequence numbers: 404956 / 450124<br />  <span class="IL_AD" id="IL_AD8">Group<span class="IL_AD_ICON"></span></span>: 357</p>
<p>  Block 11708416 is a directory. The block is Unallocated</p>
<p>            .-- <span class="IL_AD" id="IL_AD3">File type<span class="IL_AD_ICON"></span></span> in dir_entry (r=regular file, d=directory, l=symlink)<br />            |          .-- D: Deleted ; R: Reallocated<br />  Indx Next |  Inode   | Deletion time                        Mode        File name<br />  ==========+==========+----------------data-from-inode------+-----------+=========<br />     0    1 d 5849089  D 1214417009 Wed Jun 25 20:03:29 2008  drwxr-xr-x  .<br />     1    2 d       2                                         drwxr-xr-x  ..<br />     2    3 d 5849091  D 1214417009 Wed Jun 25 20:03:29 2008  drwxr-xr-x  01_hello_spe_argp<br />     3    4 d 5849090  D 1214417007 Wed Jun 25 20:03:27 2008  drwxr-xr-x  00_hello_spe<br />     4    5 d 5849100  D 1214417007 Wed Jun 25 20:03:27 2008  drwxr-xr-x  02_vsum1_spe<br />     5    6 d 5849206  D 1214417008 Wed Jun 25 20:03:28 2008  drwxr-xr-x  quad<br />     6    7 d 5849101  D 1214417009 Wed Jun 25 20:03:29 2008  drwxr-xr-x  02_vsum1_ppe<br />     7    9 d 5849119  D 1214417008 Wed Jun 25 20:03:28 2008  drwxr-xr-x  03_mat_mat_spu<br />     8    9 d 5849175  D 1214417009 Wed Jun 25 20:03:29 2008  drwxr-xr-x  single_spe_simd_dev_template<br />     9  end d 5849210  D 1214417009 Wed Jun 25 20:03:29 2008  drwxr-xr-x  mat_mat_simd<br />    10  end d 5849184  D 1214417009 Wed Jun 25 20:03:29 2008  drwxr-xr-x  single_spe_simd_matmat64<br />    11  end d 5849159  D 1214417009 Wed Jun 25 20:03:29 2008  drwxr-xr-x  single_spe_simd_matmat_4x4<br />    12  end r 5849200  D 1214417009 Wed Jun 25 20:03:29 2008  rrw-r--r--  .single_spe_simd_matmat_4x4.swp<br />    13  end r 5849204  D 1214417008 Wed Jun 25 20:03:28 2008  rrw-r--r--  .single_spe_simd_matmat_4x4.swpx</p>
<p>Ok, this is all the stuff I have to recover.</p>
<p>Let's start form a simple one, important stuff is deeper in the dir tree, so a<br />first level try will show if I can recover stuff at all:</p>
<p>     8    9 d 5849175  D 1214417009 Wed Jun 25 20:03:29 2008  drwxr-xr-x  single_spe_simd_dev_template</p>
<p>  $ ./ext3grep $IMAGE --ls --inode 5849175<br />  Running ext3grep version 0.7.0<br />  Number of groups: 820<br />  Minimum / maximum journal block: 1545 / 35886<br />  Loading journal descriptors... sorting... done<br />  Journal transaction 408734 wraps around, some data blocks might have been lost of this transaction.<br />  Number of descriptors in journal: 25996; min / max sequence numbers: 404956 / 450124<br />  Inode is Unallocated<br />  Loading sda7.ext3grep.stage2............ done<br />  There is no directory block associated with inode 5849175.</p>
<p>Argh, no directory block associated with inode 5849175.<br />Let's see what the journal has to say:</p>
<p>  $ ./ext3grep $IMAGE --show-journal-inode 5849175<br />  Running ext3grep version 0.7.0<br />  Number of groups: 820<br />  Minimum / maximum journal block: 1545 / 35886<br />  Loading journal descriptors... sorting... done<br />  Journal transaction 408734 wraps around, some data blocks might have been lost of this transaction.<br />  Number of descriptors in journal: 25996; min / max sequence numbers: 404956 / 450124<br />  Copies of inode 5849175 found in the journal:</p>
<p>  --------------Inode 5849175-----------------------<br />  Generation Id: 2552992623<br />  uid / gid: 1000 / 1000<br />  mode: drwxr-xr-x<br />  size: 0<br />  num of <span class="IL_AD" id="IL_AD6">links<span class="IL_AD_ICON"></span></span>: 0<br />  sectors: 0 (--&gt; 0 indirect blocks).</p>
<p>  Inode Times:<br />  Accessed:       1214417009 = Wed Jun 25 20:03:29 2008<br />  File Modified:  1214417009 = Wed Jun 25 20:03:29 2008<br />  Inode Modified: 1214417009 = Wed Jun 25 20:03:29 2008<br />  Deletion time:  1214417009 = Wed Jun 25 20:03:29 2008</p>
<p>  Direct Blocks:</p>
<p>  --------------Inode 5849175-----------------------<br />  Generation Id: 2552992623<br />  uid / gid: 1000 / 1000<br />  mode: drwxr-xr-x<br />  size: 4096<br />  num of links: 3<br />  sectors: 8 (--&gt; 0 indirect blocks).</p>
<p>  Inode Times:<br />  Accessed:       1214415156 = Wed Jun 25 19:32:36 2008<br />  File Modified:  1210872172 = Thu May 15 19:22:52 2008<br />  Inode Modified: 1208277183 = Tue Apr 15 18:33:03 2008<br />  Deletion time:  0</p>
<p>  Direct Blocks: 11758520</p>
<p>Ok, so there is still a version of the inode with mode: d with a Direct Block<br />defined, let's see if we can get anything out of it:</p>
<p>  $ ./ext3grep $IMAGE --ls --block 11758520<br />  Running ext3grep version 0.7.0<br />  Number of groups: 820<br />  Minimum / maximum journal block: 1545 / 35886<br />  Loading journal descriptors... sorting... done<br />  Journal transaction 408734 wraps around, some data blocks might have been lost of this transaction.<br />  Number of descriptors in journal: 25996; min / max sequence numbers: 404956 / 450124<br />  Group: 358</p>
<p>  Block 11758520 is a directory. The block is Unallocated</p>
<p>            .-- File type in dir_entry (r=regular file, d=directory, l=symlink)<br />            |          .-- D: Deleted ; R: Reallocated<br />  Indx Next |  Inode   | Deletion time                        Mode        File name<br />  ==========+==========+----------------data-from-inode------+-----------+=========<br />     0    1 d 5849175  D 1214417009 Wed Jun 25 20:03:29 2008  drwxr-xr-x  .<br />     1    2 d 5849210  D 1214417009 Wed Jun 25 20:03:29 2008  drwxr-xr-x  ..<br />     2    3 r 7749646  D 1214417009 Wed Jun 25 20:03:29 2008  rrw-r--r--  Makefile<br />     3    4 d 5849176  D 1214417009 Wed Jun 25 20:03:29 2008  drwxr-xr-x  spu<br />     4    5 r 5849182  D 1214417009 Wed Jun 25 20:03:29 2008  rrw-r--r--  <span class="IL_AD" id="IL_AD7">template<span class="IL_AD_ICON"></span></span>.c<br />     5    6 r 5849177  D 1214417009 Wed Jun 25 20:03:29 2008  rrw-r--r--  template.d<br />     6    8 r 5849183  D 1214417009 Wed Jun 25 20:03:29 2008  rrwxr-xr-x  template<br />     7    8 r 5849186  D 1214417009 Wed Jun 25 20:03:29 2008  rrw-r--r--  4913<br />     8   10 r 5849181  D 1214417009 Wed Jun 25 20:03:29 2008  rrw-r--r--  template.o<br />    10  end r 5849186  D 1214417009 Wed Jun 25 20:03:29 2008  rrw-r--r--  problem_data.h<br />    11  end r 5849187  D 1214417009 Wed Jun 25 20:03:29 2008  rrw-r--r--  problem_data.h~</p>
<p>Yay, we walked down the directory. Can we restore a file?</p>
<p>  $ ./ext3grep $IMAGE --restore-inode 7749646<br />  $  mv RESTORED_FILES/inode.7749646 Makefile</p>
<p>Yatta! File restored!</p>
<p>And I repeated that manually for all the files I had to recover.<br />Well, I know that I could have automated the process with a wrapper script,<br />but the important thing is that the files are now back, and replicated on<br />multiple hosts as originally planned Many many thanks to Carlo Wood and ext3grep.  </div>
</div>
