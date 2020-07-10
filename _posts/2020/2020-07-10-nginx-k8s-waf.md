---
layout: post
title: 'ModSecurity Web Application Firewall in kubernetes Nginx Ingress controller'
author: juned
type: post
categories: [k8s]
tags: [k8s]
image: assets/images/k8s.jpg
description: "ModSecurity Web Application Firewall in kubernetes Nginx Ingress controller"
featured: true
hidden: true
comments: true
#rating: 4.5
---
# ModSecurity Web Application Firewall in Kubernetes Nginx Ingress controller

The Nginx Ingress controller does support the WAF using the ModSecurity by default. We just have to enable it.

I faced some issues with Nginx 0.26.1 so better to use latest 0.27.1 or latest. (I have tested the setup using 0.32.0)


# Deploy the nginx ingress

```
helm3  install ingress virtual-helm-chart/nginx-ingress -f nginx.values -n datar-james-reanplatform
```

below is the values file I have used

```
COMPUTED VALUES:
controller:
  addHeaders: {}
  admissionWebhooks:
    enabled: false
    failurePolicy: Fail
    patch:
      enabled: true
      image:
        pullPolicy: IfNotPresent
        repository: jettech/kube-webhook-certgen
        tag: v1.0.0
      nodeSelector: {}
      podAnnotations: {}
      priorityClassName: ""
      resources: {}
    port: 8443
    service:
      annotations: {}
      clusterIP: ""
      externalIPs: []
      loadBalancerIP: ""
      loadBalancerSourceRanges: []
      omitClusterIP: false
      servicePort: 443
      type: ClusterIP
  affinity: {}
  autoscaling:
    enabled: false
    maxReplicas: 11
    minReplicas: 1
    targetCPUUtilizationPercentage: 50
    targetMemoryUtilizationPercentage: 50
  config:
    enable-modsecurity: "true"
    enable-owasp-modsecurity-crs: "true"
    modsecurity-snippet: |
      SecRuleEngine On
      SecRequestBodyAccess On
      SecAuditEngine RelevantOnly
      SecAuditLogParts ABIJDEFHZ
      SecAuditLog /var/log/modsec_audit.log
    enable-vts-status: "true"
    hsts-include-subdomains: "false"
    server-name-hash-bucket-size: "256"
    server-tokens: "false"
    ssl-ciphers: ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!aNULL:!eNULL:!EXPORT:!DES:!MD5:!PSK:!RC4
    ssl-protocols: TLSv1.1 TLSv1.2
    use-http2: "true"
  configMapNamespace: ""
  containerPort:
    http: 80
    https: 443
  customTemplate:
    configMapKey: ""
    configMapName: ""
  daemonset:
    hostPorts:
      http: 80
      https: 443
    useHostPort: false
  defaultBackendService: ""
  deploymentAnnotations: {}
  deploymentLabels: {}
  dnsConfig: {}
  dnsPolicy: ClusterFirst
  electionID: ingress-controller-leader
  extraContainers: []
  extraEnvs: []
  extraInitContainers: []
  extraVolumeMounts: []
  extraVolumes: []
  force-namespace-isolation: ""
  hostNetwork: false
  image:
    allowPrivilegeEscalation: true
    pullPolicy: IfNotPresent
    repository: virtual-docker-reanplatform.artifactory.reancloud.com/kubernetes-ingress-controller/nginx-ingress-controller
    runAsUser: 101
    tag : 0.32.0
    # tag: 0.27.1
  ingressClass: nginx
  kind: Deployment
  lifecycle: {}
  livenessProbe:
    failureThreshold: 3
    initialDelaySeconds: 10
    periodSeconds: 10
    port: 10254
    successThreshold: 1
    timeoutSeconds: 1
  maxmindLicenseKey: ""
  metrics:
    enabled: false
    port: 10254
    prometheusRule:
      additionalLabels: {}
      enabled: false
      namespace: ""
      rules: []
    service:
      annotations: {}
      clusterIP: ""
      externalIPs: []
      loadBalancerIP: ""
      loadBalancerSourceRanges: []
      omitClusterIP: false
      servicePort: 9913
      type: ClusterIP
    serviceMonitor:
      additionalLabels: {}
      enabled: false
      namespace: ""
      namespaceSelector: {}
      scrapeInterval: 30s
  minAvailable: 1
  minReadySeconds: 0
  name: controller
  nodeSelector:
    node-role.kubernetes.io/master: ""
  podAnnotations: {}
  podLabels: {}
  podSecurityContext: {}
  priorityClassName: ""
  proxySetHeaders: {}
  publishService:
    enabled: false
    pathOverride: ""
  readinessProbe:
    failureThreshold: 3
    initialDelaySeconds: 10
    periodSeconds: 10
    port: 10254
    successThreshold: 1
    timeoutSeconds: 1
  replicaCount: 1
  reportNodeInternalIp: false
  resources:
    requests:
      cpu: 100m
      memory: 100Mi
  scope:
    enabled: false
    namespace: datar-james-reanplatform
  service:
    annotations: {}
    clusterIP: ""
    enableHttp: true
    enableHttps: true
    enabled: true
    externalIPs: []
    externalTrafficPolicy: Local
    healthCheckNodePort: 0
    internal:
      annotations: {}
      enabled: false
    labels: {}
    loadBalancerIP: ""
    loadBalancerSourceRanges: []
    nodePorts:
      http: 30080
      https: 30443
      # tcp:
      #   "22": 30022
      udp: {}
    omitClusterIP: false
    ports:
      http: 80
      https: 443
    sessionAffinity: ""
    targetPorts:
      http: http
      https: https
    type: NodePort
  tcp:
    configMapNamespace: ""
  terminationGracePeriodSeconds: 60
  tolerations: []
  udp:
    configMapNamespace: ""
  updateStrategy: {}
  useComponentLabel: false
defaultBackend:
  affinity: {}
  apiVersion: apps/v1
  deploymentLabels: {}
  enabled: true
  extraArgs: {}
  extraEnvs: []
  image:
    pullPolicy: IfNotPresent
    repository: virtual-docker-reanplatform.artifactory.reancloud.com/defaultbackend-amd64
    runAsUser: 65534
    tag: 1.5
  livenessProbe:
    failureThreshold: 3
    initialDelaySeconds: 30
    periodSeconds: 10
    successThreshold: 1
    timeoutSeconds: 5
  minAvailable: 1
  name: default-backend
  nodeSelector:
    node-role.kubernetes.io/master: ""
  podAnnotations: {}
  podLabels: {}
  podSecurityContext: {}
  port: 8080
  priorityClassName: ""
  readinessProbe:
    failureThreshold: 6
    initialDelaySeconds: 0
    periodSeconds: 5
    successThreshold: 1
    timeoutSeconds: 5
  replicaCount: 1
  resources: {}
  service:
    annotations: {}
    clusterIP: ""
    externalIPs: []
    loadBalancerIP: ""
    loadBalancerSourceRanges: []
    omitClusterIP: false
    servicePort: 80
    type: ClusterIP
  serviceAccount:
    create: true
  tolerations: []
  useComponentLabel: false
imagePullSecrets:
- name: platform-docker-secret
podSecurityPolicy:
  enabled: true
rbac:
  create: true
  scope: false
releaseLabelOverride: ""
revisionHistoryLimit: 10
serviceAccount:
  annotations: {}
  create: true
# tcp:
#   "22": datar-james-reanplatform/gitlab-gitlab-shell:22
udp: {}

```

