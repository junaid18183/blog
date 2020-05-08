---
layout: post
title: OpenStack and Docker
date: 2015-01-06 13:01:29.000000000 +05:30
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
  post_id: '522'
  blog_id: '40736101'
  reblog_snapshot: "O:8:\"stdClass\":7:{s:5:\"title\";s:20:\"OpenStack and Docker\";s:4:\"type\";s:4:\"post\";s:9:\"mime_type\";s:0:\"\";s:6:\"format\";b:0;s:12:\"modified_gmt\";s:19:\"2014-03-08
    02:27:40\";s:9:\"permalink\";s:66:\"http://tropicaldevel.wordpress.com/2014/03/07/openstack-and-docker\";s:7:\"content\";s:6772:\"<div
    class=\"reblogged-content\">\n\n<h2>Introduction</h2>\r\nI recently tried to set
    up OpenStack with docker as the hypervisor on a single node and I ran into mountains
    of trouble.  I tried with DevStack and entirely failed using both the master branch
    and stable/havana.  After much work I was able to launch container but the network
    was not right.  Ultimately I found a path that worked.  This post explains how
    I did this.\r\n<h2>Create the base image</h2>\r\n<h3>CentOS 6.5</h3>\r\nThe first
    step is to have a VM that can support this.  Because I was using RDO this needed
    to be a Red Hat derivative.  I originally chose a stock vagrant CentOS 6.5 VM.
     I got everything set up and then ran out of disk space (many bad words were said).
     Thus I used <a title=\"Packer IO\" href=\"http://www.packer.io/\">packer</a>
    and the templates <a title=\"Packer CentOS 6.5 template\" href=\"https://github.com/osuosl/packer-templates/tree/master/vagrant/centos-6-x86_64\">here</a>
    to create a CentOS VM with 40GB of disk space.  I had to change the <em>\"disk_size\"</em>
    value under <em>\"builders\"</em> to something larger than 40000. Then I ran the
    build.\r\n<pre>packer build template.json</pre>\r\nWhen this completed I had a
    centos-6.5 vagrant box ready to boot.\r\n<h3>Vagrant</h3>\r\nI wanted to manage
    this VM with Vagrant and because OpenStack is fairly intolerant to HOST_IP changes
    I had to inject in an interface with a static IP address.  Below is the Vagrant
    file I used:\r\n<pre>Vagrant.configure(\"2\") do |config|\r\n   config.vm.box
    = \"centos-6.5-base\"\r\n   config.vm.network :private_network, ip: \"172.16.129.26\"\r\n
    \  ES_OS_MEM = 3072\r\n   ES_OS_CPUS = 1\r\n   config.vm.hostname = \"rdodocker\"\r\n
    \ config.vm.provider :virtualbox do |vb|\r\n    vb.customize [\"modifyvm\", :id,
    \"--memory\", ES_OS_MEM]\r\n    vb.customize [\"modifyvm\", :id, \"--cpus\", ES_OS_CPUS]\r\n
    \ end\r\nend</pre>\r\n<span style=\"line-height:1.5em;\">After running<em> vagrant
    up</em> to boot this VM I got the following error:</span>\r\n<pre>The following
    SSH command responded with a non-zero exit status.\r\nVagrant assumes that this
    means the command failed!\r\n/sbin/ifdown eth1 2&gt; /dev/null\r\nStdout from
    the command:\r\n\r\nStderr from the command:</pre>\r\nThankfully this was easily
    solved.  I sshed into the VM with <em>vagrant ssh,</em> and then ran the following:\r\n<pre><code>cat
    &lt;&lt;EOM | sudo tee /etc/sysconfig/network-scripts/ifcfg-eth1 &gt;/dev/null\r\nDEVICE=\"eth1\"\r\nONBOOT=\"yes\"\r\nTYPE=\"Ethernet\"\r\nEOM</code></pre>\r\nAfter
    that I exited from the ssh session and repackaged the VM with <em>vagrant package
    --output centos-6.5-goodnet.box.</em> I added the new box to vagrant and altered
    my Vagrant file to boot it.  I now had a base image on which I could install OpenStack.\r\n<h2>RDO</h2>\r\nThrough
    much trial and error I came to the conclusion that I needed the <a href=\"http://openstack.redhat.com/QuickStartDevelRelease\">icehouse
    development release</a> of <a href=\"http://openstack.redhat.com/\">RDO</a>.  Unfortunately
    this alone was not enough to properly handle docker.  I also had to install nova
    from the master branch into a python virtualenv and reconfigure the box to use
    that nova code.  This section has the specifics of what I did.\r\n<h3>RDO Install</h3>\r\nI
    followed the instructions for installing RDO that are <a href=\"http://openstack.redhat.com/QuickStartDevelRelease\">here</a>,
    only instead of running <em>packstack --allinone</em> I used a custom answer file.
     I generated a template answer file with the command packstack --gen-answer-file=~/answers.txt.
     Then I opened that file and I substituted out ever IP address with the IP address
    that vagrant was injecting into my VM (in my case this was 172.16.129.26).  I
    also set the following:\r\n<pre>CONFIG_NEUTRON_INSTALL=n</pre>\r\nThis is very
    important.  The <a href=\"https://bugs.launchpad.net/openstack-manuals/+bug/1243319\">docker
    driver does not work with neutron</a>.  (I learned this the hard way).  I then
    installed RDO with the command <em>packstack --answerfile answers.txt</em>.\r\n<h2>Docker</h2>\r\nOnce
    RDO was installed and working (without docker) I set up the VM such that nova
    would use docker.  The instructions <a href=\"https://wiki.openstack.org/wiki/Docker\">here</a>
    are basically what I followed.  Here is my command set:\r\n<pre>sudo yum -y install
    docker-io\r\nsudo service docker start\r\nsudo chkconfig docker on\r\nsudo yum
    -y install docker-registry\r\nsudo usermod -G docker nova\r\nsudo service redis
    start\r\nsudo chkconfig redis on\r\nsudo service docker-registry start\r\nsudo
    chkconfig docker-registry on</pre>\r\nI edited the file <i>/etc/sysconfig/docker-registry </i>and
    add the following:\r\n<pre>export SETTINGS_FLAVOR=openstack\r\nexport REGISTRY_PORT=5042
    \r\n. /root/keystonerc_admin \r\nexport OS_GLANCE_URL=http://172.16.129.26:9292</pre>\r\n<div></div>\r\nNote
    that some of the values in that file were already set.  I removed those entires.\r\n<h3>OpenStack
    for Docker Configuration</h3>\r\nI changed this entry in  /etc/nova/nova.conf\r\n<pre>compute_driver
    = docker.DockerDriver</pre>\r\nthis value (and uncommented it) in /etc/glance/glance-api.conf:\r\n<pre>container_formats
    = ami,ari,aki,bare,ovf,docker</pre>\r\n<h2>Hand Rolled Nova</h2>\r\nUnfortunately
    docker does not work with the current release of RDO icehouse.  Therefore I had
    to get the latest code from the master branch of <a href=\"https://github.com/openstack/nova\">nova</a>.
     Further I had to install it.  To be safe I put it in its own python virtualenv.
     In order to install nova like this a lot of dependencies must be installed.  Here
    is the yum command I used to install what I needed (and in some cases just wanted).\r\n<pre>yum
    update\r\n yum install -y telnet git libxslt-devel libffi-devel python-virtualenv
    mysql-devel</pre>\r\nThen I installed nova and its package specific dependencies
    into a virtualenv that I created.  The command sequence is below:\r\n<pre>git
    clone https://github.com/openstack/nova.git\r\nvirtualenv --no-site-packages /usr/local/OPENSTACKVE\r\nsource
    /usr/local/OPENSTACKVE/bin/activate\r\npip install -r requirements.txt\r\npip
    install qpid-python\r\npip install mysql-python\r\npython setup.py install</pre>\r\nAt
    this point I had an updated version of the nova software but it was running against
    an old version of the data base.  Thus I had to run:\r\n<pre>nova-manage db sync</pre>\r\nThe
    final step was to change all of the nova startup scripts to point to the code
    in the virtualenv instead of the code installed to the system.  I did this by
    opening up every file at <em>/etc/init.d/openstack-nova-*</em> and changing the
    <em>exec=\"/usr/bin/nova-$suffix\"</em> line to <em>exec=\"/usr/local/OPENSTACKVE/bin/nova-$suffix\"</em>.
     I then rebooted the VM and I was <strong>FINALLY</strong> all set to launch docker
    containers that I could ssh into!</div>\";}"
---

