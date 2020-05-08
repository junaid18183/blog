---
layout: post
title: Information about "PS" Command
date: 2012-06-25 14:05:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '8653042406064953586'
---
<div dir="ltr" style="text-align:left;">PID         USER     TTY         VIRT(VSZ)            RES(RSS)             STAT      %CPU    %MEM TIME+   COMMAND</p>
<p>On the display use can see the following process parameters:</p>
<p>USER                     :- username (only with u)<br />PID                         :- process ID - unique process identifier<br />TTY                         :- console with which the process is connected (? for daemons)<br />%CPU, %MEM   :- current utilization of those <span class="IL_AD" id="IL_AD10">resources<span class="IL_AD_ICON"></span></span><br />VSZ  and RSS       :- Virtual Segment Size and Resident Set Size (size of  two parts of process - that which can be moved to virtual memory, and  that which cannot)<br />STAT                      :- that is <span class="IL_AD" id="IL_AD9">the status<span class="IL_AD_ICON"></span></span> of the process: R – run-able S - sleeping, etc. as follows:</p>
<p>For BSD formats and when the stat keyword is used, additional characters may be displayed:</p>
<p>D                             :- Uninterruptible sleep (usually IO)<br />R                             :- Running or run-able (on run queue)<br />S                              :- Interruptible sleep (<span class="IL_AD" id="IL_AD4">waiting for<span class="IL_AD_ICON"></span></span> an event to <span class="IL_AD" id="IL_AD8">complete<span class="IL_AD_ICON"></span></span>)<br />T                              :- Stopped, either by a job control signal or because it is being traced.<br />W                            :- paging (not valid since the 2.6.xx kernel)<br />X                             :- dead (should never be seen)<br />Z                              :- Defunct ("zombie") process, <span class="IL_AD" id="IL_AD7">terminated<span class="IL_AD_ICON"></span></span> but not reaped by its parent.</p>
<p>&lt;                             :- high-priority (not nice to other users)<br />N                             :- low-priority (nice to other users)<br />L                              :- has pages locked into memory (for real-time and custom IO)<br />s                              :- is a session leader<br />l                               :- is multi-threaded (using CLONE_THREAD, like NPTL pthreads do)<br />+                             :- is in the foreground process group</p>
<p>START                   :- <span class="IL_AD" id="IL_AD1">this is the time<span class="IL_AD_ICON"></span></span> when the process has started to execute<br />TIME                      :- time used by the process<br />COMMAND        :- the <span class="IL_AD" id="IL_AD5">command line<span class="IL_AD_ICON"></span></span> of the process</div>
