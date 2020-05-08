---
layout: post
title: Preserving the Environment variable for sudo
date: 2013-12-17 08:30:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3053610126114617568'
---
<div dir="ltr" style="text-align:left;">There is setting in the suodoers file , using which you can preserve the environment variable while using sudo.</p>
<p>Its called env_keep, see how  I have preserved the YUM0 variable for sudo access.</p>
<p>{code}</p>
<p>#<br /># Preserving HOME has security implications since many programs<br /># use it when searching for configuration files. Note that HOME<br /># is already set when the the env_reset option is enabled, so<br /># this option is only effective for configurations where either<br /># env_reset is disabled or HOME is present in the env_keep list.<br />#<br />Defaults    always_set_home</p>
<p>Defaults    env_reset<br />Defaults    env_keep =  "COLORS DISPLAY HOSTNAME HISTSIZE INPUTRC KDEDIR LS_COLORS"<br />Defaults    env_keep += "MAIL PS1 PS2 QTDIR USERNAME LANG LC_ADDRESS LC_CTYPE"<br />Defaults    env_keep += "LC_COLLATE LC_IDENTIFICATION LC_MEASUREMENT LC_MESSAGES"<br />Defaults    env_keep += "LC_MONETARY LC_NAME LC_NUMERIC LC_PAPER LC_TELEPHONE"<br />Defaults    env_keep += "LC_TIME LC_ALL LANGUAGE LINGUAS _XKB_CHARSET XAUTHORITY"<br />Defaults    env_keep += "YUM0"</p>
<p>{code}</div>
