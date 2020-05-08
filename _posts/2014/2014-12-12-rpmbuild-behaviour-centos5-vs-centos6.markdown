---
layout: post
title: 'rpmbuild behaviour: CentOS5 vs. CentOS6'
date: 2014-12-12 15:10:41.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  _publicize_pending: '1'
  is_reblog: '1'
  post_id: '318'
  blog_id: '313548'
  reblog_snapshot: "O:8:\"stdClass\":7:{s:5:\"title\";s:39:\"rpmbuild behaviour: CentOS5
    vs. CentOS6\";s:4:\"type\";s:4:\"post\";s:9:\"mime_type\";s:0:\"\";s:6:\"format\";b:0;s:12:\"modified_gmt\";s:19:\"2012-04-24
    12:32:12\";s:9:\"permalink\";s:71:\"http://blog.naresh.moe/2011/12/22/rpmbuild-behaviour-centos5-vs-centos6\";s:7:\"content\";s:1482:\"<div
    class=\"reblogged-content\">\n\nThose of you who've tried building RPMs for c5
    on a c6 machine might've faced the symptoms described in <a href=\"http://samixblog.blogspot.com/2011/11/yum-errno-3-error-performing-checksum.html\">http://samixblog.blogspot.com/2011/11/yum-errno-3-error-performing-checksum.html</a>\r\n\r\nThe
    cause seems to involve a couple of things: 1. c6 having adopted a stronger file
    digest algorithm (sha256 as opposed to md5 in c5) and 2. compressing the payload
    with xz (as opposed to nothing in c5).\r\n\r\nThis is easily remedied by passing
    relevant options to `rpmbuild' and `createrepo'.\r\n\r\nIf you're using <a href=\"https://github.com/jordansissel/fpm\">fpm</a>
    in your <a href=\"http://jenkins-ci.org\">CI</a>, you can now append the following
    to your fpm command invocation:\r\n<pre>--rpm-rpmbuild-define '_source_filedigest_algorithm
    md5' \r\n--rpm-rpmbuild-define '_binary_filedigest_algorithm md5' \r\n--rpm-rpmbuild-define
    '_source_payload nil' \r\n--rpm-rpmbuild-define '_binary_payload nil' </pre>\r\nAnd
    invoke createrepo as `createrepo -d -s sha1 --update /path/to/rpms/for/c5'\r\n\r\n<strong>UPDATE
    (2012-04-23):</strong>\r\n\r\nfpm now supports quick shortcuts to the above:\r\n<pre>%
    fpm --help\r\n[...]\r\n--rpm-digest sha512|md5|sha384|sha256|sha1 (rpm only) Select
    a digest\r\nalgorithm. md5 works on the most platforms. (default: \"md5\")\r\n--rpm-compression
    xz|gzip|bzip2 (rpm only) Select a compression method.\r\ngzip works on the most
    platforms. (default: \"gzip\")</pre>\n</div>\";}"
---

