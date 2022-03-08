---
layout: post
title:  "Nginx ReverseProxy Pod in kubernetes"
description: "Nginx ReverseProxy Pod in kubernetes"
author: juned
categories: [ k8s ]
tags: [k8s]
image: assets/images/k8s.jpg
featured: true
hidden: true
---

# Nginx ReverseProxy Pod in kubernetes

## Use Case

If you want to have a simple reverse-proxy for a site which is having basic auth to be added without any authentication.
Lets say `grafana.ijuned.com` is having a basic auth and you want to have a reverse proxy without any authentication.

Create 
1. ConfigMap with Nginx Proxy configurations
2. Nginx Deployment
3. Nginx Service - I am using node port but we can change based on the requirement.
4. To add the Grafana as an IFRAME in another HTML, make sure to edit the grafana.ini file and add 
```
[security]
allow_embedding = true
```

```
---
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-conf
  namespace: loki
data:
  default.conf: |-
    server {
      listen 80 default_server;
      server_name _;
      location / {
              proxy_set_header Host $host;
              proxy_set_header Authorization "Basic YWRtaW46dVpONWV1N2RkN0tQd2FuSTQ0MWJCUGpvdWRKOHc3NEVHcTU3OTdYNg=="; # to generate the token use this - echo -n "admin:admin" | base64 -w 0
              proxy_pass_header Authorization;
              proxy_set_header X-Real-IP $remote_addr;
              proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
              proxy_pass http://grafana.ijuned.com:80/;
              proxy_ssl_verify off;
              proxy_ssl_server_name on;
              proxy_hide_header X-Frame-Options;
              add_header X-Frame-Options "ALLOWALL";
              proxy_set_header X-Forwarded-Proto $scheme;
              proxy_pass_request_headers on;
              proxy_http_version 1.1;
              proxy_set_header Upgrade $http_upgrade;
      }
      
    }
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-proxy
  namespace: loki
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana-proxy
  template:
    metadata:
      labels:
        app: grafana-proxy
    spec:
      volumes:
      - name: nginx-conf
        configMap:
          name: nginx-conf
          items:
            - key: default.conf
              path: default.conf
      containers:
        - name: grafana-proxy
          image: docker.io/library/nginx:1.21.6
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 80
          env:
            - name: NODE_NAME
              valueFrom:
                fieldRef:
                  fieldPath: spec.nodeName
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
            - name: POD_NAMESPACE
              valueFrom:
                fieldRef:
                  fieldPath: metadata.namespace
            - name: POD_IP
              valueFrom:
                fieldRef:
                  fieldPath: status.podIP
          volumeMounts:
            - name: nginx-conf
              mountPath: /etc/nginx/conf.d/default.conf 
              subPath: default.conf      

---
apiVersion: v1
kind: Service
metadata:
  labels:
    app: grafana-proxy
  name: grafana-proxy
  namespace: loki
spec:
  ipFamilies:
  - IPv4
  ipFamilyPolicy: SingleStack
  ports:
  - name: http
    port: 80
  selector:
    app: grafana-proxy
  type: ClusterIP


```