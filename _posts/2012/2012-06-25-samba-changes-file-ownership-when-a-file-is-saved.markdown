---
layout: post
title: Samba changes file ownership when a file is saved
date: 2012-06-25 13:56:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '9039541389447353518'
---
<div dir="ltr" style="text-align:left;">
<div><span class="IL_AD" id="IL_AD9">Question<span class="IL_AD_ICON"></span></span>: “When user B saves a word <span class="IL_AD" id="IL_AD3">document<span class="IL_AD_ICON"></span></span> that is owned by user A, the updated file is now owned by user B. Why is Samba doing this? How do I fix this?”</p>
<p>Word does the following when you modify/change a Word document: MS Word creates a new document with a temporary name. Word then closes the old document and <span class="IL_AD" id="IL_AD6">deletes<span class="IL_AD_ICON"></span></span> it, then renames the new document to the original document name. There is no <span class="IL_AD" id="IL_AD7">mechanism<span class="IL_AD_ICON"></span></span> by which Samba can in any way know that the new document really should be owned by the owners of the original file. Samba has no way of knowing that the file will be renamed by MS Word. As far as Samba is able to tell, the file that gets created is a new file, not one that the <span class="IL_AD" id="IL_AD1">application<span class="IL_AD_ICON"></span></span> (Word) is updating.</p>
<p>There  is a workaround to solve the permissions problem. It involves  understanding how you can manage file system behavior from within the  smb.conf file, as well as understanding how UNIX <span class="IL_AD" id="IL_AD12">file systems<span class="IL_AD_ICON"></span></span> work. Set on the directory in which you are changing Word <span class="IL_AD" id="IL_AD10">documents<span class="IL_AD_ICON"></span></span>:  chmod g+s `directory_name'. This ensures that all files will be created  with the group that owns the directory. In smb.conf share <span class="IL_AD" id="IL_AD2">declaration<span class="IL_AD_ICON"></span></span> section set:</p>
<p><span class="IL_AD" id="IL_AD11">force<span class="IL_AD_ICON"></span></span> create mode = 0660<br />force directory mode = 0770</p>
<p>These  two settings will ensure that all directories and files that get  created in the share will be readable/writable by the owner and group  set on the directory itself.</div>
</div>