# Deploy the test service with ingress

Below is the sample file I used to deploy the application having ingress.

```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: http-svc
spec:
  replicas: 1
  selector:
    matchLabels:
      app: http-svc
  template:
    metadata:
      labels:
        app: http-svc
    spec:
      containers:
      - name: http-svc
        image: gcr.io/kubernetes-e2e-test-images/echoserver:2.1
        ports:
        - containerPort: 8080
        readinessProbe:
          httpGet:
            path: /healthz
            port: 8080
          initialDelaySeconds: 15
          periodSeconds: 5
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

---

apiVersion: v1
kind: Service
metadata:
  name: http-svc
  labels:
    app: http-svc
spec:
  ports:
  - port: 80
    targetPort: 8080
    protocol: TCP
    name: http
  selector:
    app: http-svc

---

apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: http-svc
  annotations:
    kubernetes.io/ingress.class: nginx
    nginx.ingress.kubernetes.io/modsecurity-snippet: |
      SecRuleEngine On
spec:
  rules:
  - host: james.k8s.ijuned.com
    http:
      paths:
      - backend:
          serviceName: http-svc
          servicePort: 8080
        path: /

```

# Test using the curl

Positive i.e. working curl 

```
curl "https://james.k8s.ijuned.com/"


Hostname: http-svc-f4d976d76-c5jzt

Pod Information:
	node name:	ip-10-64-12-208.ec2.internal
	pod name:	http-svc-f4d976d76-c5jzt
	pod namespace:	datar-james-reanplatform
	pod IP:	10.244.0.166

Server values:
	server_version=nginx: 1.12.2 - lua: 10010

Request Information:
	client_address=10.244.0.1
	method=GET
	real path=/
	query=
	request_version=1.1
	request_scheme=http
	request_uri=http://james.k8s.ijuned.com:8080/

Request Headers:
	accept=*/*
	host=james.k8s.ijuned.com
	user-agent=curl/7.64.1
	x-forwarded-for=10.244.0.1
	x-forwarded-host=james.k8s.ijuned.com
	x-forwarded-port=443
	x-forwarded-proto=https
	x-original-forwarded-for=106.193.84.45
	x-real-ip=10.244.0.1
	x-request-id=f058122d88b859e82f7458783d226852
	x-scheme=https

Request Body:
	-no body in request-
```

