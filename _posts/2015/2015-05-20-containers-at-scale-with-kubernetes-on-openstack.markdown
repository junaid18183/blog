---
layout: post
title: Containers at Scale with Kubernetes on OpenStack
date: 2015-05-20 11:24:42.000000000 +05:30
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
  post_id: '808'
  blog_id: '79908823'
  reblog_snapshot: "O:8:\"stdClass\":8:{s:5:\"title\";s:48:\"Containers at Scale with
    Kubernetes on OpenStack\";s:4:\"type\";s:4:\"post\";s:9:\"mime_type\";s:0:\"\";s:6:\"format\";b:0;s:12:\"modified_gmt\";s:19:\"2015-05-11
    11:44:27\";s:9:\"permalink\";s:82:\"http://keithtenzer.com/2015/04/15/containers-at-scale-with-kubernetes-on-openstack\";s:7:\"content\";s:22510:\"<div
    class=\"reblogged-content\">\n\n<h3>Overview</h3>\r\nContainers are a burning
    hot topic right now. Several open source technologies have come together to allow
    containers to be operated at scale and in the enterprise. In this article I will
    talk about these technologies and explain how to build container infrastructure
    at scale with OpenStack. There are three main components that come together to
    create container-based infrastructure: Red Hat Enterprise Linux Atomic Host (RHEL
    Atomic), Docker and Google's Kubernetes. RHEL Atomic provides an optimized operating
    system for running containers. Docker deliversÂ container portability and a packaging
    standard. Kubernetes adds orchestration and management of Docker containers across
    a massively scalable cluster of RHEL Atomic hosts.\r\n\r\n<a href=\"https://junaid18183.files.wordpress.com/2015/05/red_hat_container_architecture.png\"><img
    class=\"  wp-image-816 aligncenter\" src=\"https://junaid18183.files.wordpress.com/2015/05/red_hat_container_architecture.png\"
    alt=\"red_hat_container_architecture\" width=\"1270\" height=\"639\" data-originalSrc=\"https://keithtenzer.files.wordpress.com/2015/04/red_hat_container_architecture.png?w=300\"
    data-rehosted=\"1\"></a>\r\n<!--more-->\r\n<h3>RHEL Atomic</h3>\r\n<a href=\"http://www.projectatomic.io/\">RHEL
    Atomic</a> is an optimized container operating system based on Red Hat Enterprise
    Linux 7 (RHEL 7). The name atomic refers to how updates are managed. RHEL Atomic
    does not use yum but rather OSTree for managing updates. Software updates are
    handled atomically across the entire system. Not only this but youÂ can rollbackÂ to
    the systems previous state if the new upgraded state is for some reason not desired.
    The intention is to reduce risk during upgrades and make the entire process seamless.Â When
    we consider the density of containers vs virtual machines to be around 10X, upgrades
    and maintenance becomeÂ that much more critical.\r\n\r\nRHEL Atomic provides both
    Docker and Kubernetes. Underneath the hood it leverages SELinux (security), Cgroups
    (process isolation) and Namespaces (network isolation). It is an Operating System
    that is optimized to run containers. In addition RHEL Atomic provides enterprise
    features such asÂ security, isolation, performance and management to the containerized
    world.\r\n<h3>Docker</h3>\r\n<a href=\"https://www.docker.com/\">Docker</a> is
    often a misused term when referring to containers. Docker is not a container,
    instead itÂ is a platform for running containers. Docker provides a packaging
    format, tool-set and all the plumbing needed for running containers withinÂ a
    single host. Docker also provides a hub for sharing Docker images.\r\n\r\nDocker
    images consist of a Base-OS and various layers that allow one to build an application
    stack (application and its dependencies). Docker images are immutable, you don't
    update them. Instead you create a new image by adding or making changes to the
    various layers. This is the future of application deployment and is not only more
    efficient but magnitudes faster than the traditional approach with virtual machines.\r\n\r\nRed
    Hat is providing a docker repository for certified, tested, secure and supportedÂ Docker
    images similar to how RPMs are currently provided.\r\n\r\nAll Docker images run
    in a container and all the containers share the same Linux kernel, RHEL Atomic.\r\n<h3>Kubernetes</h3>\r\n<a
    href=\"http://kubernetes.io/\">Kubernetes</a> is an orchestration engine built
    around Docker. It allows administrators to manage Docker containers at scale across
    many physical or virtual hosts. Kubernetes has three main components: master,
    node or minion and pod.\r\n<h4>Master</h4>\r\nThe Kubernetes master is the control
    plane and provides several services. The scheduler handles placement of pods.
    It also provides a replication controller that ensures pods are replicated according
    to policy. The master also maintains the state of the cluster and relies on ETCD
    which is a distributed key/value store for those capabilities. Finally Restful
    APIs for performing operations on nodes, pods, replication controllers and services
    are provided by the Kubernetes master.\r\n<h4>Â Node</h4>\r\nThe Kubernetes node
    or minion as it is often referred to runs pods. Placement of pod on a Kubernetes
    node is as mentioned determined by the scheduler on the Kubernetes master. The
    Kubernetes node runs several important services: kubelet and kube-proxy. The kubelet
    is responsible for node level pod management. In addition Kubernetes allows for
    the creation of services that expose applications to the outside world. The kube-proxy
    is responsible for managing Kubernetes services within a node. Since pods are
    meant to be mortal, the idea behind services is providing an abstraction that
    lives independently of a pod.\r\n<h4>Pod</h4>\r\nThe Kubernetes pod is one or
    more tightly coupled containers that are scheduled onto the same host. Containers
    within pods share some resources such as storage and networking. A pod provides
    a single unit of horizontal scaling and replication across the Kubernetes cluster.\r\n\r\nNow
    that we have a good feel for the components involved it is time to sink our teeth
    into Kubernetes. First I would like to recognize two colleaguesÂ <a href=\"https://github.com/shetze/RHEL-Atomic-Demo-Kit\">Sebastian
    Hetze</a> and <a href=\"https://github.com/scollier/SATraining\">Scott Collier</a>.
    I have usedÂ their initial work around Kubernetes configurations in this article
    as my basis.\r\n<h3>Configure Kubernetes NodesÂ in OpenStack</h3>\r\nKubernetes
    nodes or minions can be deployed and configured automatically on OpenStack. If
    more compute power is required for our container infrastructure we simply need
    to deploy additional Kubernetes nodes. OpenStack is the perfect infrastructure
    for running containers at scale. Below are the steps required to deploy Kubernetes
    nodes on OpenStack.\r\n<ul>\n<li>Download the <a href=\"https://access.redhat.com/downloads/content/271/ver=/rhel---7/7.1.0/x86_64/product-downloads\">RHEL
    Atomic</a> cloud image (QCOW2)</li>\r\n\t<li>Add RHEL Atomic Cloud Image to Glance
    in OpenStack</li>\r\n\t<li>Create atomic security group</li>\r\n</ul>\n<pre style=\"padding-left:30px;\">#neutron
    security-group-create atomic --description \"RHEL Atomic security group\"</pre>\r\n<pre
    style=\"padding-left:30px;\">#neutron security-group-rule-create atomic --protocol
    tcp --port-range-min 10250 --port-range-max 10250 --direction ingress --remote-ip-prefix
    0.0.0.0/0</pre>\r\n<pre style=\"padding-left:30px;\">#neutron security-group-rule-create
    atomic --protocol tcp --port-range-min 4001 --port-range-max 4001 --direction
    egress --remote-ip-prefix 0.0.0.0/0</pre>\r\n<pre style=\"padding-left:30px;\">#neutron
    security-group-rule-create atomic --protocol tcp --port-range-min 5000 --port-range-max
    5000 --direction egress --remote-ip-prefix 0.0.0.0/0</pre>\r\n<pre style=\"padding-left:30px;\">#neutron
    security-group-rule-create --protocol icmp --direction ingress default</pre>\r\n<ul>\n<li>Create
    user-data to automate deployment using cloud-init</li>\r\n</ul>\n<pre style=\"padding-left:30px;\">#cloud-config\r\nhostname:
    atomic01.lab.com\r\npassword: redhat\r\nssh_pwauth: True\r\nchpasswd: { expire:
    False }\r\n\r\nssh_authorized_keys:\r\n- ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCfxcho9SipUCokS29C+AJNNLcrfpT4xsu9aErax3XSNThWbiJehUDufe86ZO4lqib4dekDEL6d7vBa3WlalzJaq/p/sy1xjYdRNE0vHQCxuWgG+NaL8KcxXDhrUa0UHMW8k8hw9xzOGaRx35LRP9+B0fq/W572XPWwEPRJo8WtSKFiqJZEBkai1IcF0CErj30d0/va9c3EYqkCEWbxuIRL+qoysH+MgFbs1jjjrvfJCLiZZo95MWp4nDrmxYNlmwMIvYrsRZfygeyYPiqVzO51gmGxcVRTbqgG0fSRVRHjUE3E4VfW9wm1qn8+rEc0iQB6ER0f6U/wtEAUmvd/g4Ef
    ktenzer@ktenzer.muc.csb\r\n\r\nwrite_files:\r\n- content: |\r\n127.0.0.1 localhost
    localhost.localdomain localhost4 localhost4.localdomain4\r\n::1 localhost localhost.localdomain
    localhost6 localhost6.localdomain6\r\n\r\n192.168.2.15 atomic01.lab.com atomic01\r\n192.168.2.16
    atomic02.lab.com atomic02\r\n192.168.2.17 atomic03.lab.com atomic03\r\n192.168.2.14
    kubernetes.lab.com kubernetes\r\npath: /etc/hosts\r\npermissions: '0644'\r\nowner:
    root:root\r\n- content: |\r\n###\r\n# kubernetes system config\r\n#\r\n# The following
    values are used to configure various aspects of all\r\n# kubernetes services,
    including\r\n#\r\n# kube-apiserver.service\r\n# kube-controller-manager.service\r\n#
    kube-scheduler.service\r\n# kubelet.service\r\n# kube-proxy.service\r\n\r\n# Comma
    seperated list of nodes in the etcd cluster\r\nKUBE_ETCD_SERVERS=\"--etcd_servers=http://kubernetes.lab.com:4001\"\r\n\r\n#
    logging to stderr means we get it in the systemd journal\r\nKUBE_LOGTOSTDERR=\"--logtostderr=true\"\r\n\r\n#
    journal message level, 0 is debug\r\nKUBE_LOG_LEVEL=\"--v=0\"\r\n\r\n# Should
    this cluster be allowed to run privleged docker containers\r\nKUBE_ALLOW_PRIV=\"--allow_privileged=false\"\r\npath:
    /etc/kubernetes/config\r\npermissions: '0644'\r\nowner: root:root\r\n- content:
    |\r\n###\r\n# kubernetes kubelet (minion) config\r\n\r\n# The address for the
    info server to serve on (set to 0.0.0.0 or \"\" for all interfaces)\r\nKUBELET_ADDRESS=\"--address=0.0.0.0\"\r\n\r\n#
    The port for the info server to serve on\r\nKUBELET_PORT=\"--port=10250\"\r\n\r\n#
    You may leave this blank to use the actual hostname\r\nKUBELET_HOSTNAME=\"\"\r\n\r\n#
    Add your own!\r\nKUBELET_ARGS=--cluster_domain=kubernetes.local --cluster_dns=10.254.0.10\r\npath:
    /etc/kubernetes/kubelet\r\npermissions: '0644'\r\nowner: root:root\r\n- content:
    |\r\n# /etc/sysconfig/docker\r\nOPTIONS='--selinux-enabled'\r\nDOCKER_CERT_PATH=/etc/docker\r\nADD_REGISTRY='--add-registry
    registry.access.redhat.com'\r\nADD_REGISTRY='--add-registry kubernetes.lab.com:5000'\r\n#
    BLOCK_REGISTRY='--block-registry '\r\n# INSECURE_REGISTRY='--insecure-registry'\r\n#
    DOCKER_TMPDIR=/var/tmp\r\n# LOGROTATE=false\r\npath: /etc/sysconfig/docker\r\npermissions:
    '0644'\r\nowner: root:root\r\n- content: |\r\n# Flanneld configuration options\r\n\r\n#
    etcd url location. Point this to the server where etcd runs\r\nFLANNEL_ETCD=\"http://kubernetes.lab.com:4001\"\r\n\r\n#
    etcd config key. This is the configuration key that flannel queries\r\n# For address
    range assignment\r\nFLANNEL_ETCD_KEY=\"/flannel/network\"\r\n\r\n# Any additional
    options that you want to pass\r\nFLANNEL_OPTIONS=\"eth0\"\r\npath: /etc/sysconfig/flanneld\r\npermissions:
    '0644'\r\nowner: root:root\r\n- content: |\r\n{}\r\npath: /var/lib/kubelet/auth\r\npermissions:
    '0644'\r\nowner: root:root\r\n\r\nbootcmd:\r\n- systemctl enable kube-proxy\r\n-
    systemctl enable kubelet\r\n- systemctl enable flanneld\r\n\r\nruncmd:\r\n- hostname
    -f &gt;/etc/hostname\r\n- hostname -i &gt;&gt;/etc/issue\r\n- echo '' &gt;&gt;/etc/issue\r\n\r\nfinal_message:
    \"Cloud-init completed and the system is up, after $UPTIME seconds\"</pre>\r\n<ul>\n<li>Boot
    RHEL Atomic instances using the 'nova boot' CLI command</li>\r\n</ul>\n<pre style=\"padding-left:30px;\">#nova
    boot --flavor m1.small --poll --image Atomic_7_1 --key-name atomic-key --security-groups
    prod-base,atomic --user_data user-data-openstack --nic net-id=e3f370ab-b6ac-4788-a739-7f8de8631518
    Atomic1</pre>\r\n<ul>\n<li>Associate floating-ip to the RHEL Atomic instance</li>\r\n</ul>\n<pre
    style=\"padding-left:30px;\">#nova floating-ip-associate Atomic1 192.168.2.15</pre>\r\nOf
    course you will want to update the cloud-init user-data as well as the CLI commands
    according to your environment. In this example I did not have DNS so I updated
    the /etc/hosts file directly but this step is not required. I also did not attach
    a Red Hat subscription something you would probably want to do using the 'runcmd'
    option in cloud-init.\r\n<h3>Configure Kubernetes Master</h3>\r\nOnce Kubernetes
    nodes have been deployed we can configure the Kubernetes master. The Kubernetes
    master runs Kubernetes, Docker and ETCD services. In addition an overlay network
    is required. There are many options to create an overlay network, in this case
    we have chosen to use flannel to provide thoseÂ capabilities. Finally for the
    base OS, a minimum install of a current RHEL-7 release is required.\r\n<ul>\n<li>Register
    host with subscription-manager</li>\r\n</ul>\n<pre style=\"padding-left:30px;\">#subscription-manager
    register attach --pool=&lt;pool id&gt;\r\n#subscription-manager repos --disable=*\r\n#subscription-manager
    repos --enable=rhel-7-server-rpms\r\n#subscription-manager repos --enable=rhel-7-server-extras-rpms\r\n#subscription-manager
    repos --enable=rhel-7-server-optional-rpms\r\n#yum -y update</pre>\r\n<ul>\n<li>Install
    required packages</li>\r\n</ul>\n<pre style=\"padding-left:30px;\">#yum -y install
    docker docker-registry kubernetes flannel</pre>\r\n<ul>\n<li>Disable firewall</li>\r\n</ul>\n<pre
    style=\"padding-left:30px;\">#systemctl stop firewalld\r\n#systemctl disable firewalld</pre>\r\n<ul>\n<li>Enable
    required services</li>\r\n</ul>\n<pre style=\"padding-left:30px;\">#for SERVICES
    in docker.service docker-registry etcd kube-apiserver kube-controller-manager
    kube-scheduler flanneld; do\r\n systemctl enable $SERVICES\r\ndone</pre>\r\n<ul>\n<li>Configure
    Docker</li>\r\n</ul>\n<pre style=\"padding-left:30px;\">#vi /etc/sysconfig/docker\r\nINSECURE_REGISTRY='--insecure-registry
    kubernetes.lab.com:5000'</pre>\r\n<ul>\n<li>Â Configure Kubernetes</li>\r\n</ul>\n<pre
    style=\"padding-left:30px;\">#vi /etc/kubernetes/apiserver and set\r\nKUBE_API_ADDRESS=\"--address=0.0.0.0\"\r\nKUBE_MASTER=\"--master=http://kubernetes.lab.com:8080\"</pre>\r\n<pre
    style=\"padding-left:30px;\">#vi /etc/kubernetes/config and set\r\nKUBE_ETCD_SERVERS=\"--etcd_servers=http://kubernetes.lab.com:4001\"</pre>\r\n<pre
    style=\"padding-left:30px;\">#vi /etc/kubernets/controller-manager and set\r\nKUBELET_ADDRESSES=\"--machines=atomic01.lab.com,atomic02.lab.com,atomic03.lab.com\"</pre>\r\n<ul>\n<li>Configure
    Flannel</li>\r\n</ul>\n<pre style=\"padding-left:30px;\">#vi /etc/sysconfig/flanneld
    and set\r\nFLANNEL_ETCD=\"http://kubernetes.lab.com:4001\"\r\nFLANNEL_ETCD_KEY=\"/flannel/network\"\r\nFLANNEL_OPTIONS=\"eth0\"</pre>\r\n<ul>\n<li>Start
    ETCD</li>\r\n</ul>\n<pre style=\"padding-left:30px;\">#systemctl start etcd</pre>\r\n<ul>\n<li>Configure
    Flannel overlay network</li>\r\n</ul>\n<pre style=\"padding-left:30px;\">#vi /root/flannel-config.json\r\n{\r\n
    \"Network\": \"10.100.0.0/16\",\r\n \"SubnetLen\": 24,\r\n \"SubnetMin\": \"10.100.50.0\",\r\n
    \"SubnetMax\": \"10.100.199.0\",\r\n \"Backend\": {\r\n \"Type\": \"vxlan\",\r\n
    \"VNI\": 1\r\n }\r\n}</pre>\r\n<pre style=\"padding-left:30px;\">curl -L http://kubernetes.lab.com:4001/v2/keys/flannel/network/config
    -XPUT --data-urlencode value@/root/flannel-config.json</pre>\r\n<ul>\n<li>Load
    Docker Images</li>\r\n</ul>\n<pre style=\"padding-left:30px;\">#systemctl start
    docker\r\n#systemctl start docker-registry\r\n#for IMAGES in rhel6 rhel7 fedora/apache;
    do\r\n docker pull $IMAGES\r\n docker tag $IMAGES kubernetes.lab.com:5000/$IMAGES\r\n
    docker push kubernetes.lab.com:5000/$IMAGES\r\ndone</pre>\r\n<ul>\n<li>Reboot
    host</li>\r\n</ul>\n<pre style=\"padding-left:30px;\">systemctl reboot</pre>\r\n<h3>Container
    Administration using Kubernetes</h3>\r\nKubernetes provides a CLI and a Restful
    API for management. Currently there is no GUI. In a future article I will go into
    detail about using the API in order to build your own UI or integrate Kubernetes
    in existing dashboards.Â For the purpose of this article we will focus on kubectl,
    the Kubernetes CLI.\r\n<h4>Deploy an Application</h4>\r\nIn this example we will
    deploy an Apache web server pod. Before deploying a pod we must ensure that Kubernetes
    nodes (minions) are ready.\r\n<pre style=\"padding-left:30px;\">[root@kubernete
    ~]# kubectl get minions\r\nNAME             LABELS STATUS\r\natomic01.lab.com
    &lt;none&gt; Ready\r\natomic02.lab.com &lt;none&gt; Ready\r\natomic03.lab.com
    &lt;none&gt; Ready</pre>\r\nNext we need to create a JSON file for deploying a
    pod. The kubectl command uses JSON as input to make configuration updates and
    changes.\r\n<pre style=\"padding-left:30px;\">[root@kube-master ~]# vi apache-pod.json</pre>\r\n\r\n[code
    language=\"java\"]\r\n{\r\n \"apiVersion\": \"v1beta1\",\r\n \"desiredState\":
    {\r\n    \"manifest\": {\r\n       \"containers\": [\r\n       {\r\n          \"image\":
    \"fedora/apache\",\r\n          \"name\": \"my-fedora-apache\",\r\n          \"ports\":
    [\r\n          {\r\n             \"containerPort\": 80,\r\n             \"hostPort\":80,\r\n
    \            \"protocol\": \"TCP\"\r\n          }\r\n       ]\r\n    }\r\n    ],\r\n
    \      \"id\": \"apache\",\r\n       \"restartPolicy\": {\r\n       \"always\":
    {}\r\n    },\r\n       \"version\": \"v1beta1\",\r\n       \"volumes\": null\r\n
    \   }\r\n },\r\n \"id\": \"apache\",\r\n \"kind\": \"Pod\",\r\n \"labels\": {\r\n
    \   \"name\": \"apache\"\r\n },\r\n \"namespace\": \"default\"\r\n}\r\n\r\n[/code]\r\n\r\n \r\n<pre
    style=\"padding-left:30px;\">[root@kube-master ~]# kubectl create -f apache-pod.json</pre>\r\nWe
    can now get the status of our newly created Apache pod.\r\n<pre style=\"padding-left:30px;\">[root@kubernetes
    ~]# kubectl get pods\r\nPOD    IP           CONTAINER(S)     IMAGE(S)      HOST
    \             LABELS      STATUS\r\napache 10.100.119.6 my-fedora-apache fedora/apache
    atomic02.lab.com/ name=apache Running</pre>\r\nNotice that the pod is running
    on atomic02.lab.com. The Kubernetes scheduler takes care of scheduling the pod
    on a node.\r\n<h4>Â Create Services</h4>\r\nIn Kubernetes services are used to
    provide external access to an application running in a pod. The idea is that since
    pods are mortal and transient in nature a service should provide abstraction so
    applications do not need to understand underlying pod or containers infrastructure.
    Services use the kube-proxy to accessÂ applications from any Kubernetes node configured
    as public IPs in the service itself. In the example below we are creating a service
    that will be available from allÂ three of the Kubernetes nodes atomic01.lab.com,
    atomic02.lab.com and atomic03.lab.com. The pod is running on atomic02.lab.com.
    Similar to pods, services alsoÂ requirec a JSON file as input to kubectl.\r\n<pre
    style=\"padding-left:30px;\">[root@kubernetes ~]# vi apache-service.json</pre>\r\n\r\n[code
    language=\"java\"]\r\n\r\n{\r\nÂ  Â \"apiVersion\": \"v1beta1\",\r\nÂ  Â \"containerPort\":
    80,\r\nÂ  Â \"id\": \"frontend\",\r\nÂ  Â \"kind\": \"Service\",\r\nÂ  Â \"labels\":
    {\r\nÂ  Â  Â  \"name\": \"frontend\"\r\nÂ  Â },\r\nÂ  Â \"port\": 80,\r\nÂ  Â \"publicIPs\":
    [\r\nÂ  Â \"192.168.2.15\",\"192.168.2.16\",\"192.168.2.17\"\r\nÂ  Â ],\r\nÂ 
    Â \"selector\": {\r\nÂ  Â  Â  \"name\": \"apache\"\r\nÂ  Â }\r\n}\r\n\r\n[/code]\r\n\r\n<pre
    style=\"padding-left:30px;\">[root@kube-master ~]# kubectl create -f apache-service.json</pre>\r\nWe
    can now get the status of our newly created apache-frontend service.\r\n<pre style=\"padding-left:30px;\">[root@kubernetes
    ~]# kubectl get services\r\nNAME            LABELS               SELECTOR    IP
    \           PORT\r\napache-frontend name=apache-frontend name=apache 10.254.94.252
    80</pre>\r\nAs one would expect, we can access our Apache pod externally through
    any of our three Kubernetes nodes.\r\n<pre style=\"padding-left:30px;\">[root@kubernetes
    ~]# curl http://atomic01.bigred.com\r\nApache</pre>\r\n<h4>Creating Replication
    Controllers</h4>\r\nSo far we have seen how toÂ create a pod containing one or
    more containers and build a service to expose the application externally. If we
    want to scale our application horizontally however we need to create a replication
    controller. In Kubernetes replication controllers are pods that have a replication
    policy. Kubernetes will create multiple pods across the cluster and a pod is our
    base unit of scaling. In the example below we will create a replication controller
    for our Apache web server that will ensure three replicas. The same service we
    already created can be used but this time an Apache pod will be running on each
    Kubernetes node. In our previous example we only had one Apache web server on
    atomic02.lab.com and though we could access it through any node it was done through
    the kube-proxy.\r\n<pre style=\"padding-left:30px;\">[root@kubernetes ~]# vi apache-replication-controller.json</pre>\r\n\r\n[code
    language=\"java\"]\r\n\r\n{\r\n   \"apiVersion\": \"v1beta1\",\r\n   \"desiredState\":
    {\r\n      \"podTemplate\": {\r\n         \"desiredState\": {\r\n            \"manifest\":
    {\r\n            \"containers\": [\r\n            {\r\n               \"image\":
    \"fedora/apache\",\r\n               \"name\": \"my-fedora-apache\",\r\n               \"ports\":
    [\r\n               {\r\n                  \"containerPort\": 80,\r\n                  \"hostPort\":
    80,\r\n                  \"protocol\": \"TCP\"\r\n               }\r\n               ]\r\n
    \           }\r\n            ],\r\n            \"id\": \"apache\",\r\n            \"restartPolicy\":
    {\r\n               \"always\": {}\r\n            },\r\n            \"version\":
    \"v1beta1\",\r\n            \"volumes\": null\r\n            }\r\n         },\r\n
    \        \"labels\": {\r\n            \"name\": \"apache\"\r\n         }\r\n      },\r\n
    \     \"replicaSelector\": {\r\n         \"name\": \"apache\"\r\n   },\r\n   \"replicas\":
    3\r\n   },\r\n   \"id\": \"apache-controller\",\r\n   \"kind\": \"ReplicationController\",\r\n
    \  \"labels\": {\r\n   \"name\": \"apache\"\r\n   }\r\n}\r\n\r\n[/code]\r\n\r\n<pre
    style=\"padding-left:30px;\">[root@kube-master ~]# kubectl create -f apache-replication-controller.json</pre>\r\nWe
    can now get the status of our newly created Apache replication controller.\r\n<pre
    style=\"padding-left:30px;\">[root@kubernetes ~]# kubectl get replicationcontrollers\r\nCONTROLLER
    \       CONTAINER(S)     IMAGE(S)      SELECTOR    REPLICAS\r\napache-controller
    my-fedora-apache fedora/apache name=apache 3</pre>\r\nWe can also see that the
    replication controller created three pods as expected.\r\n<pre style=\"padding-left:30px;\">[root@kubernetes
    ~]# kubectl get pods\r\nPOD                                  IP           CONTAINER(S)
    \    IMAGE(S)      HOST                 LABELS      STATUS\r\nfb9936f3-e21d-11e4-ad6e-000c295b1de9
    10.100.119.6 my-fedora-apache fedora/apache atomic03.bigred.com/ name=apache Running\r\nfb9acf1a-e21d-11e4-ad6e-000c295b1de9
    10.100.65.6  my-fedora-apache fedora/apache atomic02.bigred.com/ name=apache Running\r\nfb97a111-e21d-11e4-ad6e-000c295b1de9
    10.100.147.6 my-fedora-apache fedora/apache atomic01.bigred.com/ name=apache Running</pre>\r\n<h3>Summary</h3>\r\nIn
    this article we discussed the different components required to run application
    containers at scale: RHEL Atomic, Docker and Kubernetes. We also saw how to deploy
    Kubernetes RHEL Atomic nodes on OpenStack. Having scalable application containers
    means little if your infrastructure underneath cannot scale and that is why OpenStack
    should be key to any enterprise container strategy. Finally we went into a lot
    of detail on how to configure Kubernetes pods, services and replication controllers.
    Running application containers at scale in the enterprise is a lot more than just
    Docker. It has only been until very recently that these best-of-breed open source
    technologies have come together and allowed such wonderful possibilities. This
    is a very exciting time, containers will change everything about how we deploy,
    run and manage our applications. Hopefully you found this article interesting
    and useful. If you have any feedback I would really like to hear it, please share.\r\n\r\nHappy
    Containerizing!\r\n\r\n(c) 2015 Keith Tenzer</div>\";s:15:\"images_mirrored\";i:1;}"
---

