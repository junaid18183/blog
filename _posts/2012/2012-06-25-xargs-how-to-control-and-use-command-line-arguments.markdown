---
layout: post
title: 'xargs: How To Control and Use Command Line Arguments'
date: 2012-06-25 13:39:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '5907980718744100592'
---
<div dir="ltr" style="text-align:left;">xargs: How To Control and Use Command Line Arguments</p>
<p>I am trying  to use xargs command using shell pipes and not able to understand how to  control and use command line arguments. For example I'd like to find  out all *.c file located in 100s of sub-directories and move them to  another directory called ~/old.src. <span class="IL_AD" id="IL_AD10">How do I<span class="IL_AD_ICON"></span></span> use command line args with xargs to achieve the same?</p>
<p>xargs command is designed <span class="IL_AD" id="IL_AD8">to construct<span class="IL_AD_ICON"></span></span> argument lists and invoke other utility. xargs reads items from <span class="IL_AD" id="IL_AD7">the standard<span class="IL_AD_ICON"></span></span> input or pipes, delimited by blanks or newlines, and executes the command one or more times with any initial-arguments followed by items read from standard input. Blank lines on the standard input are ignored.<br />xargs is more safer and easy to use</p>
<p>xargs  functionality can be achived using the backquote feature of shell. But,  it offers more options. It can deal with blanks or special characters  in file names easily. It is often used with find, grep and other  commands.<br />xargs examples</p>
<p>For example following example will print 1 2 3 4 using xargs (echo command is default)<br />$ echo 1 2 3 4 | xargs echo<br />OR<br />$ echo 1 2 3 4 | xargs<br />You can force xargs to use at most max-args arguments per command line. For example following will use first two argument per command:<br />$ echo 1 2 3 4 | xargs -n 2<br />Find all .bak files in or below the current directory and delete them.<br />$ find . -name "*.bak" -type f -print | xargs /bin/rm -f<br />{} as the argument list marker</p>
<p>{} is the default argument list marker. You need to use {} this with various command which take more than two arguments <span class="IL_AD" id="IL_AD12">at a time<span class="IL_AD_ICON"></span></span>.  For example mv command need to know the file name. The following will  find all .bak files in or below the current directory and move them to  ~/.old.files directory:<br />$ find . -name "*.bak" -print0 | xargs -0 -I mv {} ~/old.files<br />You  can rename {} to something else. In the following example {} is renamed  as file. This is more readable as compare to previous example:<br />$ find . -name "*.bak" -print0 | xargs -0 -I file mv file ~/old.files<br />Where,</p>
<p>    1. -0 If there are blank spaces or characters (including newlines)  many commands will not work. This option take cares of file names with  blank space.<br />   2. -I Replace occurrences of replace-str in the initial-arguments  with names read from standard input. Also, unquoted blanks do not  terminate input items; instead the separator is the newline character.</p>
<p>Dealing file names with blank spaces and newline</p>
<p>The  following will work incorrectly if there are any filenames containing  newlines or spaces (it will find out all .mp3 file located in current  directory and play them using mplayer):<br />$ find . -iname "*.mp3" -print | xargs mplayer<br />To get rid of this problem use -0 option:<br />$ find . -iname "*.mp3" -print0 | xargs -0 -I mp3file mplayer mp3file<br />To find out all *.c file located in 100s of subdirectories and move them to another directory called ~/old.src, use:<br />$ find /path/to/dir -iname "*.c" -print0 | xargs -0 -I file mv file ~/old.src<br />Avoiding errors and <span class="IL_AD" id="IL_AD4">resource<span class="IL_AD_ICON"></span></span> hungry problems with xargs and find combo</p>
<p>To copy all media files to another location called /bakup/iscsi, you can use cp as follows:<br />$ cp -r -v -p /share/media/mp3/ /backup/iscsi/mp3<br />However, cp command may fail if an error occurs such as if <span class="IL_AD" id="IL_AD1">the number<span class="IL_AD_ICON"></span></span> of files is too large for the cp command to handle. xargs in <span class="IL_AD" id="IL_AD9">combination<span class="IL_AD_ICON"></span></span> with find can handle such operation nicely. xargs is more resource <span class="IL_AD" id="IL_AD2">efficient<span class="IL_AD_ICON"></span></span> and will not halt with an error:</p>
<p>$ find /share/media/mp3/ -type f -name "*.mp3" -print0 | xargs -0 -r -I file cp -v -p file --target-directory=/bakup/iscsi/mp3</p>
<p>Please note that <span class="IL_AD" id="IL_AD3">all of the above<span class="IL_AD_ICON"></span></span> commands are tested with GNU/xargs version. BSD and UNIX xargs command  may not have options such as -r. Please refer to your local xargs man  page for further info:<br />man xargs</div>