Blocking i.e. non working curl
```
$ curl "https://james.k8s.ijuned.com/?test=%271%20OR%201=1&x=%3Cscript%3Ealert%28%27hello%27%29;%3C/script%3E"
<html>
<head><title>403 Forbidden</title></head>
<body>
<center><h1>403 Forbidden</h1></center>
<hr><center>nginx</center>
</body>
</html>
```

Logs from the ingress-controller pod 
```
2020/07/10 09:29:13 [error] 3849#3849: *47585 [client 10.244.0.1] ModSecurity: Access denied with code 403 (phase 2). Matched "Operator `Ge' with parameter `5' against variable `TX:ANOMALY_SCORE' (Value: `15' ) [file "/etc/nginx/owasp-modsecurity-crs/rules/REQUEST-949-BLOCKING-EVALUATION.conf"] [line "79"] [id "949110"] [rev ""] [msg "Inbound Anomaly Score Exceeded (Total Score: 15)"] [data ""] [severity "2"] [ver ""] [maturity "0"] [accuracy "0"] [tag "application-multi"] [tag "language-multi"] [tag "platform-multi"] [tag "attack-generic"] [hostname "10.244.0.163"] [uri "/"] [unique_id "159437335364.564617"] [ref ""], client: 10.244.0.1, server: james.k8s.ijuned.com, request: "GET /?test=%271%20OR%201=1&x=%3Cscript%3Ealert%28%27hello%27%29;%3C/script%3E HTTP/1.1", host: "james.k8s.ijuned.com"
10.244.0.1 - - [10/Jul/2020:09:29:13 +0000] "GET /?test=%271%20OR%201=1&x=%3Cscript%3Ealert%28%27hello%27%29;%3C/script%3E HTTP/1.1" 403 146 "-" "curl/7.64.1" 261 0.000 [datar-james-reanplatform-http-svc-8080] [] - - - - 1b21c1f39f81c608a4b74bf587042001
```

# References
[1]: https://kubernetes.github.io/ingress-nginx/user-guide/third-party-addons/modsecurity/
[2]: https://github.com/kubernetes/ingress-nginx/issues/4902
[3]: https://github.com/kubernetes/ingress-nginx/issues/4385