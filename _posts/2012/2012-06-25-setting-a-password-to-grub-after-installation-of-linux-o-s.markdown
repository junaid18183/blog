---
layout: post
title: Setting a password to grub after installation of Linux O.S.
date: 2012-06-25 12:53:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '766894609127751050'
---
<div dir="ltr" style="text-align:left;">Hi All,</p>
<p>Everyone who is using linux knows that while installation we can set grub a password.<br />But if in case some one forgets to set a password for the same,then we can do it even after installation.<br />Here is the way to do it.<br />Please find the <span class="IL_AD" id="IL_AD2">attachment<span class="IL_AD_ICON"></span></span>.</p>
<blockquote class="tr_bq"><p>Note:-  you should be a root to do that.</p>
<p># grub-md5-crypt <br />(t will ask for a password then)<br />Password :- xyz<br />Retype  password :-  xyz</p>
<p>Password will then be created in an encrypted form.<br />Just copy that encrypted  password.</p>
<p>Then Go to <br /># vi  /boot/grub/grub.conf<br />Under the <span class="IL_AD" id="IL_AD3">option<span class="IL_AD_ICON"></span></span> “Hiddenmenu” write<br />Password  --md5  (paste the password which you have copied above)<br />Save <span class="IL_AD" id="IL_AD5">the file<span class="IL_AD_ICON"></span></span> and restart your machine to go into <span class="IL_AD" id="IL_AD7">single<span class="IL_AD_ICON"></span></span> user mode.<br />You’ll be unable to enter into it unless and until you press the “P” button to type the<br />Password which you have set for the grub.<br />Once you enter that, you are done.<br /> </p></blockquote>
</div>
