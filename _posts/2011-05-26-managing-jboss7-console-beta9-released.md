---
title: 'Managing JBoss7: Console Beta9 released'
author: hbraun
layout: post
permalink: /2011/05/managing-jboss7-console-beta9-released/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2011/05/manage-jbossas7-console-beta9-released.html
dsq_thread_id:
  - 707283542
categories:
  - Wildfly
---
We just updated to 1.0.0.Beta9:  
===================

- suport for standalone  
- i18n  
- deployments  
- authentication

- datasources  
- jms configurations  
- messaging  
- web subsystem

- server groups  
- server configurations

- system properties  
- jvm options  
- socket bindings

The given functionality has small glitches here and there but most of it has been reported and is being worked on. In terms real tasks, this is still outstanding:

- transaction subsystem  
- security  
- webservices  
- threads  
- logging

But we expect this to be ready for 7.0.CR1.

Give it try &#038; let us know what you think.   
Tell us what works and what doesn&#8217;t.

How do I access the console?  
==================

http://localhost:9990/console

How do I enable authentication?  
====================

Simply create a security realm configuration.   
This needs to be done in &#8220;domain/configuration/host.xml&#8221; for domain mode: 

<pre><br />&lt;management><br />       &lt;security-realms><br />           &lt;security-realm name="ManagementRealm"><br />               &lt;authentication><br />                   &lt;users><br />                       &lt;user username="admin"><br />                           &lt;password><br />                               password<br />                           &lt;/password><br />                       &lt;/user><br />                   &lt;/users><br />               &lt;/authentication><br />           &lt;/security-realm><br />       &lt;/security-realms><br />   &lt;/management><br />   &lt;management-interfaces><br />       &lt;native-interface interface="public" port="9999"/><br />       &lt;http-interface interface="public" <br />            port="9990" security-realm="ManagementRealm"/><br />   &lt;/management-interfaces><br /><br /></pre>

Or &#8220;standalone/configuration/standalone.xml&#8221;:

<pre><br />&lt;management><br />       &lt;security-realms><br />           &lt;security-realm name="ManagementRealm"><br />               &lt;authentication><br />                   &lt;users><br />                       &lt;user username="admin"><br />                           &lt;password>password&lt;/password><br />                       &lt;/user><br />                   &lt;/users><br />               &lt;/authentication><br />           &lt;/security-realm><br />       &lt;/security-realms><br />   &lt;/management><br /><br />   &lt;management-interfaces><br />      &lt;native-interface interface="default" port="9999"/><br />      &lt;http-interface interface="default" <br />              port="9990" security-realm="ManagementRealm"/><br />   &lt;/management-interfaces><br /><br /></pre>

How do I switch between standalone and domain administration?  
========================================

Just boot AS7 in either one of these modes and reload the console web application.