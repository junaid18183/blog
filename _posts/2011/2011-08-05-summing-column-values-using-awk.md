---
layout: post
title: Summing column values using AWK
author: juned
categories: [Linux,Bash]
tags: [bash,linux]
image: assets/images/bash.jpg
featured: true
hidden: true
comments: true

---
# Summing column values using AWK

if you have value like this
```
cat /tmp/juned.txt
juned_workers 0.03322
juned_workers 0
juned_workers 0.17053
juned_workers 0
juned_workers 0.41322
juned_workers 0
juned_workers 0.16864
juned_workers 0.05603
juned_workers 0
juned_workers 0.15836
juned_workers 5
```


and if you want the total of column 2 , awk will be handy

```
cat /tmp/juned.txt |  awk '{print "Row"NR " is "$2} { s += $2 } END { print "Total : ", s}'
Row1 is 0.03322
Row2 is 0
Row3 is 0.17053
Row4 is 0
Row5 is 0.41322
Row6 is 0
Row7 is 0.16864
Row8 is 0.05603
Row9 is 0
Row10 is 0.15836
Row11 is 5
Total :  6
```
