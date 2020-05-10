---
layout: post
title:  "Taint all resources from one module"
description: "Terraform: taint all resources from one module"
author: juned
categories: [ Terraform ]
tags: [Terraform]
image: assets/images/terraform.jpg
featured: true
hidden: true
#rating: 4.5
---

# Terraform: taint all resources from one module

If you want to taint all resources from one module, here is a simple way to do it.

```
#!/bin/bash

module=$1

for resource in `terraform show -module-depth=1 | grep module.${module} | tr -d ':' | sed -e 's/module.${module}.//'`; do
  terraform taint -module ${module} ${resource}
done
