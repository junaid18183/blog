---
layout: post
title: mysql auto increment Reset
author: juned
categories: [Linux,Mysql]
tags: [Mysql,Linux]
image: assets/images/mysql.jpg
featured: false
hidden: true
comments: true
---
# Mysql auto increment reset

in order to reset the auto_increment, or in a situation where some of the most recently added rows were deleted, use:

```
ALTER TABLE theTableInQuestion AUTO_INCREMENT=1234
```

And future insertions will be numbered from 1234 again; Unless you still had rows numbered greater than 1234. 
In that case the future insertions will start from the greatest number + 1
