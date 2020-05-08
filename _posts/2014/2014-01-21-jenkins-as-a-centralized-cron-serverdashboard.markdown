---
layout: post
title: Jenkins as a Centralized Cron Server/Dashboard
date: 2014-01-21 08:34:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Cron. Jenkins
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '5105542264947960529'
---
<div dir="ltr" style="text-align:left;">h3.  Jenkins</p>
<p>{quote}Jenkins is an open source continuous integration tool written in Java.</p>
<p>Jenkins provides continuous integration services for software development. It is a server-based system running in a servlet container such as Apache Tomcat. It supports SCM tools including CVS, Subversion, Git, Mercurial, Perforce, Clearcase and RTC, and can execute Apache Ant and Apache Maven based projects as well as arbitrary shell scripts and Windows batch commands. The primary developer of Jenkins is Kohsuke Kawaguchi.[3] Released under the MIT License, Jenkins is free software.[4]<br />Builds can be started by various means, including being triggered by commit in a version control system, scheduling via a cron-like mechanism, building when other builds have completed, and by requesting a specific build URL.{quote}</p>
<p>h3. features :</p>
<p>h5. History :</p>
<p>Jenkins can be configured to retain logs of jobs that it has run. So You have full visibility of what's happening with your system.</p>
<p>Centralized management<br />With Jenkins you can manage all your imortant cron  jobs centrally.You can also export all Jenkins jobs as XML and check it into a repository.</p>
<p>Alert only if the Jobs fails :<br />If you enable email for Cron , You end up with too much of emails and eventully end up ignoring them. Jenkins on other hand can be configured to alert only when a particular job fails ie. a job exits with return code other than 0.<br />In addition you can use the awesome Jenkins Text Finder plugin which allows you to specify words or regular expressions to look for in console output. They can be used to mark a "job" unstable. F</p>
<p>h5. Job dependency :</p>
<p>With Jenkins you can trigger one job only after the first one completes successfully. Creating a well known Dependacy structure and rely on it.</p>
<p>h5. Test immediately :</p>
<p>With Jenkins you can click Build Now and job will run immediately. Where in Cron you have wait for the specified schedule to execute.</p>
<p>h5. Quick  setup</p>
<p>Setting up jobs is easy.</p>
<p>h3. Pros/Cons :</p>
<p>* Backup and restoration becomes very handy.<br />* We can control the access to Jenkins based on LDAP role.<br />* Can have multi node Jenkins setup for failover.<br />* We can schedule the cron job's with dependency i.e. start job B once Job A completes<br />* Each Job have its history preserved , when did it last run , when failed etc.<br />* The output of  each job is also captured.<br />* we can have email alert if the job fails.<br />* We must have ssh trust between Jenkins server and the target hosts.<br />* Need to research further.</p>
<p>h3. Implementation method</p>
<p>* h5. Jenkins External Monitor - ( Using your Existing Cron )</p>
<p># Make Sure the `Jenkins External Monitor Job` plugin is installed.<br /># Add a New Job in Jenkins, with a type 'Monitor an external job' ( Pick a relevent and name and provide the brief description )<br /># Now on the remote server<br /><span class="Apple-tab-span" style="white-space:pre;"> </span># Make sure the Java is installed<br /><span class="Apple-tab-span" style="white-space:pre;"> </span># export the JENKINS_HOME variable JENKINS_HOME=http://host1:8080  ( You can add this info in your .bashrc or Crontab as well )<br /><span class="Apple-tab-span" style="white-space:pre;"> </span># If the security on Jenkins server is enabled and only authorized users can run a Job, then JENKINS_HOME should be:<br />             export JENKINS_HOME=http://user_id:password@host1:8080<br /><span class="Apple-tab-span" style="white-space:pre;"> </span># Copy below files from Jenkins server to the remote server in /root/jenkins direcorty<br /><span class="Apple-tab-span" style="white-space:pre;"> </span>{code} jenkins-core-*.jar remoting-*.jar ant-[1-9]*.jar commons-io-[1-9]*.jar  commons-lang-[0-9]*.jar jna-posix-*.jar xstream-*.jar {code}<br /><span class="Apple-tab-span" style="white-space:pre;"> </span><br /><span class="Apple-tab-span" style="white-space:pre;"> </span># Add below 2 lines to your crontab<br />        {code}<br /><span class="Apple-tab-span" style="white-space:pre;"> </span>export JENKINS_HOME=http://user_id:password@host1:8080<br /><span class="Apple-tab-span" style="white-space:pre;"> </span>* * * * * export JENKINS_HOME=$JENKINS_HOME; java -jar /root/jenkins/jenkins-core-*.jar "Job_Name_In_Jenkins" /path_to/script 2&gt;&amp;1 &gt; /dev/null<br />        {code}</p>
<p>* h5. Jenkins SSH<br /># Make Sure the `Jenkins SSH` plugin is installed<br /># Add the remote hosts details in “Manage Jenkins” –&gt; “Configure System” -&gt; “SSH remote hosts” -&gt; “Add“ ( fill in the details)<br /># Add new Job in Jenkins , with a type “Build a free-style software project”  ( Pick a relevent and name and provide the brief description )<br /># Now add in the details for this Job<br /># Source Code Management -&gt;None<br /># Build Triggers -&gt; Build periodically -&gt; Schedule -&gt; put a cron schedule<br /># Build Environment -&gt; Execute shell script on remote host using ssh -&gt; Select the Site added already in above step.<br /># provide the Pre build script and Post build script , rest all configurations are up to your own requirement.</p>
<p>----</p>
<p>h3. Another proposed solution: Tron</p>
<p>{quote}Tron is a centralized system for managing periodic batch processes and services across a cluster{quote}</p>
<p>h4. The good...</p>
<p>* Manage dependencies between batch process<br />* A centralized configuration for batches which run on many machines<br />* Start and restart services running on many machines<br />* Monitor and report on batch process and services</p>
<p>h4. Tron Architecture</p>
<p>* Tron is a python daemon that executes Jobs or Services across multiple Nodes.<br />* It is powered by SSH. Meaning Tron just needs to be installed in one centralized location and configured to remotely execute commands.<br />* Tron manages executing Jobs based on predefined schedules. It resolves dependencies between other jobs in a work flow. It maintains the history of job runs for later reporting. It has a flexible system for monitoring job failures.<br />* State and job output (stdout/stderr) are stored on disk to avoid loss due to machine failure.<br />* Tron communicates with command line tools, web interface, or whatever else you can dream up via a REST API.</p>
<p>!http://yelp.typepad.com/.a/6a00d83452b44469e20134871f25c7970c-pi|border=1!</p>
<p>h4. [Tron homepage|https://github.com/Yelp/Tron/wiki]<br />----</div>
