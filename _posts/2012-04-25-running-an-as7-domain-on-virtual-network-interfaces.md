---
title: Running a domain on a single machine
author: hbraun
layout: post
permalink: /2012/04/running-an-as7-domain-on-virtual-network-interfaces/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2012/04/running-as7-domain-on-virtual-network.html
dsq_thread_id:
  - 675263370
categories:
  - Wildfly
---
Sometimes it&#8217;s required to verify a domain setup with multiple hosts involved. But what if only a single machine is at your service? In this post, I am going to walk you through a simple setup that allows you to create a JBossAS 7 domain on a number of virtual hosts: Simply by binding the slave controllers to virtual network interfaces.

**Create a slave controller configuration **

Create a copy of the domain directory that ships with the default distribution.

[code]  
cp -R domain domain2  
[/code]

The slave controller configuration (domain2/configuration/host.xml) requires two significant changes:

1.) assign a distinct host name  
2.) turn the host control into a slave

The first step requires you to chose a name that distinct across the domain. We are going to name it &#8220;slave.local&#8221;:

[code]  
<host name=&#8221;slave.local&#8221; xmlns=&#8221;urn:jboss:domain:1.3&#8243;>  
[/code]

The second step is as simple. Instead of declaring another master controller (element) we point the slave controller to a master it should connect to:

[code]  
<remote host=&#8221;${jboss.domain.master.address}&#8221; port=&#8221;${jboss.domain.master.port:9999}&#8221; security-realm=&#8221;ManagementRealm&#8221;/>  
[/code]

For our purposes we stick with the expressions (${foo.bar}), because it allows us to easily pass in arguments from the command line. But you could as well provide fixed values.

**Starting the host controller and it slave**

Bring up the domain by starting the domain controller:

[code]  
./bin/domain.sh  
[/code]

Notice that we launch it without arguments. In this case it will refer to the default domain directory.

After a few seconds the host controller should up and running and started it&#8217;s default servers:

[code]  
\[Host Controller] 12:55:32,157 INFO  [org.jboss.as\] (Controller Boot Thread) JBAS015874: JBoss AS 7.1.2.Final-SNAPSHOT &#8220;Brontes&#8221; (Host Controller) started in 5194ms &#8211; Started 12 of 12 services (0 services are passive or on-demand)  
[/code]

**The virtual network interface**

Before we can launch the second controller (slave) we need to create a virtual network interface (alias) for the second process to bind to. We&#8217;ll simply create an alias on loopback adapter:

[code]  
ifconfig lo0 alias 172.16.123.1  
[/code]

Now we are ready to start the slave controller process, pointing it to the second directory:

[code]./bin/domain.sh \  
-Djboss.domain.master.address=127.0.0.1 \  
-Djboss.bind.address=172.16.123.1 \  
-Djboss.bind.address.management=172.16.123.1 \  
-Djboss.domain.base.dir=./domain2  
[/code]

After a while the main controller registers it:

[code]  
\[Host Controller] 12:59:57,260 INFO  [org.jboss.as.domain\] (domain-mgmt-handler-thread &#8211; 1) JBAS010918: Registered remote slave host &#8220;slave.local&#8221;, JBoss AS 7.1.2.Final-SNAPSHOT &#8220;Brontes&#8221;  
[/code]

This means the domain including both &#8220;hosts&#8221; (aka &#8216;master&#8217; and &#8216;slave.local&#8217;) is up and running. The same steps would be necessary to create a domain with two physical distinct hosts.

For more information please consult the JBoss AS7 Administration Guide:  
[https://docs.jboss.org/author/display/AS71/Admin+Guide][1]

Stay tuned,  
Heiko

 [1]: https://docs.jboss.org/author/display/AS71/Admin+Guide "JBoss AS7 Administration Guide"