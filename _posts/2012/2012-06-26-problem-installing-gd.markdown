---
layout: post
title: Problem installing GD
date: 2012-06-26 14:01:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3212456228976976676'
---
<div dir="ltr" style="text-align:left;">perl -MCPAN -e 'install GD' fails with error </p>
<p>This issue is resolved and here's the <span class="IL_AD" id="IL_AD5">summary<span class="IL_AD_ICON"></span></span> of what I found in order to resolve <span class="IL_AD" id="IL_AD2">the issue<span class="IL_AD_ICON"></span></span> in hopes it helps other users. </p>
<p><i>gdlib-config  is a script file that has been included in the open source distribution  of the gd library since version 2.0.26. we have the <span class="IL_AD" id="IL_AD8">Red Hat<span class="IL_AD_ICON"></span></span> gd library version 2.0.28 installed as an rpm however this distribution (RHEL AS 4) does not include gdlib-config! contacted Red Hat  support about this and they confirmed that gdlib-config is not part of  their official 2.0.28 distribution and they only began includin the  script as part of RHEL AS 5. So to resolve this, we <span class="IL_AD" id="IL_AD1">downloaded<span class="IL_AD_ICON"></span></span> the open source gd library from the following link:  http://www.boutell.com/gd/manual2.0.28.html#getgd decompressed/untarred  the file, and then ran ./configure from the gd-2.0.28 directory. once  the command had <span class="IL_AD" id="IL_AD4">completed<span class="IL_AD_ICON"></span></span> we copied the newly created gdlib-config file from the gd-2.0.28/config  directory to the /usr/bin directory and made the file executable by  running 'chmod 774 gdlib-config'. after that every one of the perl GD <span class="IL_AD" id="IL_AD6">modules<span class="IL_AD_ICON"></span></span> installed without error.</i></div>
