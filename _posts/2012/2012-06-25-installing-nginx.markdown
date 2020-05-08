---
layout: post
title: Installing nginx
date: 2012-06-25 13:47:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '8800862306066828805'
---
<div dir="ltr" style="text-align:left;"><b><span class="IL_AD" id="IL_AD6">Install<span class="IL_AD_ICON"></span></span> Nginx </b> <br /><i>cd /opt<br />wget http://sysoev.ru/nginx/nginx-0.8.33.tar.gz</i><br /><i>tar -zxvf nginx-0.8.33.tar.gz<br />cd nginx-0.8.33<br />./<span class="IL_AD" id="IL_AD5">configure<span class="IL_AD_ICON"></span></span> --with-http_stub_status_module</i>
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote">Other option complied with configure as per <span class="IL_AD" id="IL_AD7">requirement<span class="IL_AD_ICON"></span></span><br />--prefix=/usr \<br />--sbin-path=/usr/sbin/nginx \<br />--conf-path=/etc/nginx/nginx.conf \<br />--error-log-path=/var/log/nginx/error.log \<br />--pid-path=/var/run/nginx/nginx.pid  \<br />--lock-path=/var/lock/nginx.lock \<br />--user=nginx \<br />--group=nginx \<br />--with-http_ssl_module \<br />--with-http_flv_module \<br />--with-http_gzip_static_module \<br />--http-log-path=/var/log/nginx/access.log \<br />--http-client-body-temp-path=/var/tmp/nginx/client/ \<br />--http-proxy-temp-path=/var/tmp/nginx/proxy/ \<br /> --http-fastcgi-temp-path=/var/tmp/nginx/fcgi/ </div>
</blockquote>
<div class="quote"></div>
<p><i>make</i><br /><i>make install</i></p>
<p><i>useradd -s /sbin/nologin -d /usr/local/nginx/html -M nginx</i><br /><i>passwd -l nginx</i>
<div class="quoteheader">Quote</div>
<div class="quote">Now in File # vi /usr/local/nginx/conf/nginx.conf<br />Uncomment or edit option <br />pid               logs/nginx.pid;</p>
<p>user              nginx nginx;</p>
<p>worker_processes  10;</p>
<p>events {<br />    worker_connections  1024;<br />}</p>
<p>And in httpd Tagged add lines<br />#http {</p>
<p>## <span class="IL_AD" id="IL_AD11">Common<span class="IL_AD_ICON"></span></span> options ##<br /> include options.conf;</p>
<p> ## Proxy settings ##<br /> include proxy.conf;</div>
<div class="quoteheader"></div>
<div class="quote">In File # vi /usr/local/nginx/conf/options.conf</p>
<blockquote><p>## Size Limits<br />  client_body_buffer_size     128K;<br />  client_header_buffer_size   1M;<br />  client_max_body_size          1M;<br />  large_client_header_buffers 8 8k;</p>
<p> ## Timeouts<br />  client_body_timeout   60;<br />  client_header_timeout 60;<br />  expires               24h;<br />  keepalive_timeout     60 60;<br />  send_timeout          60;</p>
<p> ## General Options<br />  ignore_invalid_headers   on;<br />  keepalive_requests      100;<br />  limit_zone gulag $binary_remote_addr 5m;<br />  recursive_error_pages    on;<br />  sendfile                 on;<br />  server_name_in_redirect off;<br />  server_tokens           off;</p>
<p> ## TCP options<br />  tcp_nodelay on;<br />  tcp_nopush  on;</p>
<p> ## Compression<br />  gzip              on;<br />  gzip_buffers      16 8k;<br />  gzip_comp_level   6;<br />  gzip_http_version 1.0;<br />  gzip_min_length   0;<br />  gzip_types        text/plain text/css image/x-icon <span class="IL_AD" id="IL_AD1">application<span class="IL_AD_ICON"></span></span>/x-perl application/x-httpd-cgi;<br />  gzip_vary         on;</p>
<p> ## Log Format<br />  log_format  main  '$remote_addr $host $remote_user [$time_local] "$request" '<br />                    '$status $body_bytes_sent "$http_referer" "$http_user_agent" '<br />                    '"$gzip_ratio"';</p></blockquote>
</div>
<div class="quoteheader"></div>
<div class="quote">In file /usr/local/nginx/conf/proxy.conf</p>
<p>
<blockquote class="tr_bq">## Proxy caching options<br />  proxy_buffering           on;<br />  proxy_cache_min_uses       3;<br />  proxy_cache_path          /usr/local/nginx/proxy_temp/ levels=1:2 keys_zone=cache:10m inactive=10m max_size=1000M;<br />  proxy_cache_valid         any 10m;<br />  proxy_ignore_client_abort off;<br />  proxy_intercept_errors    on;<br />  proxy_next_upstream       error timeout invalid_header;<br />  proxy_redirect            off;<br />  proxy_set_header          X-Forwarded-For $remote_addr;<br />  proxy_connect_timeout     60;<br />  proxy_send_timeout        60;<br />  proxy_read_timeout        60;</p></blockquote>
</div>
<div class="quoteheader"></div>
<div class="quote">Edit  file vi /usr/local/nginx/conf/nginx.conf in server tagged </div>
<div class="quote">
<blockquote class="tr_bq">Server {<br />location /nginx_status {<br />  stub_status on;<br />  access_log on;<br />  allow all; <br />   # you can specify ip for specific host <br />#  deny all;<br />}<br />•        For nginx_status_url: http://127.0.0.1/nginx_status</p></blockquote>
<p>Note Make sure line commented in file /usr/local/nginx/conf/nginx.conf</p></div>
<div class="quote">
<blockquote class="tr_bq">#    sendfile        on;<br />    #tcp_nopush     on;</p>
<p>    #keepalive_timeout  0;<br />#    keepalive_timeout  65;</p>
<p>    #gzip  on;</p></blockquote>
</div>
<p>Start nginx web <span class="IL_AD" id="IL_AD12">server<span class="IL_AD_ICON"></span></span>:<br /># /usr/<span class="IL_AD" id="IL_AD8">local<span class="IL_AD_ICON"></span></span>/nginx/sbin/nginx<br /># netstat -tulpn | grep :80<br /># <span class="IL_AD" id="IL_AD3">echo<span class="IL_AD_ICON"></span></span> ' /usr/local/nginx/sbin/nginx' &gt;&gt; /etc/rc.local</div>
