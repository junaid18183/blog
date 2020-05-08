---
layout: post
title: Instaling Tomcat
date: 2012-06-25 14:01:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '2140773398718768588'
---
<div dir="ltr" style="text-align:left;">IMP LINK - http://www.meritonlinesystems.com/docs/apache_tomcat_redhat.html</p>
<p>installing  jakarta-tomcat-5.0.28.tar.gz + httpd-2.59.tar.gz with tomcat-connectors-1.2.26-src.tar.gz</p>
<p>1) <span class="IL_AD" id="IL_AD7">Install<span class="IL_AD_ICON"></span></span> apache using following steps<br />   - tar -xvzf httpd-2.0.59.tar.gz<br />   - cd httpd-2.0.59<br />   - ./configure --prefix=/usr/local/apache2<br />   - make<br />   - make install<br />   - start apache using /usr/local/apache2/bin/apachectl start<br />   - You can <span class="IL_AD" id="IL_AD4">check<span class="IL_AD_ICON"></span></span> by opening url http://<span class="IL_AD" id="IL_AD8">localhost<span class="IL_AD_ICON"></span></span> or http://192.168.4.26. You will see the apache default page here.<br />   - Or you can check port by $ netstat -tanpu | grep "80"<br />2) Now <span class="IL_AD" id="IL_AD1">install java<span class="IL_AD_ICON"></span></span><br />  - Install java in /usr/local/java directory. cd /usr/local/java<br />  - sh jdk-1_5_0_07-linux-i586.bin and follow the steps.<br />  - ln -s jdk-1_5_0_07   java<br />  - You have to set JAVA_HOME path as<br />  - JAVA_HOME=/usr/local/java/java<br />  - export JAVA_HOME<br />  - you can check by echo $JAVA_HOME</p>
<p>3) Install tomcat using following steps<br />  - Extract source jakarta-tomcat-5.0.28.tar.gz in /usr/loca/<br />  - ln -s jakarta-tomcat-5.0.28   tomcat<br />  - You can set CATALINA_HOME=/usr/local/tomcat<br />  - export CATALINA_HOME<br />  - Start tomcat using CATALINA_HOME/bin/startup.sh<br />  - You can see the tomcat default page using http://localhost:8080<br />  - Also check whether 8080 port is open using netstat</p>
<p>4) Install tomcat-connectors-1.2.26-src.tar.gz<br /> - tar xvzf tomcat-connectors-1.2.26-src.tar.gz<br /> - cd tomcat-connectors-1.2.26-src/native/<br /> - ./buildconf.sh<br /> - ./configure --with-apxs=/usr/local/apache2/bin/apxs<br /> - make<br /> - cp /jk/native/apache-2.0/mod_jk.so /usr/loca/apache2//<span class="IL_AD" id="IL_AD3">modules<span class="IL_AD_ICON"></span></span></p>
<p>4)  workers.properties<br />  - vi /usr/local/apache2/conf/worker.properties<br />  - Add following line in workers.properties<br />      # Setting variables<br />   workers.tomcat_home=/usr/local/jakarta/jakarta-tomcat-5.0.28/<br />   #workers.tomcat_home=/usr/local/jakarta/old_tomcat/tomcat<br />   workers.java_home=/usr/local/jakarta/jdk1.5.0_07/<br />   ps=/<br />   worker.list=wrkr<br />   worker.wrkr.port=8009<br />   worker.wrkr.host=localhost<br />   worker.wrkr.type=ajp13</p>
<p>5)httpd.conf<br />- Add <span class="IL_AD" id="IL_AD6">the line<span class="IL_AD_ICON"></span></span> in <span class="IL_AD" id="IL_AD2">Mail Server<span class="IL_AD_ICON"></span></span> configuration<br />  -  LoadModule jk_module modules/mod_jk.so<br />  -   JkWorkersFile "/usr/local/apache2/conf/worker.properties"<br />      JkLogFile "/usr/local/apache2//logs/mod_jk.log"<br />      JkLogLevel info<br />- Add Virtual As like<br />    <br />     ServerAdmin <a href="mailto:b.mahesh@drushti.in">b.mahesh@drushti.in</a><br />     DocumentRoot /home/htdocs/<br />     ServerName testtomcat.com<br />     DirectoryIndex index.jsp<br />    JkMount /*.jsp wrkr<br />    JkMount /servlet/* wrkr<br />   ErrorLog logs/testtomcat.com-error_log<br />    CustomLog logs/testtomcat.com-access_log common<br />  </p>
<p>6)<br /> server.xml<br /> <br />www.testtomcat.com<br />&lt;Context path=&quot;&quot;  docBase=&quot;/home/htdocs&quot; crossContext=&quot;false&quot; <span class="IL_AD" id="IL_AD10">debug<span class="IL_AD_ICON"></span></span>="0" reloadable="true" &gt; <br />&lt;Logger className=&quot;org.apache.<span class="IL_AD" id="IL_AD11">catalina<span class="IL_AD_ICON"></span></span>.logger.FileLogger" prefix="testtomcat." suffix=".txt" <span class="IL_AD" id="IL_AD5">timestamp<span class="IL_AD_ICON"></span></span>="true"/&gt;<br />  </div>
