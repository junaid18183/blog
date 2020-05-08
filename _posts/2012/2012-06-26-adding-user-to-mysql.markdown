---
layout: post
title: Adding user to Mysql
date: 2012-06-26 14:34:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Mysql
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '1040468526902775581'
---
<div dir="ltr" style="text-align:left;">mysql&gt; GRANT ALL ON cacti.* TO cactiuser@<span class="IL_AD" id="IL_AD4">localhost<span class="IL_AD_ICON"></span></span> <span class="IL_AD" id="IL_AD6">IDENTIFIED<span class="IL_AD_ICON"></span></span> BY 'somepassword';<br />mysql&gt; flush <span class="IL_AD" id="IL_AD2">privileges<span class="IL_AD_ICON"></span></span>;</p>
<p>or adding a new user to MySQL you just need to add a new entry to user  table in database mysql. Below is an example of adding new user phpcake  with SELECT, INSERT and UPDATE privileges with the password  mypass  the SQL query is :<br />mysql&gt; use mysql;<br />Database changed</p>
<p>mysql&gt; <span class="IL_AD" id="IL_AD9">INSERT INTO<span class="IL_AD_ICON"></span></span> user (host, user, password, select_priv, insert_priv, update_priv) VALUES ('localhost', 'phpcake', PASSWORD('mypass'), 'Y', 'Y', 'Y');<br />Query OK, 1 row affected (0.20 sec)</p>
<p>mysql&gt; FLUSH PRIVILEGES;<br />Query OK, 1 row affected (0.01 sec)</p>
<p>mysql&gt; SELECT host, user, password FROM user WHERE user = 'phpcake';<br />+-----------+---------+------------------+<br />| host      | user    | password         |<br />+-----------+---------+------------------+<br />| localhost | phpcake | 6f8c114b58f2ce9e |<br />+-----------+---------+------------------+<br />1 row in set (0.00 sec)</p>
<p>When adding a new user remember to encrypt the <span class="IL_AD" id="IL_AD3">new password<span class="IL_AD_ICON"></span></span> using PASSWORD() function provided by MySQL. As you can see in the  above example the password mypass is encrypted to 6f8c114b58f2ce9e.</p>
<p>Notice the the FLUSH PRIVILEGES <span class="IL_AD" id="IL_AD7">statement<span class="IL_AD_ICON"></span></span>. This tells the server to reload the grant tables. If you don't use it then you won't be able to <span class="IL_AD" id="IL_AD8">connect<span class="IL_AD_ICON"></span></span> to mysql using the new <span class="IL_AD" id="IL_AD1">user account<span class="IL_AD_ICON"></span></span> (at least until the server is reloaded).</p>
<p>You can also specify other privileges to a new user by setting the values of these columns in user table to 'Y' when executing the INSERT query :</p>
<p>    * Select_priv<br />    * Insert_priv<br />    * Update_priv<br />    * Delete_priv<br />    * Create_priv<br />    * Drop_priv<br />    * Reload_priv<br />    * Shutdown_priv<br />    * Process_priv<br />    * File_priv<br />    * Grant_priv<br />    * References_priv<br />    * Index_priv<br />    * Alter_priv</p>
<p>I think you can guess what those privileges serve by <span class="IL_AD" id="IL_AD11">reading<span class="IL_AD_ICON"></span></span> it's name</p>
<p><a name="more"></a>I was just working on a new Bugzilla installation, and noticed their  grant command example, and thought I'd share it here as another example:</p>
<p>mysql&gt; GRANT SELECT, INSERT,<br />       UPDATE, DELETE, INDEX, ALTER, CREATE, LOCK TABLES,<br />       CREATE TEMPORARY TABLES, DROP, REFERENCES ON <span class="IL_AD" id="IL_AD10">bugs<span class="IL_AD_ICON"></span></span>.*<br />       TO bugs@localhost IDENTIFIED BY '$db_pass';</p>
<p>mysql&gt; FLUSH PRIVILEGES;</p>
<p>They  also show this syntax for changing the MySQL root user password, which  is a little different than the syntax I normally use, so I thought I'd  share that here as well:</p>
<p>mysql&gt; UPDATE user <br />       SET password = password('new_password') <br />       WHERE user = 'root';</p>
<p>mysql&gt; FLUSH PRIVILEGES; </p></div>
