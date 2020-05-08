---
layout: post
title: 'Step by Step Guide: ganglia + graphite + cubism.js'
date: 2015-06-29 05:32:22.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  is_reblog: '1'
  post_id: '177'
  blog_id: '35977787'
  reblog_snapshot: "O:8:\"stdClass\":7:{s:5:\"title\";s:50:\"Step by Step Guide: ganglia
    + graphite + cubism.js\";s:4:\"type\";s:4:\"post\";s:9:\"mime_type\";s:0:\"\";s:6:\"format\";b:0;s:12:\"modified_gmt\";s:19:\"2014-05-23
    06:59:25\";s:9:\"permalink\";s:90:\"https://sakamotomsh.wordpress.com/2014/05/23/step-by-step-guide-ganglia-graphite-cubism-js\";s:7:\"content\";s:7249:\"<div
    class=\"reblogged-content\">\n\nIn this post, I'll build a monitoring infracture
    with ganglia, graphite, and cubism.js on CentOS 6 in AWS EC2. It is no easy to
    build such environment, I hope someone (including myself in the future) feels
    helpful by reading this post.\r\n\r\nSo let's get started.\r\n\r\nFirst off. disable
    iptables and selinux :)\r\n[sourcecode]\r\n/etc/init.d/iptables stop\r\nsetenforce
    permissive\r\n[/sourcecode]\r\n\r\nNext, setup graphite. Specifying Twisted version
    and Django version is essential.\r\n[sourcecode]\r\n#### setuptools&amp;pip\r\nyum
    -y install wget\r\nwget https://pypi.python.org/packages/source/s/setuptools/setuptools-3.6.tar.gz#md5=8f3a1dcdc14313c8334eb6af4f66ea0a\r\n#-----
    extract tarball and cd ----\r\npython setup.py install\r\neasy_install pip\r\n####
    Django and Graphite\r\nyum -y install gcc python-devel pycairo httpd mod_wsgi
    bitmap-fonts\r\npip install 'Twisted&lt;12.0'\r\npip install 'django&lt;1.4' 'django-tagging==0.3.1'\r\npip
    install carbon whisper graphite-web\r\n[/sourcecode]\r\n\r\nConfigure graphite.
    NOTE: If you need an original dashboard, you need to mount them as / (AFAIK there
    exists no easy solution except but mounting /).\r\n[sourcecode]\r\necho WSGIScriptAlias
    \"/graphite /opt/graphite/webapp/graphite/django.wsgi\" &gt;&gt; /etc/httpd/conf.d/wsgi.conf\r\ncp
    /opt/graphite/conf/graphite.wsgi.example /opt/graphite/webapp/graphite/django.wsgi\r\ncd
    /opt/graphite/webapp/graphite\r\necho DEBUG = True &gt; local_settings.py\r\npython
    manage.py syncdb\r\n#------- answer some questions ---------\r\nchown -R apache:apache
    /opt/graphite/storage/\r\ncd /opt/graphite/conf/\r\ncp carbon.conf.example carbon.conf\r\ncp
    storage-schemas.conf.example storage-schemas.conf\r\n[/sourcecode]\r\n\r\nStart
    carbon-cache and apache.\r\n[sourcecode]\r\n/etc/init.d/httpd start\r\n/opt/graphite/bin/carbon-cache.py
    start\r\n[/sourcecode]\r\n\r\nOK, lets continue to build ganglia. Prepare build-kits
    and retrieve sourcecode, and build RPMs.\r\n[sourcecode]\r\n####### Ganglia Build\r\nyum
    -y install rpm-build\r\nyum -y install gcc-c++ make automake autoconf libtool\r\nyum
    -y install python-devel expat-devel rrdtool-devel libpng-devel pcre-devel apr-devel
    freetype-devel libart_lgpl-devel\r\nyum -y install php php-gd\r\nrpm -ivh http://dl.fedoraproject.org/pub/epel/6/x86_64/libconfuse-2.7-4.el6.x86_64.rpm\r\nrpm
    -ivh http://dl.fedoraproject.org/pub/epel/6/x86_64/libconfuse-devel-2.7-4.el6.x86_64.rpm\r\n\r\nmkdir
    -p ~/rpmbuild/SOURCES\r\ncd\r\nwget -O ganglia-3.6.0.tar.gz \"http://downloads.sourceforge.net/project/ganglia/ganglia%20monitoring%20core/3.6.0/ganglia-3.6.0.tar.gz?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fganglia%2Ffiles%2Fganglia%2520monitoring%2520core%2F3.6.0%2F&amp;ts=1400806454&amp;use_mirror=cznic\"\r\nwget
    -O ganglia-web-3.5.12.tar.gz \"http://downloads.sourceforge.net/project/ganglia/ganglia-web/3.5.12/ganglia-web-3.5.12.tar.gz?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fganglia%2Ffiles%2Fganglia-web%2F3.5.12%2F&amp;ts=1400806532&amp;use_mirror=jaist\"\r\nmv
    ganglia-3.6.0.tar.gz ganglia-web-3.5.12.tar.gz  ~/rpmbuild/SOURCES\r\n### -------
    extract tarball and put *.spec and apache.conf to working directory ---\r\ncp
    apache.conf ~/rpmbuild/SOURCES/\r\nchown -R root:root ganglia.spec\r\nchown root:root
    ./ganglia-web.spec\r\nrpmbuild -ba ganglia.spec\r\n##### Install Ganglia\r\ncd
    ~/rpmbuild/RPMS/x86_64/\r\nrpm -ivh *rpm\r\ncd ~/rpmbuild/RPMS/noarch/\r\nrpm
    -ivh *rpm\r\n[/sourcecode]\r\n\r\nOK, modify gmetad.conf and gmond.conf as follows(unified
    diff format). NOTE: on EC2, multicast is prohibitted so we need set up to unicast.\r\n[sourcecode]\r\ndiff
    --git a/gmetad.conf b/gmetad.conf\r\nindex 7c4857d..5cb7fea 100644\r\n--- a/gmetad.conf\r\n+++
    b/gmetad.conf\r\n@@ -148,7 +148,7 @@ case_sensitive_hostnames 0\r\n #\r\n # The
    hostname or IP address of the Graphite server\r\n # default: unspecified\r\n-#
    carbon_server \"my.graphite.box\"\r\n+carbon_server \"127.0.0.1\"\r\n #\r\n #
    The port and protocol on which Graphite is listening\r\n # default: 2003\r\n@@
    -161,7 +161,7 @@ case_sensitive_hostnames 0\r\n # metric names exported by gmetad.
    Graphite uses dot-\r\n # separated paths to organize and refer to metrics.\r\n
    # default: unspecified\r\n-# graphite_prefix \"datacenter1.gmetad\"\r\n+graphite_prefix
    \"mycluster.gmetad\"\r\n #\r\n # A user-definable graphite path. Graphite uses
    dot-\r\n # separated paths to organize and refer to metrics.\r\ndiff --git a/gmond.conf
    b/gmond.conf\r\nindex eed595d..acab31d 100644\r\n--- a/gmond.conf\r\n+++ b/gmond.conf\r\n@@
    -27,7 +27,7 @@ globals {\r\n  * tag that will wrap all hosts collected by this
    instance.\r\n  */\r\n cluster {\r\n-  name = \"unspecified\"\r\n+  name = \"my
    cluster\"\r\n   owner = \"unspecified\"\r\n   latlong = \"unspecified\"\r\n   url
    = \"unspecified\"\r\n@@ -47,17 +47,18 @@ udp_send_channel {\r\n                        #
    this, the metrics may appear to come from any\r\n                        # interface
    and the DNS names associated with\r\n                        # those IPs will
    be used to create the RRDs.\r\n-  mcast_join = 239.2.11.71\r\n+  #mcast_join =
    239.2.11.71\r\n+  host = 127.0.0.1\r\n   port = 8649\r\n-  ttl = 1\r\n+  ttl =
    100\r\n }\r\n\r\n /* You can specify as many udp_recv_channels as you like as
    well. */\r\n udp_recv_channel {\r\n-  mcast_join = 239.2.11.71\r\n+  #mcast_join
    = 239.2.11.71\r\n   port = 8649\r\n-  bind = 239.2.11.71\r\n-  retry_bind = true\r\n+
    \ #bind = 239.2.11.71\r\n+  #retry_bind = true\r\n   # Size of the UDP buffer.
    If you are handling lots of metrics you really\r\n   # should bump it up to e.g.
    10MB or even higher.\r\n   # buffer = 10485760\r\n[/sourcecode]\r\n\r\nNow it's
    time to start gmond and gmetad\r\n[sourcecode]\r\n/etc/init.d/gmetad start\r\n/etc/init.d/gmond
    start\r\n[/sourcecode]\r\n\r\nOK, the last is to put a graphite dashboard alternatives,
    such as cubism.js. Put the following html to /var/www/html/monitor.html and view
    with your browser. Oops, assigned public IP is in the html. Substitute with your
    environment!!!\r\n\r\n[sourcecode]\r\n&lt;!DOCTYPE html&gt;\r\n&lt;meta charset=\"utf-8\"&gt;\r\n&lt;style&gt;\r\n
    \   @import url(http://fonts.googleapis.com/css?family=Yanone+Kaffeesatz:400,700);\r\n
    \   @import url(http://square.github.io/cubism/style.css);\r\n&lt;/style&gt;\r\n&lt;script
    src=\"http://d3js.org/d3.v3.min.js\" charset=\"utf-8\"&gt;&lt;/script&gt;\r\n&lt;script
    src=\"http://square.github.io/cubism/cubism.v1.js\"&gt;&lt;/script&gt;\r\n&lt;div
    id=\"body\"&gt; &lt;div id=\"graph\" /&gt;&lt;/div&gt;\r\n\r\n&lt;script&gt;\r\n//
    create context and horizon\r\nvar context = cubism.context().step( 1 * 60 * 1000
    ).size(960)\r\nvar graphite = context.graphite(\"http://54.178.12.43/graphite\")\r\nvar
    horizon = context.horizon().metric(graphite.metric).height(100)\r\n\r\n// draw
    graph\r\nvar metrics = [\"mycluster.gmetad.my_cluster.localhost_localdomain.cpu_idle\"];\r\n\r\nd3.select(\"#graph\").selectAll(\".horizon\")\r\n
    \     .data(metrics)\r\n      .enter()\r\n      .append(\"div\")\r\n      .attr(\"class\",
    \"horizon\")\r\n      .call(horizon);\r\n\r\n// set rule\r\nd3.select(\"#body\").append(\"div\")\r\n
    \ .attr(\"class\", \"rule\")\r\n  .call(context.rule());\r\n\r\n// set focus\r\ncontext.on(\"focus\",
    function(i) {\r\n    d3.selectAll(\".value\")\r\n        .style( \"right\", i
    == null ? null : context.size() - i + \"px\");\r\n});\r\n// set axis\r\nvar axis
    = context.axis()\r\nd3.select(\"#graph\").append(\"div\").attr(\"class\", \"axis\").append(\"g\").call(axis);\r\n&lt;/script&gt;\r\n[/sourcecode]\r\n\r\nThat's
    all. If you reach here without any trouble, you are lucky :)\r\n\r\nthanks for
    reading.</div>\";}"
---

