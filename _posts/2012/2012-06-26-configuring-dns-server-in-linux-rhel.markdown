---
layout: post
title: Configuring DNS server in linux (RHEL)
date: 2012-06-26 12:39:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '2051537005583985653'
---
<div dir="ltr" style="text-align:left;"><!--[if !mso]&gt;v\:* {behavior:url(#default#VML);} o\:* {behavior:url(#default#VML);} w\:* {behavior:url(#default#VML);} .shape {behavior:url(#default#VML);} &lt;![endif]--><!--[if gte mso 9]&gt;   800x600 &lt;![endif]--><!--[if gte mso 9]&gt;   Normal  0          false  false  false    EN-US  X-NONE  X-NONE                                 MicrosoftInternetExplorer4                                     &lt;![endif]--><!--[if gte mso 9]&gt;                                                                                                                                                                                                                                                                                          &lt;![endif]--><!--[if gte mso 10]&gt; /* Style Definitions */  table.MsoNormalTable  {mso-style-name:"Table Normal";  mso-tstyle-rowband-size:0;  mso-tstyle-colband-size:0;  mso-style-noshow:yes;  mso-style-priority:99;  mso-style-parent:"";  mso-padding-alt:0in 5.4pt 0in 5.4pt;  mso-para-margin:0in;  mso-para-margin-bottom:.0001pt;  mso-pagination:widow-orphan;  font-size:10.0pt;  font-family:"Times New Roman","serif";} &lt;![endif]--> 
<div class="MsoNormal"><a href="" name="pr6ch7sc1dbs"><b><span style="color:black;font-size:24pt;">Linux DNS and BIND Server</span></b></a><b><span style="color:black;font-size:24pt;"></span></b></div>
<div class="MsoNormal"><a href="" name="AEN10516"></a><span style="color:black;">Setting up a caching server for client local machines will reduce the load on the site's primary server. A caching only name server will find the answer to name queries and remember the answer the next time we need it. This will shorten the waiting time the next time significantly. For security reasons, it is very important that DNS doesn't exist between hosts on the corporate network and external hosts; it is far safer to simply use IP addresses to connect to external machines from the corporate network and vice-versa. </span></div>
<div class="MsoNormal"><span style="color:black;">In our configuration and installation we'll run BIND/DNS as non root-user and in a chrooted environment. We also provide you three different configurations; </span></div>
<ul type="disc">
<li class="MsoNormal" style="color:black;">one for a simple caching      name server only <i>client</i> </li>
<li class="MsoNormal" style="color:black;">one for a slave <i>secondary      server</i> </li>
<li class="MsoNormal" style="color:black;">one for a master name      server <i>primary server</i>. </li>
</ul>
<div class="MsoNormal"><span style="color:black;">The simple </span><span>caching</span><span style="color:black;"> name server configuration will be used for your servers that don't act as a master or slave name server, and the slave and master configurations will be used for your servers that act as a master name server and slave name server. Usually one of your servers acts as master, another one acts as slave and the rest act as simple </span><span>caching</span><span style="color:black;"> client name server. </span></div>
<div class="MsoNormal"><span style="color:black;">This is a graphical representation of the DNS configuration we use in this book. We try to show you different settings </span></div>
<div class="MsoNormal"><span style="color:black;"><br /></span></div>
<div class="MsoNormal"><!--[if !mso]&gt;v\:* {behavior:url(#default#VML);} o\:* {behavior:url(#default#VML);} w\:* {behavior:url(#default#VML);} .shape {behavior:url(#default#VML);} &lt;![endif]--><!--[if gte mso 9]&gt;   800x600 &lt;![endif]--><!--[if gte mso 9]&gt;   Normal  0          false  false  false    EN-US  X-NONE  X-NONE                                 MicrosoftInternetExplorer4                                     &lt;![endif]--><!--[if gte mso 9]&gt;                                                                                                                                                                                                                                                                                          &lt;![endif]--><!--[if gte mso 10]&gt; /* Style Definitions */  table.MsoNormalTable  {mso-style-name:"Table Normal";  mso-tstyle-rowband-size:0;  mso-tstyle-colband-size:0;  mso-style-noshow:yes;  mso-style-priority:99;  mso-style-parent:"";  mso-padding-alt:0in 5.4pt 0in 5.4pt;  mso-para-margin:0in;  mso-para-margin-bottom:.0001pt;  mso-pagination:widow-orphan;  font-size:10.0pt;  font-family:"Times New Roman","serif";} &lt;![endif]--><span><img alt="DNS caching name server" height="220" src="{{ site.baseurl }}/assets/%5CUsers%5Cjunedm%5CAppData%5CLocal%5CTemp%5Cmsohtmlclip1%5C01%5Cclip_image001.gif" width="497" /></span></div>
<ul type="disc">
<li class="MsoNormal" style="color:black;">Caching Only DNS </li>
<li class="MsoNormal" style="color:black;">Master DNS </li>
<li class="MsoNormal" style="color:black;">Slave DNS </li>
</ul>
<div class="MsoNormal"><span style="color:black;">on different servers. A lot of possibilities exist, and depend on your needs, and network architecture. </span></div>
<div class="MsoNormal"><span style="color:black;">These installation instructions assume </span></div>
<ul type="disc">
<li class="MsoNormal" style="color:black;">Commands are      Unix-compatible. </li>
<li class="MsoNormal" style="color:black;">The source path is <span>/var/tmp</span>.      <i>other paths are possible</i>. </li>
<li class="MsoNormal" style="color:black;">Installations were      tested on Red Hat Linux 6.1 and 6.2. </li>
<li class="MsoNormal" style="color:black;">All steps in the      installation will happen in super-user account root. </li>
<li class="MsoNormal" style="color:black;">ISC BIND version number      is 8.2.2-patchlevel5 </li>
</ul>
<div class="MsoNormal"><span style="color:black;">These are the Package(s) required: </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span style="color:black;">ISC BIND Homepage:<a href="http://www.faqs.org/docs/securing/appendixa.html#prtinxfp18"><span style="color:blue;">http://www.isc.org/</span></a> </span></div>
</td>
</tr>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span style="color:black;">ISC BIND FTP Site: <a href="http://www.faqs.org/docs/securing/appendixa.html#prtinxfp18"><span>204.152.184.27</span></a> </span></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><span style="color:black;">You must be sure to download: </span><span>bind-contrib.tar.gz, bind-doc.tar.gz, bind-src.tar.gz</span><span style="color:black;"> </span></div>
<div class="MsoNormal"><span style="color:black;">Before you decompress Tarballs and install, it is a good idea to make a list of files on the system before you install BIND, and one afterwards, and then compare them using diff to find out what file it placed where. Simply run <b>find</b> </span><b><span>/* &gt; DNS1</span></b><span style="color:black;"> before and <b>find</b> </span><b><span>/* &gt; DNS2</span></b><span style="color:black;"> after you install the software, and use <b>diff</b> </span><b><span>DNS1 DNS2 &gt; DNS-Installed</span></b><span style="color:black;"> to get a list of what changed. </span></div>
<div class="MsoNormal"><span style="color:black;">Compile and Decompress the tarball (tar.gz). </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span>          </span>[root@deep] /# <b>mkdir</b>  /var/tmp/bind</span></div>
<div class="MsoNormal"><span><span>          </span>[root@deep] /# <b>cp</b>  bind-contrib.tar.gz /var/tmp/bind/</span></div>
<div class="MsoNormal"><span><span>          </span>[root@deep] /# <b>cp</b>  bind-doc.tar.gz /var/tmp/bind/</span></div>
<div class="MsoNormal"><span><span>          </span>[root@deep] /# <b>cp</b>  bind-src.tar.gz /var/tmp/bind/</span></div>
<div class="MsoNormal"><span><span>          </span></span></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><span style="color:black;">We create a directory named bind to handle the tar archives and copy them to this new directory. </span></div>
<div class="MsoNormal"><span style="color:black;">Move into the new bind directory <b>cd</b> </span><span>/var/tmp/bind</span><span style="color:black;"> and decompress the tar files: </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span>          </span>[root@deep ]/bind# <b>tar</b> xzpf   bind-contrib.tar.gz</span></div>
<div class="MsoNormal"><span><span>          </span>[root@deep ]/bind# <b>tar</b> xzpf   bind-doc.tar.gz</span></div>
<div class="MsoNormal"><span><span>          </span>[root@deep ]/bind# <b>tar</b> xzpf   bind-src.tar.gz</span></div>
<div class="MsoNormal"><span><span>          </span></span></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><a href="" name="AEN10608"><b><span style="color:black;font-size:24pt;">21.2. Configure</span></b></a><b><span style="color:black;font-size:24pt;"></span></b></div>
<div class="MsoNormal"><span style="color:black;">Configuration files for different services are very specific depending on your needs and your network architecture. People can install DNS Servers at home as a </span><span>caching-only</span><span style="color:black;"> server, though companies may install it with </span><span>primary</span><span style="color:black;">, </span><span>secondary</span><span style="color:black;"> and </span><span>caching</span><span style="color:black;"> DNS servers. </span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><b><span style="color:black;"> </span></b><span style="color:black;">All the configuration files required for each software described in this book has been provided by us as a gzipped file, </span><span>floppy.tgz</span><span style="color:black;"> for your convenience. This can be downloaded from this web address: <a href="http://www.faqs.org/docs/securing/appendixa.html#sc24obecfrs2"><span style="color:blue;">http://www.openna.com/books/floppy.tgz</span></a> You can unpack this to any location on your local machine, say for example </span><span>/tmp</span><span style="color:black;">, assuming you have done this your directory structure will be </span><span>/tmp/floppy</span><span style="color:black;">. Within this floppy directory each configuration file has its own directory for respective software. For example <i>BIND-DNS</i>configuration file are organised like this: </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span>    </span>total 24</span></div>
<div class="MsoNormal"><span>drwxr-xr-x<span>    </span>2   harrypotter<span>    </span>harrypotter<span>        </span>4096 Jun<span>  </span>8 13:00 Caching-Only-DNS/</span></div>
<div class="MsoNormal"><span>-rw-r--r--<span>    </span>1   harrypotter<span>    </span>harrypotter<span>         </span>484 Jun<span>  </span>8 13:00 Compile-BIND</span></div>
<div class="MsoNormal"><span>drwxr-xr-x<span>    </span>2   harrypotter<span>    </span>harrypotter<span>        </span>4096 Jun<span>  </span>8 13:00 Primary-Master-DNS/</span></div>
<div class="MsoNormal"><span>drwxr-xr-x<span>    </span>2   harrypotter<span>    </span>harrypotter<span>        </span>4096 Jun<span>  </span>8 13:00 Secondary-Slave-DNS/</span></div>
<div class="MsoNormal"><span>-rwx------<span>    </span>1   harrypotter<span>    </span>harrypotter<span>         </span>300 Jun<span>  </span>8 13:00 bind.sh*</span></div>
<div class="MsoNormal"><span>drwxr-xr-x<span>    </span>3   harrypotter<span>    </span>harrypotter<span>        </span>4096 Jun<span>  </span>8 13:00 init.d/</span></div>
<div class="MsoNormal"><span><span>    </span></span><span></span></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><span style="color:black;">You can either cut and paste this directly if you are faithfully following our instructions from the begining or manually edit these to modify to your needs. This facility is there though as a convenience but please don't forget ultimately it will be your responsibility to check, verify, etc. before you use them whether modified or as it is. </span></div>
<div class="MsoNormal"><span style="color:black;">To run a </span><span>caching-only</span><span style="color:black;"> name server, the following files are required and must be created or copied to the appropriate directories on your server. </span></div>
<ol start="1" type="i">
<li class="MsoNormal" style="color:black;">Copy the <span>named.conf</span>     file to the <span>/etc/</span> directory. </li>
<li class="MsoNormal" style="color:black;">Copy the <span>db.127.0.0</span>     file to the <span>/var/named/</span> directory. </li>
<li class="MsoNormal" style="color:black;">Copy the <span>db.cache</span>     file to the <span>/var/named/</span> directory. </li>
<li class="MsoNormal" style="color:black;">Copy the <span>named</span>     script file to the <span>/etc/rc.d/init.d/</span> directory. </li>
</ol>
<div class="MsoNormal"><span style="color:black;">To run a </span><span>master</span><span style="color:black;"> name server, the following files are required and must be created or copied to the appropriate directories on your server. </span></div>
<ol start="1" type="i">
<li class="MsoNormal" style="color:black;">Copy the <span>named.conf</span>     file to the <span>/etc/</span> directory. </li>
<li class="MsoNormal" style="color:black;">Copy the <span>db.127.0.0</span>     file to the <span>/var/named/</span> directory. </li>
<li class="MsoNormal" style="color:black;">Copy the <span>db.cache</span>     file to the <span>/var/named/</span> directory. </li>
<li class="MsoNormal" style="color:black;">Copy the <span>db.208.164.186</span>     file to the <span>/var/named/</span> directory. </li>
<li class="MsoNormal" style="color:black;">Copy the <span>db.openna</span>     file to the <span>/var/named/</span> directory. </li>
<li class="MsoNormal" style="color:black;">Copy the <span>named</span>     script file to the <span>/etc/rc.d/init.d/</span> directory. </li>
</ol>
<div class="MsoNormal"><span style="color:black;">To run a slave name server, the following files are required and must be created or copied to the appropriate directories on your server. </span></div>
<ol start="1" type="i">
<li class="MsoNormal" style="color:black;">Copy the <span>named.conf</span>     file to the <span>/etc/</span> directory. </li>
<li class="MsoNormal" style="color:black;">Copy the <span>db.127.0.0</span>     file to the <span>/var/named/</span> directory. </li>
<li class="MsoNormal" style="color:black;">Copy the <span>db.cache</span>     file to the <span>/var/named/</span> directory. </li>
<li class="MsoNormal" style="color:black;">Copy the <span>named</span>     script file to the <span>/etc/rc.d/init.d/</span> directory. </li>
</ol>
<div class="MsoNormal"><b><span style="color:black;"><span> </span></span></b><span style="color:black;">You can obtain the configuration files listed over the next few sections on the </span><span>floppy.tgz</span><span style="color:black;"> archive. Copy the following files from the decompressed </span><span>floppy.tgz</span><span style="color:black;"> archive to the appropriate places, or copy them directly from this book to the concerned file.</span></div>
<div class="MsoNormal"><a href="" name="AEN10707"><b><span style="color:black;font-size:24pt;">21.3. </span></b></a><span><b><span>Caching-only</span></b></span><span><b><span style="color:black;font-size:24pt;"> name Server</span></b></span><b><span style="color:black;font-size:24pt;"></span></b></div>
<div class="MsoNormal"><span style="color:black;">Caching-only name servers are servers not authoritative for any domains except </span><span>0.0.127.in-addr.arpa</span><span style="color:black;">, the localhost. A </span><span>caching-only</span><span style="color:black;"> name server can look up names inside and outside your zone, as can primary and slave name servers. The difference is that when a </span><span>caching-only</span><span style="color:black;"> name server initially looks up a name within your zone, it ends up asking one of the primary or slave names servers for your zone for the answer. </span></div>
<div class="MsoNormal"><span style="color:black;">The necessary files to setup a simple caching name server are: </span></div>
<ol start="1" type="1">
<li class="MsoNormal" style="color:black;"><span>named.conf</span>     </li>
<li class="MsoNormal" style="color:black;"><span>db.127.0.0</span>     </li>
<li class="MsoNormal" style="color:black;"><span>db.cache</span>     </li>
<li class="MsoNormal" style="color:black;"><span>named script</span>     </li>
</ol>
<div class="MsoNormal"><span style="color:black;">To configure the </span><span>/etc/named.conf</span><span style="color:black;"> file for a simple caching name server, use this for all servers that dont act as a </span><span>master</span><span style="color:black;"> or </span><span>slave</span><span style="color:black;"> name server. Setting up a simple caching server for local client machines will reduce the load on the network's primary server. Many users on dialup connections may use this configuration along with bind for such a purpose. Create the </span><span>named.conf</span><span style="color:black;"> file, <b>touch</b> </span><span>/etc/named.conf</span><span style="color:black;"> and add the following lines to the file: </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>options {</span></div>
<div class="MsoNormal"><span><span> </span>directory "/var/named";</span></div>
<div class="MsoNormal"><span><span> </span>forwarders { 208.164.186.1; 208.164.186.2;   };</span></div>
<div class="MsoNormal"><span><span> </span>forward only;</span></div>
<div class="MsoNormal"><span><span> </span>};</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>//</span></div>
<div class="MsoNormal"><span><span> </span>// a caching only nameserver config</span></div>
<div class="MsoNormal"><span><span> </span>zone "." in {</span></div>
<div class="MsoNormal"><span><span> </span>type hint;</span></div>
<div class="MsoNormal"><span><span> </span>file "db.cache";</span></div>
<div class="MsoNormal"><span><span> </span>};</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>zone "0.0.127.in-addr.arpa" in {</span></div>
<div class="MsoNormal"><span><span> </span>type master;</span></div>
<div class="MsoNormal"><span><span> </span>file "db.127.0.0";</span></div>
<div class="MsoNormal"><span><span> </span>};</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><span style="color:black;"><a href="http://www.faqs.org/docs/securing/chap21sec164.html#frwdrs1"><span style="color:blue;text-decoration:none;"></span></a></span></div>
<div class="MsoNormal" style="margin-left:.5in;"><span style="color:black;">In the forwarders line, </span><span>208.164.186.1</span><span style="color:black;"> and </span><span>208.164.186.2</span><span style="color:black;"> are the IP addresses of your </span><span>Primary</span><span style="color:black;"> <i>Master</i> and </span><span>Secondary</span><span style="color:black;"> <i>Slave</i> DNS server. They can also be the IP addresses of your ISPs DNS server and another DNS server, respectively. </span></div>
<div class="MsoNormal"><b><span style="color:black;">: </span></b><span style="color:black;">To improve the security of your BIND/DNS server you can stop it from even trying to contact an off-site server if their forwarder is down or doesn't respond. With the </span><span>forward only</span><span style="color:black;"> option set in your </span><span>named.conf</span><span style="color:black;"> file, the name server doesn't try to contact other servers to find out information if the forwarder doesn't give it an answer. </span></div>
<div class="MsoNormal"><span style="color:black;">To configure the </span><span>/var/named/db.127.0.0</span><span style="color:black;"> file for a simple caching name server,you can use this configuration for all machines on your network that don't act as a master or slave name server. The </span><span>db.127.0.0</span><span style="color:black;"> file covers the loopback network. Create the following files in </span><span>/var/named/</span><span style="color:black;">, <b>touch</b> </span><span>/var/named/db.127.0.0</span><span style="color:black;"> and add the following lines in the file: </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>$TTL 345600</span></div>
<div class="MsoNormal"><span><span> </span>@<span>         </span>IN<span>      </span>SOA<span>     </span>localhost. root.localhost.<span>  </span>(</span></div>
<div class="MsoNormal"><span><span> </span>00<span>     </span>;   Serial</span></div>
<div class="MsoNormal"><span><span> </span>86400<span>  </span>;   Refresh</span></div>
<div class="MsoNormal"><span><span> </span>7200<span>   </span>;   Retry</span></div>
<div class="MsoNormal"><span><span> </span>2592000<span>       </span>;   Expire</span></div>
<div class="MsoNormal"><span><span> </span>345600 )<span>      </span>;   Minimum</span></div>
<div class="MsoNormal"><span><span> </span>IN<span>        </span>NS<span>      </span>localhost.</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>1<span>          </span>IN<span>      </span>PTR<span>     </span>localhost.</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><span style="color:black;">Configure the </span><span>/var/named/db.cache</span><span style="color:black;"> file for a simple caching name server before starting your DNS server. You must take a copy of </span><span>db.cache</span><span style="color:black;"> file and copy this file to the </span><span>/var/named/</span><span style="color:black;"> directory. The </span><span>db.cache</span><span style="color:black;"> tells your server where the servers for the root zone are. </span></div>
<div class="MsoNormal"><span style="color:black;">Use the following commands on another Unix computer in your organization to query a new </span><span>db.cache</span><span style="color:black;"> file for your DNS Server or pick one from your Red Hat Linux CD-ROM source distribution: </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>[root@deep]# <b>dig</b> @.aroot-servers.net   . ns &gt; db.cache</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><span style="color:black;">Don't forget to copy the </span><span>db.cache</span><span style="color:black;"> file to the </span><span>/var/named/</span><span style="color:black;"> directory on your server where you're installing DNS server after retrieving it over the Internet. </span></div>
<div class="MsoNormal"><span style="color:black;">Internal addresses like </span><span>192.168.1/24</span><span style="color:black;"> are not included in the DNS configuration files for security reasons. It is very important that DNS doesn't exist between hosts on the corporate network and external hosts. </span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><a href="" name="AEN10804"><b><span style="color:black;font-size:24pt;">21.4. Primary </span></b></a><span><b><span>master</span></b></span><span><b><span style="color:black;font-size:24pt;"> name Server</span></b></span><b><span style="color:black;font-size:24pt;"></span></b></div>
<div class="MsoNormal"><span style="color:black;">A primary </span><span>master</span><span style="color:black;"> name server for a zone reads the data for the zone from a file on it's host and are authoritative for that zone.The necessary files to setup a primary master name server are: </span></div>
<ol start="1" type="a">
<li class="MsoNormal" style="color:black;"><span>named.conf</span>     </li>
<li class="MsoNormal" style="color:black;"><span>db.127.0.0</span>     </li>
<li class="MsoNormal" style="color:black;"><span>db.208.164.186</span>     </li>
<li class="MsoNormal" style="color:black;"><span>db.openna</span>     </li>
<li class="MsoNormal" style="color:black;"><span>db.cache</span>     </li>
<li class="MsoNormal" style="color:black;"><span>named script</span>     </li>
</ol>
<div class="MsoNormal"><span style="color:black;">To configure the </span><span>/etc/named.conf</span><span style="color:black;"> file for a </span><span>master</span><span style="color:black;"> name server, use this configuration for the server on your network that acts as a master name server. After compiling DNS, you need to set up a </span><span>primary</span><span style="color:black;"> domain name for your server. We'll use </span><span>openna.com</span><span style="color:black;"> as an example domain, and assume you are using IP network address of </span><span>208.164.186.0.</span><span style="color:black;"> To do this, add the following lines to your </span><span>/etc/named.conf</span><span style="color:black;">. Create the </span><span>named.conf</span><span style="color:black;"> file <b>touch</b> </span><span>/etc/named.conf</span><span style="color:black;"> and add: </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>options {</span></div>
<div class="MsoNormal"><span><span> </span>directory "/var/named";</span></div>
<div class="MsoNormal"><span><span> </span>fetch-glue no;<span>                    </span></span></div>
<div class="MsoNormal"><span><span> </span>recursion no;<span>                     </span></span></div>
<div class="MsoNormal"><span><span> </span>allow-query { 208.164.186/24; 127.0.0/8;   };<span>  </span><a href="" name="alqr1"></a></span></div>
<div class="MsoNormal"><span><span> </span>allow-transfer { 208.164.186.2; };<span>           </span><a href="" name="altr1"></a></span></div>
<div class="MsoNormal"><span><span> </span>transfer-format many-answers;</span></div>
<div class="MsoNormal"><span><span> </span>};</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>// These files are not specific to any zone</span></div>
<div class="MsoNormal"><span><span> </span>zone "." in {</span></div>
<div class="MsoNormal"><span><span> </span>type hint;</span></div>
<div class="MsoNormal"><span><span> </span>file "db.cache";</span></div>
<div class="MsoNormal"><span><span> </span>};</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>zone "0.0.127.in-addr.arpa" in {</span></div>
<div class="MsoNormal"><span><span> </span>type master;</span></div>
<div class="MsoNormal"><span><span> </span>file "db.127.0.0";</span></div>
<div class="MsoNormal"><span><span> </span>};</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>// These are our primary zone files</span></div>
<div class="MsoNormal"><span><span> </span>zone "openna.com" in {</span></div>
<div class="MsoNormal"><span><span> </span>type master;</span></div>
<div class="MsoNormal"><span><span> </span>file "db.openna ";</span></div>
<div class="MsoNormal"><span><span> </span>};</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>zone "186.164.208.in-addr.arpa" in   {</span></div>
<div class="MsoNormal"><span><span> </span>type master;</span></div>
<div class="MsoNormal"><span><span> </span>file "db.208.164.186";</span></div>
<div class="MsoNormal"><span><span> </span>};</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><a href="/Users/junedm/AppData/Local/Temp/msohtmlclip1/01/clip_image003.gif" style="clear:left;float:left;margin-bottom:1em;margin-right:1em;"></a><span style="color:black;"><a href="http://www.faqs.org/docs/securing/chap21sec165.html#ftgl1"><span style="color:blue;text-decoration:none;"></span></a><a href="http://www.faqs.org/docs/securing/chap21sec165.html#rcsn1"><span style="color:blue;text-decoration:none;"><br /></span></a></span></div>
<div class="MsoNormal" style="margin-left:.5in;"><span style="color:black;">The </span><span>fetch-glue</span><span style="color:black;"> no option can be used in conjunction with the option </span><span>recursion no</span><span style="color:black;"> to prevent the server's cache from growing or becoming corrupted. Also, disabling recursion puts your name servers into a passive mode, telling it never to send queries on behalf of other name servers or resolvers. A non-recursive name server is very difficult to spoof, since it doesn't send queries, and hence doesn't cache any data. </span></div>
<div class="MsoNormal"><span style="color:black;"><a href="http://www.faqs.org/docs/securing/chap21sec165.html#alqr1"><span style="color:blue;text-decoration:none;"><br /></span></a></span></div>
<div class="MsoNormal" style="margin-left:.5in;"><span style="color:black;">In the allow-query line, 208.164.186/24 and 127.0.0/8 are the IP addresses allowed to ask ordinary questions to the server. </span></div>
<div class="MsoNormal"><span style="color:black;"><a href="http://www.faqs.org/docs/securing/chap21sec165.html#altr1"><span style="color:blue;text-decoration:none;"><br /></span></a></span></div>
<div class="MsoNormal" style="margin-left:.5in;"><span style="color:black;">In the allow-transfer line, 208.164.186.2 is the IP address allowed to receive zone transfers from the server. You must ensure that only your real slave name servers can transfer zones from your name serve, as the information provided is often used by spammers and IP spoofers. </span></div>
<div class="MsoNormal"><b><span style="color:black;">: </span></b><span style="color:black;">The options </span><span>recursion no</span><span style="color:black;">, </span><span>allow-query</span><span style="color:black;">, and </span><span>allow-transfer</span><span style="color:black;"> in the </span><span>named.conf</span><span style="color:black;"> file above are security features. </span></div>
<div class="MsoNormal"><span style="color:black;">To configure the </span><span>/var/named/db.127.0.0</span><span style="color:black;"> file for a master and slave name server, you can use this configuration file by both a master name server and a slave name server. The </span><span>db.127.0.0</span><span style="color:black;"> file covers the loopback network. Create the following files in </span><span>/var/named/</span><span style="color:black;">. </span></div>
<div class="MsoNormal"><span style="color:black;">Create the </span><span>db.127.0.0</span><span style="color:black;"> file, <b>touch</b> </span><span>/var/named/db.127.0.0</span><span style="color:black;"> and add: </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>; Revision History: April 22, 1999 -   admin@mail.openna.com</span></div>
<div class="MsoNormal"><span><span> </span>; Start of Authority (SOA) records.</span></div>
<div class="MsoNormal"><span><span> </span>$TTL 345600</span></div>
<div class="MsoNormal"><span><span> </span>@<span>    </span>IN<span>  </span>SOA<span>  </span>deep.openna.com.   admin.mail.openna.com.<span>  </span>(</span></div>
<div class="MsoNormal"><span><span> </span>00<span>     </span>;   Serial</span></div>
<div class="MsoNormal"><span><span> </span>86400<span>  </span>;   Refresh</span></div>
<div class="MsoNormal"><span><span> </span>7200<span>   </span>;   Retry</span></div>
<div class="MsoNormal"><span><span> </span>2592000<span>       </span>;   Expire</span></div>
<div class="MsoNormal"><span><span> </span>345600 )<span>      </span>;   Minimum</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>; Name Server (NS) records.</span></div>
<div class="MsoNormal"><span><span> </span>NS<span>     </span>deep.openna.com.</span></div>
<div class="MsoNormal"><span><span> </span>NS<span>     </span>mail.openna.com.</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>; only One PTR record.</span></div>
<div class="MsoNormal"><span><span> </span>1<span>        </span>PTR<span>  </span>localhost.</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><span style="color:black;">To configure the </span><span>/var/named/db.208.164.186</span><span style="color:black;"> file for a master name server, Use this configuration for the server on your network that acts as a master name server. The file </span><span>db.208.164.186</span><span style="color:black;"> maps host names to addresses. Create the following files in </span><span>/var/named/</span><span style="color:black;">. </span></div>
<div class="MsoNormal"><span style="color:black;">Create the </span><span>db.208.164.186</span><span style="color:black;"> file, <b>touch</b> </span><span>/var/named/db.208.164.186</span><span style="color:black;"> and add: </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>; Revision History: April 22, 1999 -   admin@mail.openna.com</span></div>
<div class="MsoNormal"><span><span> </span>; Start of Authority (SOA) records.</span></div>
<div class="MsoNormal"><span><span> </span>$TTL 345600</span></div>
<div class="MsoNormal"><span><span> </span>@<span>    </span>IN<span>  </span>SOA<span>  </span>deep.openna.com.   admin.mail.openna.com.<span>  </span>(</span></div>
<div class="MsoNormal"><span><span> </span>00<span>     </span>;   Serial</span></div>
<div class="MsoNormal"><span><span> </span>86400<span>  </span>;   Refresh</span></div>
<div class="MsoNormal"><span><span> </span>7200<span>   </span>;   Retry</span></div>
<div class="MsoNormal"><span><span> </span>2592000<span>       </span>;   Expire</span></div>
<div class="MsoNormal"><span><span> </span>345600 )<span>      </span>;   Minimum</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>; Name Server (NS) records.</span></div>
<div class="MsoNormal"><span><span> </span>NS<span>     </span>deep.openna.com.</span></div>
<div class="MsoNormal"><span><span> </span>NS<span>     </span>mail.openna.com.</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>; Addresses Point to Canonical Names (PTR)   for Reverse lookups</span></div>
<div class="MsoNormal"><span><span> </span>1<span>    </span>PTR<span>      </span>deep.openna.com.</span></div>
<div class="MsoNormal"><span><span> </span>2 <span> </span>PTR<span>        </span>mail.openna.com.</span></div>
<div class="MsoNormal"><span><span> </span>3<span>    </span>PTR<span>      </span>www.openna.com.</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><span style="color:black;">To configure of the </span><span>/var/named/db.openna</span><span style="color:black;"> file for a master name server, use this configuration for the server on your network that acts as a master name server. The file </span><span>db.openna</span><span style="color:black;"> maps addresses to host names. Create the following file in </span><span>/var/named/</span><span style="color:black;">. </span></div>
<div class="MsoNormal"><span style="color:black;">Create the </span><span>db.openna</span><span style="color:black;"> file <b>touch</b> </span><span>/var/named/db.openna</span><span style="color:black;"> and add: </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>; Revision History: April 22, 1999 -   admin@mail.openna.com</span></div>
<div class="MsoNormal"><span><span> </span>; Start of Authority (SOA) records.</span></div>
<div class="MsoNormal"><span><span> </span>$TTL 345600</span></div>
<div class="MsoNormal"><span><span> </span>@<span>    </span>IN<span>  </span>SOA<span>  </span>deep.openna.com.   admin.mail.openna.com.<span>  </span>(</span></div>
<div class="MsoNormal"><span><span> </span>00<span>     </span>;   Serial</span></div>
<div class="MsoNormal"><span><span> </span>86400<span>  </span>;   Refresh</span></div>
<div class="MsoNormal"><span><span> </span>7200<span>   </span>;   Retry</span></div>
<div class="MsoNormal"><span><span> </span>2592000<span>       </span>;   Expire</span></div>
<div class="MsoNormal"><span><span> </span>345600 )<span>      </span>;   Minimum</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>; Name Server (NS) records.</span></div>
<div class="MsoNormal"><span><span> </span>NS<span>     </span>deep.openna.com.</span></div>
<div class="MsoNormal"><span><span> </span>NS<span>     </span>mail.openna.com.</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>; Mail Exchange (MX) records.</span></div>
<div class="MsoNormal"><span><span> </span>MX<span>     </span>0<span>  </span>mail.openna.com.</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>; Address (A) records.</span></div>
<div class="MsoNormal"><span><span> </span>localhost<span>     </span>A<span>       </span>127.0.0.1</span></div>
<div class="MsoNormal"><span><span> </span>deep<span>   </span>A<span>       </span>208.164.186.1</span></div>
<div class="MsoNormal"><span><span> </span>mail<span>   </span>A<span>       </span>208.164.186.2</span></div>
<div class="MsoNormal"><span><span> </span>www<span>    </span>A<span>       </span>208.164.186.3</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>; Aliases in Canonical Name (CNAME) records.</span></div>
<div class="MsoNormal"><span><span> </span>;www<span>                           </span>CNAME<span>  </span>deep.openna.com.</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><span style="color:black;">To configure the </span><span>/var/named/db.cache</span><span style="color:black;"> file for a master and slave name servers Before starting your DNS server you must take a copy of the </span><span>db.cache</span><span style="color:black;"> file and copy it into the </span><span>/var/named/</span><span style="color:black;"> directory. The </span><span>db.cache</span><span style="color:black;"> tells your server where the servers for the root zone are. </span></div>
<div class="MsoNormal"><span style="color:black;">Use the following command on another Unix computer in your organization to query a new </span><span>db.cache</span><span style="color:black;"> file for your DNS Server or pick one from your Red Hat Linux CD-ROM source distribution: </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>dig</b>  @.aroot-servers.net . ns &gt; db.cache</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><span style="color:black;">Don't forget to copy the </span><span>db.cache</span><span style="color:black;"> file to the </span><span>/var/named/</span><span style="color:black;"> directory on your server where you're installing DNS server after retrieving it over the Internet. </span></div>
<div class="MsoNormal"></div>
<h1><a href="" name="AEN10913">21.5. </a><span><tt><span style="font-size:10pt;">Secondary</span></tt> slave name Server</span></h1>
<p>The purpose of a <tt><span style="font-size:10pt;">slave</span></tt> name server is to share the load with the <tt><span style="font-size:10pt;">master</span></tt>server, or handle the entire load if the <tt><span style="font-size:10pt;">master</span></tt>server is down. A <tt><span style="font-size:10pt;">slave</span></tt> name server loads its data over the network from another name server <em>usually the </em><tt><i><span style="font-size:10pt;">master</span></i></tt><em> name server, but it can load from another </em><tt><i><span style="font-size:10pt;">slave</span></i></tt><em>name server too</em>. This process is called a <span class="token">zone</span>transfer. Necessary files to setup a secondary slave name server are: <br /> 
<div style="margin-left:.5in;text-indent:-.5in;"><span><span>        </span>i.<span>            </span></span>named.conf </div>
<div style="margin-left:.5in;text-indent:-.5in;"><span><span>      </span>ii.<span>            </span></span>db.127.0.0 </div>
<div style="margin-left:.5in;text-indent:-.5in;"><span><span>    </span>iii.<span>            </span></span>db.cache </div>
<div style="margin-left:.5in;text-indent:-.5in;"><span><span>    </span>iv.<span>            </span></span>named script </div>
<p>To configure the <tt><span style="font-size:10pt;">/etc/named.conf</span></tt>file for a <tt><span style="font-size:10pt;">slave</span></tt> name server, use this configuration for the server on your network that acts as a <span class="token">slave</span> name server. You must modify the <tt><span style="font-size:10pt;">named.conf</span></tt> file on the <span class="token">slave</span>name server host. Change every occurrence of primary to secondary except for <tt><span style="font-size:10pt;">0.0.127.in-addr.arpa</span></tt> and add a masters line with the <span class="acronym">IP</span> address of the <tt><span style="font-size:10pt;">master</span></tt> server as shown below. <br />  Create the named.conf file (touch /etc/named.conf) and add: <br /> <br />
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<pre><span>   </span>options {</pre>
<pre><span>   </span>directory "/var/named";</pre>
<pre><span>   </span>fetch-glue no;</pre>
<pre><span>   </span>recursion no;</pre>
<pre><span>   </span>allow-query { 208.164.186/24; 127.0.0/8; };</pre>
<pre><span>   </span>allow-transfer { 208.164.186.1; };</pre>
<pre><span>   </span>transfer-format many-answers;</pre>
<pre><span>   </span>};</pre>
<pre> </pre>
<pre><span>   </span>// These files are not specific to any zone</pre>
<pre><span>   </span>zone "." in {</pre>
<pre><span>   </span>type hint;</pre>
<pre><span>   </span>file "db.cache";</pre>
<pre><span>   </span>};</pre>
<pre> </pre>
<pre><span>   </span>zone "0.0.127.in-addr.arpa" in {</pre>
<pre><span>   </span>type master;</pre>
<pre><span>   </span>file "db.127.0.0";</pre>
<pre><span>   </span>};</pre>
<pre> </pre>
<pre><span>   </span>// These are our slave zone files</pre>
<pre><span>   </span>zone "openna.com" in {</pre>
<pre><span>   </span>type slave;</pre>
<pre><span>   </span>file "db.openna";</pre>
<pre><span>   </span>masters { 208.164.186.1; };</pre>
<pre><span>   </span>};</pre>
<pre> </pre>
<pre><span>   </span>zone "186.164.208.in-addr.arpa" in {</pre>
<pre><span>   </span>type slave;</pre>
<pre><span>   </span>file "db.208.164.186";</pre>
<pre><span>   </span>masters { 208.164.186.1; };</pre>
<pre><span>   </span>};</pre>
<pre><span>   </span></pre>
</td>
</tr>
</tbody>
</table>
<p>This tells the name server that it is a <span class="token">slave</span> for the zone <tt><span style="font-size:10pt;">openna.com</span></tt> and should track the version of this zone that is being kept on the host <tt><span style="font-size:10pt;">208.164.186.1</span></tt>. <br />  A <tt><span style="font-size:10pt;">slave</span></tt> name server doesn't need to retrieve all of its database (db) files over the network because these db files <tt><span style="font-size:10pt;">db.127.0.0</span></tt> and <tt><span style="font-size:10pt;">db.cache</span></tt> are the same as on a <tt><span style="font-size:10pt;">primary</span></tt> master, so you can keep a local copy of these files on the slave name server. <br /> 
<div style="margin-left:.5in;text-indent:-.5in;"><span><span>        </span>i.<span>            </span></span>Copy the <tt><span style="font-size:10pt;">db.127.0.0</span></tt>file from <tt><span style="font-size:10pt;">master</span></tt> name server to <tt><span style="font-size:10pt;">slave</span></tt> name server. </div>
<div style="margin-left:.5in;text-indent:-.5in;"><span><span>      </span>ii.<span>            </span></span>Copy the <tt><span style="font-size:10pt;">db.cache</span></tt>file from <tt><span style="font-size:10pt;">master</span></tt> name server to <tt><span style="font-size:10pt;">slave</span></tt> name server. </div>
<h2><a href="" name="AEN10964">21.5.1. </a><span><tt><span style="font-size:10pt;">/etc/rc.d/init.d/named script </span></tt></span></h2>
<p>Configure your <tt><span style="font-size:10pt;">/etc/rc.d/init.d/named</span></tt>script file to start and stop the <span class="acronym">BIND</span>/<span class="acronym">DNS</span> daemon on your Server. This configuration script file can by used for all type of name server <tt><span style="font-size:10pt;">caching</span></tt>, <tt><span style="font-size:10pt;">master</span></tt> or <tt><span style="font-size:10pt;">slave</span></tt>. <br />  Create the named script file <b>touch</b> <tt><span style="font-size:10pt;">/etc/rc.d/init.d/named</span></tt>and add: <br /> <br />
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<pre><span>   </span>#!/bin/sh</pre>
<pre><span>   </span>#</pre>
<pre><span>   </span># named<span>           </span>This shell script takes care of starting and stopping</pre>
<pre><span>   </span>#<span>                 </span>named (BIND <span class="acronym">DNS</span> server).</pre>
<pre><span>   </span>#</pre>
<pre><span>   </span># chkconfig: - 55 45</pre>
<pre><span>   </span># description: named (BIND) is a Domain Name Server (<span class="acronym">DNS</span>) \</pre>
<pre><span>   </span># that is used to resolve host names to <span class="acronym">IP</span> addresses.</pre>
<pre><span>   </span># probe: true</pre>
<pre> </pre>
<pre><span>   </span># Source function library.</pre>
<pre><span>   </span>. /etc/rc.d/init.d/functions</pre>
<pre> </pre>
<pre><span>   </span># Source networking configuration.</pre>
<pre><span>   </span>. /etc/sysconfig/network</pre>
<pre> </pre>
<pre><span>   </span># Check that networking is up.</pre>
<pre><span>   </span>[ ${NETWORKING} = "no" ] &amp;&amp; exit 0</pre>
<pre> </pre>
<pre><span>  </span><span> </span>[ -f /usr/sbin/named ] || exit 0</pre>
<pre> </pre>
<pre><span>   </span>[ -f /etc/named.conf ] || exit 0</pre>
<pre> </pre>
<pre><span>   </span>RETVAL=0</pre>
<pre> </pre>
<pre><span>   </span># See how we were called.</pre>
<pre><span>   </span>case "$1" in</pre>
<pre><span>   </span>start)</pre>
<pre><span>   </span># Start daemons.</pre>
<pre><span>   </span>echo -n "Starting named: "</pre>
<pre><span>   </span>daemon named</pre>
<pre><span>   </span>RETVAL=$?</pre>
<pre><span>   </span>[ $RETVAL -eq 0 ] &amp;&amp; touch /var/lock/subsys/named</pre>
<pre><span>   </span>echo</pre>
<pre><span>   </span>;;</pre>
<pre><span>   </span>stop)</pre>
<pre><span>   </span># Stop daemons.</pre>
<pre><span>   </span>echo -n "Shutting down named: "</pre>
<pre><span>   </span>killproc named</pre>
<pre><span>   </span>RETVAL=$?</pre>
<pre><span>   </span>[ $RETVAL -eq 0 ] &amp;&amp; rm -f /var/lock/subsys/named</pre>
<pre><span>   </span>echo</pre>
<pre><span>   </span>;;</pre>
<pre><span>   </span>status)</pre>
<pre><span>   </span>/usr/sbin/ndc status</pre>
<pre><span>   </span>exit $?</pre>
<pre><span>   </span>;;</pre>
<pre><span>   </span>restart)</pre>
<pre> <span>  </span>$0 stop</pre>
<pre><span>   </span>$0 start</pre>
<pre><span>   </span>;;</pre>
<pre><span>   </span>reload)</pre>
<pre><span>   </span>/usr/sbin/ndc reload</pre>
<pre><span>   </span>exit $?</pre>
<pre><span>   </span>;; </pre>
<pre><span>   </span>probe)</pre>
<pre><span>   </span># named knows how to reload intelligently; we don't want linuxconf</pre>
<pre><span>   </span># to offer to restart every time</pre>
<pre><span>   </span>/usr/sbin/ndc reload &gt;/dev/null 2&gt;&amp;1 || echo start</pre>
<pre><span>   </span>exit 0</pre>
<pre><span>   </span>;;</pre>
<pre> </pre>
<pre><span>   </span>*)</pre>
<pre><span>   </span>echo "Usage: named {start|stop|status|restart}"</pre>
<pre><span>   </span>exit 1</pre>
<pre><span>   </span>esac</pre>
<pre> </pre>
<pre><span>   </span>exit $RETVAL</pre>
<pre><span>   </span></pre>
</td>
</tr>
</tbody>
</table>
<p>Now, make this script executable and change its default permissions: <br /> <br />
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<pre><span>   </span>[root@deep]# <b>chmod</b> 700<span>  </span>/etc/rc.d/init.d/named</pre>
<pre><span>   </span></pre>
</td>
</tr>
</tbody>
</table>
<p>Create the symbolic <tt><span style="font-size:10pt;">rc.d</span></tt>links for <span class="acronym">BIND</span>/<span class="acronym">DNS</span> with the command: <br /> <br />
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<pre><span>   </span>[root@deep]# <b>chkconfig</b> --add named</pre>
<pre><span>   </span></pre>
</td>
</tr>
</tbody>
</table>
<p>The <span class="acronym">BIND</span>/<span class="acronym">DNS</span> script will not automatically start the named daemon when you reboot the server. You can change its default by executing the following command: <br /> <br />
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<pre><span>   </span>[root@deep]# <b>chkconfig</b> --level 345 named on</pre>
<pre><span>   </span></pre>
</td>
</tr>
</tbody>
</table>
<p>Start your <span class="acronym">DNS</span> Server manually with the following command: <br /> <br />
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<pre><span>   </span>[root@deep]# /etc/rc.d/init.d/named <b>start</b></pre>
<pre><span>   </span></pre>
</td>
</tr>
</tbody>
</table>
<div style="margin:0;"></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<pre><tt> </tt></pre>
<pre><tt><span>   </span>Starting named:<span>                                            </span>[<span>  </span>OK<span>  </span>]</tt></pre>
<pre><tt><span>   </span></tt></pre>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"></div>
<div class="MsoNormal"><a href="" name="AEN10999"><b><span style="color:black;font-size:24pt;">21.6. Run ISC BIND/DNS in a chroot jail</span></b></a><b><span style="color:black;font-size:24pt;"></span></b></div>
<div class="MsoNormal"><a href="" name="AEN11004"></a><span style="color:black;">The main benefit of a chroot jail is that the jail will limit the portion of the file system the DNS daemon program can see to the root directory of the jail. Additionally, since the jail only needs to support DNS, the programs related to ISC BIND/DNS available in the jail can be extremely limited. Most importantly, there is no need for setuid-root programs, which can be used to gain root access and break out of the jail. </span></div>
<table border="1" cellpadding="0" class="MsoNormalTable">
<tbody>
<tr>
<td style="padding:3.75pt;">
<div class="MsoNormal"><a href="" name="AEN11011"></a><b><span style="color:black;">Securing ISC BIND/DNS</span></b><span style="color:black;"></span></div>
<div class="MsoNormal"><span style="color:black;">This part focuses on preventing ISC BIND/DNS from being   used as a point of break-in to the system hosting it. Since ISC BIND/DNS   performs a relatively large and complex function, the potential for bugs that   affect security is rather high with this software. In fact, there have been   exploitable bugs in the past that allowed a remote attacker to obtain root   access to hosts running ISC BIND/DNS. To minimize this risk, ISC BIND/DNS can   be run as a non-root user, which will limit any damage to what can be done as   a normal user with a local shell. Of course, this is not enough for the   security requirements of most DNS servers, so an additional step can be taken   - that is, running ISC BIND in a chroot jail. </span></div>
<div class="MsoNormal"><span style="color:black;"></span></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><b><span style="color:black;">: </span></b><span style="color:black;">The named binary program must be in a directory listed within your </span><span>PATH</span><span style="color:black;">environment variable for this to work. For the rest of the documentation, I'll assume the path of your original named program is </span><span>/usr/sbin/named</span><span style="color:black;">. </span></div>
<div class="MsoNormal"><span style="color:black;">The following are the necessary steps to run ISC BIND/DNS software in a chroot jail: </span></div>
<div class="MsoNormal"><span style="color:black;">We must find the shared library dependencies of named, <i>named is the DNS daemon</i>. These will need to be copied into the chroot jail later. </span></div>
<ol start="1" type="1">
<li class="MsoNormal" style="color:black;">To find the shared      library dependencies of named, execute the following command: </li>
</ol>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;margin-left:.5in;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>ldd</b> /usr/sbin/named</span></div>
<div class="MsoNormal"><span><span> </span>libc.so.6 =&gt; /lib/libc.so.6 (0x40017000)</span></div>
<div class="MsoNormal"><span><span> </span>/lib/ld-linux.so.2 =&gt; /lib/ld-linux.so.2   (0x40000000) </span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<ol start="2" type="1">
<li class="MsoNormal" style="color:black;">Make a note of the      files listed above; you will need these later in our steps. </li>
</ol>
<div class="MsoNormal"><span style="color:black;">Now we must set up the chroot environment, and create the root directory of the jail. We've chosen </span><span>/chroot/named</span><span style="color:black;"> because we want to put this on its own separate file system to prevent file system attacks. Early in our Linux installation procedure we created a special partition </span><span>/chroot</span><span style="color:black;"> for this purpose. </span></div>
<ol start="1" type="1">
<li class="MsoNormal" style="color:black;"> </li>
</ol>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;margin-left:.5in;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span>     </span>[root@deep] /# /etc/rc.d/init.d/named   stop <span> </span></span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<ol start="2" style="margin-top:0;" type="1">
<li class="MsoNormal" style="color:black;"><span style="color:blue;text-decoration:none;"></span></li>
<li class="MsoNormal" style="color:black;">Require only if an existing named daemon is running. </li>
</ol>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;margin-left:.5in;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"></div>
<div class="MsoNormal"><span><span> </span>Shutting down named:<span>                </span><span>              </span>[<span>  </span>OK<span>  </span>]</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<ol start="4" style="margin-top:0;" type="1">
<li class="MsoNormal" style="color:black;display:none;"><span style="display:none;"> </span></li>
</ol>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;margin-left:.5in;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>mkdir</b> -p /chroot/named</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<ol start="5" type="1">
<li class="MsoNormal" style="color:black;">Next, create the rest      of directories as follows: </li>
</ol>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;margin-left:.5in;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>mkdir</b>  /chroot/named/dev</span></div>
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>mkdir</b>  /chroot/named/lib</span></div>
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>mkdir</b>  /chroot/named/etc</span></div>
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>mkdir</b> -p   /chroot/named/usr/sbin</span></div>
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>mkdir</b> -p   /chroot/named/var/run</span></div>
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>mkdir</b>  /chroot/named/var/named</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<ol start="6" type="1">
<li class="MsoNormal" style="color:black;">Now copy the main      configuration file, the zone files, the named and the named-xfer programs      into the appropriate places in the chroot jail directory: </li>
</ol>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;margin-left:.5in;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>cp</b> /etc/named.conf   /chroot/named/etc/</span></div>
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>cd</b> /var/named ; cp -a   . /chroot/named/var/named/</span></div>
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>mknod</b>  /chroot/named/dev/null c 1 3</span></div>
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>chmod</b> 666   /chroot/named/dev/null</span></div>
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>cp</b> /usr/sbin/named   /chroot/named/usr/sbin/</span></div>
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>cp</b>  /usr/sbin/named-xfer /chroot/named/usr/sbin/</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal" style="margin-left:1in;text-indent:-.25in;"><span style="color:black;"><span>7.<span>      </span></span></span><b><span style="color:black;">: </span></b><span style="color:black;">The owner of the </span><span>/chroot/named/var/named</span><span style="color:black;"> directory and all files in this directory must be the process name named under the </span><span>slave</span><span style="color:black;"> server and only the </span><span>slave</span><span style="color:black;"> server or you wouldn't be able to make a </span><span>zone</span><span style="color:black;"> transfer. </span></div>
<ol start="8" type="1">
<li class="MsoNormal" style="color:black;">To make the <span>named</span>     directory and all its files own by the named process name under the <span>slave</span>     server, use the command: </li>
</ol>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;margin-left:.5in;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>chown</b> -R named.named   /chroot/named/var/named/</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><span style="color:black;">Copy the shared libraries identified above to the chrooted lib directory: </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>cp</b> /lib/libc.so.6   /chroot/named/lib/</span></div>
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>cp</b> /lib/ld-linux.so.2   /chroot/named/lib/</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><span style="color:black;">Copy the </span><span>localtime</span><span style="color:black;"> and </span><span>nsswitch.conf</span><span style="color:black;"> files to the chrooted </span><span>etc</span><span style="color:black;"> directory so that log entries are adjusted for your local timezone properly: </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>cp</b> /etc/localtime   /chroot/named/etc/</span></div>
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>cp</b> /etc/nsswitch.conf   /chroot/named/etc/</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"><span style="color:black;">We must set some files under the </span><span>/chroot/named/etc</span><span style="color:black;"> directory with the immutable bit enabled for better security: </span></div>
<ol start="1" type="1">
<li class="MsoNormal" style="color:black;">Set the immutable bit      on <span>nsswitch.conf</span> file: </li>
</ol>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;margin-left:.5in;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>cd</b> /chroot/named/etc/</span></div>
<div class="MsoNormal"><span><span> </span>[root@deep etc]# <b>chattr</b><span>  </span>+i nsswitch.conf</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<ol start="2" type="1">
<li class="MsoNormal" style="color:black;">Set the immutable bit      on <span>named.conf</span> file: </li>
</ol>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;margin-left:.5in;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>[root@deep] /# <b>cd</b> /chroot/named/etc/</span></div>
<div class="MsoNormal"><span><span> </span>[root@deep etc]# <b>chattr</b><span>  </span>+i named.conf</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<ol start="3" type="1">
<li class="MsoNormal" style="color:black;">A file with the +i      attribute cannot be modified, deleted or renamed; no link can be created      to this file and no data can be written to it. Only the superuser can set      or clear this attribute. </li>
</ol>
<div class="MsoNormal"><span style="color:black;">Add a new UID and a new GID for running the daemon </span><span>named</span><span style="color:black;"> if this is not already set. This is important because running it as root defeats the purpose of the jail, and using a different user id that already exists on the system can allow your services to access each others' resources. Check the </span><span>/etc/passwd</span><span style="color:black;"> and </span><span>/etc/group</span><span style="color:black;"> files for a free UID/GID number available. In our example we'll use the number 53 and the name named. </span></div>
<table border="0" cellpadding="0" class="MsoNormalTable" style="background:#E0E0E0;width:100%;">
<tbody>
<tr>
<td style="padding:.75pt;">
<div class="MsoNormal"><span><span> </span>[root@deep] /#<b>useradd</b> -c DNS Server   -u 53 -s /bin/false -r -d /chroot/named named 2&gt;/dev/null || :</span></div>
<div class="MsoNormal"></div>
</td>
</tr>
</tbody>
</table>
<div class="MsoNormal"></div>
<div class="MsoNormal"></div>
</div>
