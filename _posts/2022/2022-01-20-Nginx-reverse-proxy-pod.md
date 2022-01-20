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

```
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-conf
data:
  proxy.conf: |-
    server {
      listen 80 default_server;
      server_name _;
      location / {
                    proxy_set_header Host $host;
                    proxy_set_header Authorization "Basic YWRtaW46cHJvbS1vcGVyYXRvcg=="; # to generate the token use this - echo -n "admin:admin" | base64 -w 0
                    proxy_set_header X-Real-IP $remote_addr;
                    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                    proxy_pass https://grafana.ijuned.com;
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
            - key: proxy.conf
              path: proxy.conf
      containers:
        - name: grafana-proxy
          image: docker.io/library/nginx:latest
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
              mountPath: /etc/nginx/conf.d/proxy.conf 
              subPath: proxy.conf      

---
apiVersion: v1
kind: Service
metadata:
  labels:
    app: grafana-proxy
  name: grafana-proxy
  namespace: default
spec:
  ipFamilies:
  - IPv4
  ipFamilyPolicy: SingleStack
  ports:
  - name: http
    nodePort: 31973
    port: 80
  selector:
    app: grafana-proxy
  type: NodePort

```