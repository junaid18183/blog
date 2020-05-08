---
layout: post
title: removing the file -X
date: 2012-06-26 13:01:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7682990310165552674'
---
<div dir="ltr" style="text-align:left;">I have created a file named in my home folder named -x (just for curiocity that can it be deleted or not)<br />oops .... its problematic the file is not <span class="IL_AD" id="IL_AD5">deleting<span class="IL_AD_ICON"></span></span> now.</p>
<p>and then I Learned about ,</p>
<blockquote class="tr_bq"><p><i><b>rm -- -x</b></i></p></blockquote>
<p>-- means ignore any further options.<br />Usefule for lots of commands, not just rm</p>
<p><a name="more"></a></p>
<p># Try the <span class="IL_AD" id="IL_AD3">regular<span class="IL_AD_ICON"></span></span> rm command and enclose your <span class="IL_AD" id="IL_AD2">troublesome<span class="IL_AD_ICON"></span></span> filename in quotes. This may <span class="IL_AD" id="IL_AD1">solve the problem<span class="IL_AD_ICON"></span></span> of deleting files with <span class="IL_AD" id="IL_AD6">spaces<span class="IL_AD_ICON"></span></span> in their name, for example:  rm "File Name"</p>
<p>You can also remove some other characters in this manner, for example:<br />rm "filename;#"</p>
<p>The  quotes prevent the semicolon from being interpreted as a stacking  command. (Since you can string commands together in Unix with  semicolons, Unix will <span class="IL_AD" id="IL_AD7">interpret<span class="IL_AD_ICON"></span></span> a semicolon in a filename that way, unless you put it in quotes.)<br />#  You can also try renaming the problem file, using quotes around your  original filename, by entering: mv "filename;#" new_filename</p>
<p>If this command successfully renames the file, you can then use the rm command to <span class="IL_AD" id="IL_AD12">delete<span class="IL_AD_ICON"></span></span> the file using the <span class="IL_AD" id="IL_AD9">new name<span class="IL_AD_ICON"></span></span>.<br />#  If this doesn't work, insert a backslash ( \ ) before the  meta-character in your filename. The backslash causes the character that  follows to be interpreted literally. For example, to remove the file named my$project, enter: rm my\$project<br /># To remove a file whose name begins with a dash ( - ) character, refer to the file with the following syntax: rm ./-filename</p>
<p>Using  the redundant  ./  directory information prevents the dash from  occurring at the beginning of the filename, and being interpreted as an  option of the rm command.</div>
