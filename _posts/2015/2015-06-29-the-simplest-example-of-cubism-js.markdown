---
layout: post
title: the simplest example of cubism.js
date: 2015-06-29 06:04:42.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  is_reblog: '1'
  post_id: '86'
  blog_id: '35977787'
  reblog_snapshot: "O:8:\"stdClass\":7:{s:5:\"title\";s:33:\"the simplest example
    of cubism.js\";s:4:\"type\";s:4:\"post\";s:9:\"mime_type\";s:0:\"\";s:6:\"format\";b:0;s:12:\"modified_gmt\";s:19:\"2014-05-12
    13:39:36\";s:9:\"permalink\";s:78:\"https://sakamotomsh.wordpress.com/2014/05/12/the-simplest-example-of-cubism-js\";s:7:\"content\";s:3462:\"<div
    class=\"reblogged-content\">\n\nIn this post, I will show the simplest example
    of cubism.js, hoping that someone interested in cubism.js feels familiar quickly
    by using this post.\r\n\r\nTimeseries chart that cubism.js provides is acuired
    by the following steps.\r\n\r\n1. create context\r\n2. define metrics and metric
    accessor\r\n3. draw graphs in a way of D3.js\r\n4. add some components (axis,
    rules, ...)\r\n\r\nOK. Let's get started.\r\n\r\nFirst off, let's create context,
    which contains state of cubism.js. And create horizon(chart object) from context.\r\n\r\n[sourcecode]\r\nvar
    context = cubism.context();\r\nvar horizon = context.horizon();\r\n[/sourcecode]\r\n\r\nyou
    can change the values from default, such as graph size, steps, serverDelay, etc..
    See <a href=\"https://github.com/square/cubism/wiki/Context\"> here</a> for details.\r\n\r\nNext,
    we need to define metric accessor, which tells cubism.js how to get metric values\r\nwhen
    a metric name is specified. In this post, metric values are ramdom values whatever
    the metric name is.\r\nFor more details see <a href=\"https://github.com/square/cubism/wiki/Context#metric\">this
    part</a>.\r\n\r\n[sourcecode]\r\nfunction random_ma(name) {\r\nreturn context.metric(function(start,stop,step,callback){\r\nvar
    values = [];\r\nwhile ( +start &amp;lt; +stop ){\r\n+start += step; values.push(Math.random());\r\n}\r\ncallback(null,values);\r\n},
    name)\r\n}\r\n[/sourcecode]\r\n\r\nAnd tells cubism.js that this is a metric accessor\r\n\r\n[sourcecode]\r\nhorizon.metric(random_ma);\r\n[/sourcecode]\r\n\r\nAnd,
    next? That's all, folks. Draw the graph is just the same as D3.\r\n\r\n[sourcecode]\r\nvar
    metrics = [\"X,\"Y\",\"Z\"]\r\nd3.select(\"#graph\").selectAll(\".horizon\")\r\n.data(metrics)\r\n.enter()\r\n.append(\"div\")\r\n.attr(\"class\",
    \"horizon\")\r\n.call(horizon);\r\n[/sourcecode]\r\n\r\nThe following is a complete
    set. cut and paste and save them as \"index.html\",\r\nand view it with web browser.
    You don't need anything, such as apache.\r\n\r\nThanks for reading.\r\n\r\n[sourcecode]\r\n&lt;!DOCTYPE
    html&gt;\r\n&lt;meta charset=\"utf-8\"&gt;\r\n&lt;style&gt;\r\n    @import url(http://fonts.googleapis.com/css?family=Yanone+Kaffeesatz:400,700);\r\n
    \   @import url(http://square.github.io/cubism/style.css);\r\n&lt;/style&gt;\r\n&lt;script
    src=\"http://d3js.org/d3.v3.min.js\" charset=\"utf-8\"&gt;&lt;/script&gt;\r\n&lt;script
    src=\"http://square.github.io/cubism/cubism.v1.js\"&gt;&lt;/script&gt;\r\n&lt;div
    id=\"body\"&gt; &lt;div id=\"graph\" /&gt;&lt;/div&gt;\r\n\r\n&lt;script&gt;\r\n//
    create context and horizon\r\nvar context = cubism.context().size(960)\r\nvar
    horizon = context.horizon().extent([0,2])\r\n\r\n// define metric accessor\r\nfunction
    random_ma(name) {\r\n   return context.metric(function(start,stop,step,callback){\r\n
    \       var values = [];\r\n        while (+start &lt; +stop){ start = +start
    +step; values.push(Math.random());}\r\n       callback(null, values);\r\n   },
    name);\r\n}\r\n\r\n// draw graph\r\nvar metrics = [\"foo\",\"bar\",\"baz\"];\r\nhorizon.metric(random_ma);\r\n\r\nd3.select(\"#graph\").selectAll(\".horizon\")\r\n
    \     .data(metrics)\r\n      .enter()\r\n      .append(\"div\")\r\n      .attr(\"class\",
    \"horizon\")\r\n      .call(horizon);\r\n\r\n// set rule\r\nd3.select(\"#body\").append(\"div\")\r\n
    \ .attr(\"class\", \"rule\")\r\n  .call(context.rule());\r\n\r\n// set focus\r\ncontext.on(\"focus\",
    function(i) {\r\n    d3.selectAll(\".value\")\r\n        .style( \"right\", i
    == null ? null : context.size() - i + \"px\");\r\n});\r\n// set axis \r\nvar axis
    = context.axis()\r\nd3.select(\"#graph\").append(\"div\").attr(\"class\", \"axis\").append(\"g\").call(axis);\r\n&lt;/script&gt;\r\n[/sourcecode]\r\n</div>\";}"
---

