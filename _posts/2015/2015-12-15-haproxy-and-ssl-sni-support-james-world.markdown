---
layout: post
title: HAProxy and SSL SNI Support | James' World
date: 2015-12-15 14:11:19.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta: {}
---
<p>For CentOS 5 users, SNI requires you to build haproxy from source with a newer version of OpenSSL statically. The README tells you how to do that. Use the latest version of <a href="http://openssl.org/source/">OpenSSL</a> to avoid errors about missing function names.</p>
<pre>cd openssl-1.0.2
export STATICLIBSSL=/tmp/staticlibssl
make clean
./config --prefix=$STATICLIBSSL no-shared
make &amp;&amp; make test &amp;&amp; make install
cd ../haproxy-1.5*
make clean
make TARGET=linux26 USE_OPENSSL=1 SSL_INC=$STATICLIBSSL/include SSL_LIB=$STATICLIBSSL/lib ADDLIB=-ldl
service haproxy stop
make install
service haproxy start</pre>
<p>Source: <a href="http://www.jebriggs.com/blog/2015/01/haproxy-and-ssl-sni-support/">HAProxy and SSL SNI Support | James' World</a></p>
