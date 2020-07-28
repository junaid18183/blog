---
layout: post
title:  "How to delete the dangling namespace in kubernetes"
description: "How to delete the dangling namespace in kubernetes"
author: juned
categories: [ k8s ]
tags: [k8s]
image: assets/images/k8s.jpg
featured: true
hidden: true
#rating: 4.5
---

### How to delete the dangling namespace in kubernetes

If you have got a dangling namespace which in `Terminating` state forever like below

```
NAME                STATUS        AGE
test-solutions   Terminating   7d1h
```

You can get rid of them using simple hack below, Reference [1]


```
(
NAMESPACE=your-rogue-namespace
kubectl proxy &
kubectl get namespace $NAMESPACE -o json |jq '.spec = {"finalizers":[]}' >temp.json
curl -k -H "Content-Type: application/json" -X PUT --data-binary @temp.json 127.0.0.1:8001/api/v1/namespaces/$NAMESPACE/finalize
)
```
[1]: https://stackoverflow.com/questions/52369247/namespace-stuck-as-terminating-how-do-i-remove-it/53661717#53661717
