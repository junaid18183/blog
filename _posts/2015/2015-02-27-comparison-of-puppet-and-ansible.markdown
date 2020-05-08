---
layout: post
title: Comparison of Puppet and Ansible
date: 2015-02-27 13:27:12.000000000 +05:30
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
  post_id: '899'
  blog_id: '1765838'
  reblog_snapshot: "O:8:\"stdClass\":8:{s:5:\"title\";s:32:\"Comparison of Puppet
    and Ansible\";s:4:\"type\";s:4:\"post\";s:9:\"mime_type\";s:0:\"\";s:6:\"format\";b:0;s:12:\"modified_gmt\";s:19:\"2015-01-04
    20:36:58\";s:9:\"permalink\";s:75:\"https://ifireball.wordpress.com/2015/01/03/comparison-of-puppet-and-ansible\";s:7:\"content\";s:14891:\"<div
    class=\"reblogged-content\">\n\n<a href=\"https://junaid18183.files.wordpress.com/2015/02/puppet-vs-ansible.png\"><img
    class=\"alignright wp-image-913 size-medium\" title=\"Puppet vs. Ansible\" src=\"https://junaid18183.files.wordpress.com/2015/02/puppet-vs-ansible.png\"
    alt=\"Puppet vs. Ansible\" width=\"300\" height=\"212\" data-originalSrc=\"https://ifireball.files.wordpress.com/2015/01/puppet-vs-ansible.png?w=300\"
    data-rehosted=\"1\"></a>A configuration management system is a crucial tool in
    the tool box of any sysadmin. I have been using and advocating <a title=\"Puppet\"
    href=\"http://puppetlabs.com/\">Puppet</a> for several years now. Recently I have
    noticed that <a title=\"Ansible\" href=\"http://www.ansible.com/home\">Ansible</a>
    had emerged to be considered as an alternative to Puppet. I've decided to give
    Ansible a good look, evaluate its strengths and weaknesses, and decide if, by
    chance, it is time for me to put Puppet aside.\r\n\r\n<!--more-->\r\n<h3>Server
    installation</h3>\r\nProperly setting up a Puppetmaster can be a challenging task.
    To obtain basic setup one needs to do no more than install a package. However,
    To enjoy the full capabilities of Puppet, one needs to layer many additional tools
    on top, including:\r\n<ul>\n<li>Setting up <a title=\"Passenger\" href=\"https://www.phusionpassenger.com/\">Passenger</a>
    with Apache or Nginx to make the Puppetmaster more scaleable.</li>\r\n\t<li>Adding
    PostgreSQL and <a title=\"PuppetDB\" href=\"https://docs.puppetlabs.com/puppetdb/latest/\">PuppetDB</a>
    to enable advanced cross-server features such as '<a title=\"Puppet Exported Resources\"
    href=\"https://docs.puppetlabs.com/puppet/latest/reference/lang_exported.html\">Exported
    Resources</a>'.</li>\r\n\t<li>Layering a <a title=\"Puppet Dashboard\" href=\"https://github.com/sodabrew/puppet-dashboard\">management
    and reporting system</a> on top to obtain GUI capabilities.</li>\r\n</ul>\r\nMany
    of the steps above could be greatly simplified by using ready-made Puppet modules.
    Prepackaged solutions can also be obtained either for a <a title=\"Puppet Enterprise\"
    href=\"http://puppetlabs.com/puppet/puppet-enterprise\">price</a> or for <a title=\"The
    Foreman\" href=\"http://theforeman.org/\">free</a>.\r\n\r\nAnsible doesn't really
    have a server. The common configuration of Ansible seems to be to install it locally
    on the laptop of the sysadmin or developer using it, and run it ad-hoc when needed.
    While this makes initial setup quick and easy (Install one package on one machine,
    and away you go), it also means you lose the benefit of having a server act as
    a central location for data gathering and coordination. The Ansible developers
    had seen the need for a server of sort, and provide a solution in the form of
    <a title=\"Ansible Tower\" href=\"http://www.ansible.com/tower\">Ansible Tower</a>.
    Ansible Tower is a proprietary, closed source, solution. I will not cover it here.\r\n<h3>Client
    architecture and installation</h3>\r\nPuppet client installation is quite straight
    forward. One typically has to install the puppet client package vie the operating
    system's package manager, and then run it with the '<code>waitforcert</code>'
    parameter to make it obtain a signed certificate from the Puppetmaster server.
    The signing of the certificate could either be done manually on the Puppetmaster,
    or automated by creating an 'autosign' file. Once the client had run for the first
    time, further configuration (if needed) could be done via Puppet itself by distributing
    the '<code>/etc/puppet.conf</code>' file. The Puppet client installation could
    be very easily embedded in to the host deployment processes performed via deployment
    automation systems such as Kickstart. This way hosts can automatically become
    managed by Puppet with no need for sysadmin intervention.\r\n\r\nAnsible claims
    to make things simple by not having a client at all and leveraging SSH instead.
    This does sound simpler but in practice, it creates a situation where the sysadmin
    would have to create his own solutions for managing and distributing SSH keys
    as well as managing the 'known_hosts' file on the machine Ansible is invoked from.
    These solutions cannot be created using Ansible itself because they must be in
    place before Ansible can run. While SSH key distribution could be performed as
    a Kickstart post-installation task, it is more complex to accomplish then simply
    running a command provided by the configuration management system. It is only
    fair to mention that on cloud-hosted virtual machines, SSH key distribution is
    already taken care of by the cloud infrastructure.\r\n\r\nApart from enabling
    SSH connections from the machine running Ansible to the clients, a sysadmin also
    needs to devise means to gather information about which hosts exist. This can
    be done either by manually maintaining an inventory file or by integrating 3rd-party
    means of discovering hosts. This problem can also be mitigated in cloud environments
    where the environment can report to Ansible which hosts had been created within
    it.\r\n\r\nI find Puppet's 'pull' architecture to be more robust and useful then
    Ansible's push-over-SSH. Since Puppet clients can be set up to periodically report
    their state to the sever, it can be used as a crude monitoring system, measuring
    client's health by the frequency of reports arriving from it. Having an 'x509' 
    certificate authority and distribution system embedded into the configuration
    management system means you have handy certificates you can use for other things,
    such as securing communications to application messaging systems. The pull architecture
    also enables one to better secure the clients by using a firewall to block all
    incoming TCP connections. With Ansible you have to keep the SSH port open.\r\n<h3>Configuration
    language</h3>\r\nPuppet has a declarative domain-specific-language (DSL) that
    allows a sysadmin to map out how hosts should be configured. The design of the
    language is such that it encourages high-level and abstract style of describing
    what a host should be like rather the what should be done to it. This creates
    a situation where a well written, so-called, configuration manifest file can be
    used to obtain the same goals across many operating systems and hardware types.\r\n\r\nWhen
    configurations get complex, the Puppet language offers abstraction mechanisms
    in the form of custom 'defined resources' and 'classes'.\r\n\r\nThe puppet language
    has its shortcomings, the declarative nature of the language means it can be harder
    to learn for sysadmins accustomed to the imperative nature of shell scripting
    languages. It also means that controlling exact ordering of execution of configuration
    changes can be tricky, requiring one to manually specify configuration dependencies.\r\n\r\nAnsible's
    language, despite being based on the declarative YAML language, is imperative.
    Ansible playbooks are a sequence of plays to be carried out on different groups
    of hosts. Plays are in turn sequences of tasks that invoke modules to commit changes
    to individual hosts. In essence Ansible provide a high-level scripting language
    that can run across hosts.\r\n\r\nI consider one of the most important aspects
    on a language is its ability to convey the meaning of a thing described with it
    over time. I think the Puppet DSL wins here. A well-written puppet manifest is
    a terse description of the nature of the configuration applied to a host. An Ansible
    playbook is a description of how to get a certain configuration. A deeper understanding
    of the result of the process may be harder to obtain. One means Ansible provides
    to bridge that gap is forcing one to enter a textual description for each and
    every task.\r\n\r\nAnsible includes language feature called 'roles'. Ansible 'roles'
    are collections of tasks which are declarative in nature. With discipline, one
    can end up using roles to create Ansible playbooks that are very terse and declarative.
    Novice users of the Puppet DSL can end up creating manifest files that are too
    long and complex and end up providing less then adequate description of their
    purpose.\r\n<h3>Change management and control</h3>\r\nPuppet can be run with the
    '<code>--noop</code>' parameter to make it show what changes are going to be made
    to a particular host without actually committing them. Comparably, Ansible provides
    the '<code>--check</code>' option which does the same thing.\r\n\r\nBoth tools
    encourage users to use a source code management system (SCM) such as Git to track
    changes being made to the configuration language source files.\r\n\r\nPuppet is
    architecturally designed to have the client agent run periodically in order to
    detect and possibly automatically mend configuration drift, e.g. hosts no longer
    conforming with their prescribed configuration. The Puppetmaster, when coupled
    with the PuppetDB collects information that allows the sysadmin to determine exactly
    where and which configuration drift had occurred in the network.\r\n\r\nAnsible
    could theoretically be setup to be run periodically form a centralized server
    against a predetermined playbook in order to detect drift. It seems that Ansible`s
    design and architecture doesn`t make it very efficient for that kind of use. One
    would also need to devise a way to collect reporting data over time to make it
    useful.\r\n\r\nPuppet provides the concept of 'environments'  as a means to have
    different hosts run against different versions of the configuration. This provides
    a way to test configuration changes against staging servers for example, without
    affecting the production servers. Ansible's nature of ad-hoc invocation creates
    a situation where such a feature is not needed. One can simply decide at invocation
    time which servers to run against.\r\n<h3>Host information management</h3>\r\nPuppet
    has a sibling tool called 'Facter' which can gather various facts about a particular
    host. Those facts can them be used inside manifest files to tune the configuration
    to that specific host. The facts are also collected and stored by the Puppetmaster
    in the PuppetDB. The facts could then be queried to generate various reports about
    the hosts puppet runs on. In this manner Puppet provides very detailed and useful
    host inventory.\r\n\r\nLike Puppet, Ansible collects facts about a host when it
    is invoked to run on it and can use those facts to tune the actions being performed
    on that host. Ansible, however, throws away the facts once a particular playbook
    execution has ended and does not provide means to store and query facts over time.\r\n\r\nAnsible
    can use various sources to gather facts from. That includes sources like Facter
    and also sources that are extrinsic to the host such as the cloud infrastructure
    running it. Facter, in comparison, only gathers information from the host itself.
    While plugins can be written to make Facter gather information from other sources,
    its design doesn't lend itself to making that task easy.\r\n<h3>Push Orchestration</h3>\r\nI
    call \"Push Orchestration\" the situation where a command or a set of commands
    are sent ad-hoc to a group of hosts to be performed immediately.\r\n\r\nAnsible's
    very design revolves around push orchestration, so its no surprise it provides
    easy means to run arbitrary commands on sets of hosts.\r\n\r\nPuppet architecture
    of periodically executing agents does not lend itself to be used for \"Push Orchestration\".
    When committing changes through Puppet, one typically has to wait until the Puppet
    agent had completed its periodic run on all the designated hosts for the changes
    to take place. Puppet also does no provide any easy means to make a particular
    command be run only once.\r\n\r\nPuppet has a complementary tool called <a title=\"Marionette
    Collective AKA MCollective\" href=\"http://puppetlabs.com/mcollective\">MCollective</a>
    which is designed for \"Push Orchestration\". That tool is, however, considered
    difficult to setup ans use and is not widely used.\r\n<h3>Service Orchestration</h3>\r\nI
    call \"Service Orchestration\" the situation where setting up a service requires
    creating a complex configuration with inter-dependencies between different hosts.\r\n\r\nAnsible
    imperative ad-hoc nature makes it simple to carry out such a configuration. One
    can simply create a playbook where certain steps are performed of a certain hosts,
    then other steps are preformed on another host using information gathered in the
    previous steps, and so forth.\r\n\r\nPuppet can also be used for complex service
    orchestration by means of a language feature called \"exported resources\" that
    allows Puppet to move commands and information between different hosts. When performing
    \"Service Orchestration\" with Puppet, one takes the approach of having each host
    configured individually with the information available, while generating additional
    information for use by other hosts. It can take several Puppet runs until the
    configuration on all relevant hosts settles down to the final desired state.\r\n\r\nIt
    can be difficult to design and implement complex distributed configuration with
    the tools provided by Puppet, doing it in the imperative way described by Ansible
    can be simpler.\r\n<h3>Included Batteries</h3>\r\nAnsible comes pre-packaged with
    a large variety of modules that allow performing many different operations oh
    hosts such as running commands, managing files, users and packages and interacting
    with visualization and cloud infrastructure.\r\n\r\nPuppet, in comparison, includes
    a smaller and simpler set of basic types included in the default installation.
    It can, however, be easily extended by adding modules (by means of a provided
    tool) from the <a title=\"Puppetforge\" href=\"https://forge.puppetlabs.com/\">Puppetforge</a>
    module repository.\r\n<h3>Conclusion</h3>\r\nAfter looking deeply into both tools,
    I have concluded that, while there are some overlaps between the two tools, eventually
    they are far outweighed by the differences, and most importantly, the different
    and complementary use cases.\r\n\r\nAnsible lends itself for performing complex
    ad-hoc, on-off tasks across large groups of servers. It can be setup with as little
    as one command run on a sysadmin's laptop and then used immediately for tasks
    such as setting up and deploying complex system architectures and carrying out
    sensitive rolling upgrades. I see this tool as most fitting for a sysadmin that
    carries out freelance or consulting kind of work, roaming between different networks
    and organizations while carrying his tools of trade with him in his laptop.\r\n\r\nPuppet
    lends itself to managing large and complex networks over time. It provides a centralized
    server that can be used to monitor hosts, gather information about then and measure
    their compliance to predetermined configuration formally-specified policy. It
    also provides means to perform well-controlled network-wide changes and upgrades
    over time. I see Puppet as being mainly used by a sysadmin that is charged with
    maintaining a set of servers and systems over time, gaining good familiarity with
    their fine details and keeping up-times long.</div>\";s:15:\"images_mirrored\";i:1;}"
---

