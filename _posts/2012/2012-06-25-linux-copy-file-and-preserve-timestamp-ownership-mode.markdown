---
layout: post
title: Linux - copy file and preserve timestamp, ownership, mode
date: 2012-06-25 12:43:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7556973930929554912'
---
<div dir="ltr" style="text-align:left;">
<div>If you want to copy <span class="IL_AD" id="IL_AD7">files<span class="IL_AD_ICON"></span></span> in Linux and also want to keep or preserve the original mode or timestamp or ownership (or all) , cp <span class="IL_AD" id="IL_AD5">command<span class="IL_AD_ICON"></span></span> gives an option (--preserve).</p>
<p>From cp command man pages:</p>
<p>--preserve[=ATTR_LIST]<br />preserve the <span class="IL_AD" id="IL_AD12">specified<span class="IL_AD_ICON"></span></span> attributes (default: mode,ownership,timestamps) and <span class="IL_AD" id="IL_AD11">security<span class="IL_AD_ICON"></span></span> contexts, if possible additional attributes: links, all</p>
<p>Lets discuss this with some small <span class="IL_AD" id="IL_AD4">examples<span class="IL_AD_ICON"></span></span>.</p>
<p>I am logged in as user 'jk'</p>
<p>$ id<br />uid=32321(jk) gid=700(staff)</p>
<p>The example file tre.sh is having the following details:</p>
<p>$ ls -l tre.sh<br />-rw-r--r-- 1 jk staff 476 2009-01-13 16:20 tre.sh</p>
<p>Lets copy tre.sh to /tmp/tre.sh</p>
<p>$ cp tre.sh /tmp/tre.sh</p>
<p>So the timestamp is changed to the <span class="IL_AD" id="IL_AD10">present<span class="IL_AD_ICON"></span></span> timestamp</p>
<p>$ ls -l /tmp/tre.sh<br />-rw-r--r-- 1 jk staff 476 2009-02-05 15:10 /tmp/tre.sh</p>
<p>Now copy using "--preserve=timestamps" option.</p>
<p>$ cp --preserve=timestamps tre.sh /tmp/tre.sh.1</p>
<p>The original timestamp is preserved here</p>
<p>$ ls -l /tmp/tre.sh.1<br />-rw-r--r-- 1 jk staff 476 2009-01-13 16:20 /tmp/tre.sh.1</p>
<p>Now I just switched to root user</p>
<p>$ id<br />uid=0(root) gid=0(root) groups=0(root)</p>
<p>Copy tre.sh to /tmp/tre.sh.2</p>
<p>$ cp tre.sh /tmp/tre.sh.2</p>
<p><span class="IL_AD" id="IL_AD8">Notice<span class="IL_AD_ICON"></span></span> the ownership and timestamp of the /tmp/tre.sh.2</p>
<p>$ ls -l /tmp/tre.sh.2<br />-rw-r--r-- 1 root root 476 2009-02-05 15:13 /tmp/tre.sh.2</p>
<p>You can preserve the ownership like this:<br />$ cp --preserve=ownership tre.sh /tmp/tre.sh.4</p>
<p>So /tmp/tre.sh.4 is still owned by user jk" (copied by root though)<br />$ ls -l /tmp/tre.sh.4<br />-rw-r--r-- 1 jk staff 476 2009-02-05 15:14 /tmp/tre.sh.4</p>
<p>Also we can specify "--preserve=ownership,timestamps" and also preserve the mode(permission) of the file with "--preserve=mode"</p>
<p>The cp command -p option is <span class="IL_AD" id="IL_AD6">equivalent<span class="IL_AD_ICON"></span></span> to --preserve=mode,ownership,timestamps</p>
<p>I am still 'root'; now copy using -p option</p>
<p>$ cp -p tre.sh /tmp/tre.sh.5</p>
<p>All the original attributes (mode,permission,ownership) of tre.sh is preserved.</p>
<p>$ ls -l /tmp/tre.sh.5<br />-rw-r--r-- 1 jk staff 476 2009-01-13 16:20 /tmp/tre.sh.5 </div>
</div>
