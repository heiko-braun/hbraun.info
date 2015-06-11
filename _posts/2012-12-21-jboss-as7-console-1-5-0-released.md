---
title: JBoss AS7 Console 1.5.0 released
author: hbraun
layout: post
permalink: /2012/12/jboss-as7-console-1-5-0-released/
dsq_thread_id:
  - 985745907
categories:
  - Wildfly
---
I am very happy to announce the 1.5.0 release of the [AS7 web management interface][1]. This release is intended to be used with [AS 7.2][2] and [EAP 6.1][3]. 

Among plenty of bug fixes here&#8217;s a quick overview of the most notable enhancements:

**Domain Topology Overview**  
All hosts, servers and groups at a glance. You can start, stop single instances or complete groups from a single view.

<a href="/2012/12/jboss-as7-console-1-5-0-released/topology/" rel="attachment wp-att-414"><img src="/wp-content/uploads/2012/12/topology-300x273.png" alt="topology" width="300" height="273" class="aligncenter size-medium wp-image-414" /></a>

**Deployment Browser**  
This has been one the highly requested features: Drill down into deployments and subsystem references.

<a href="/2012/12/jboss-as7-console-1-5-0-released/deployment_browser/" rel="attachment wp-att-415"><img src="/wp-content/uploads/2012/12/deployment_browser-300x273.png" alt="deployment_browser" width="300" height="273" class="aligncenter size-medium wp-image-415" /></a>

**Unmanaged Deployments**  
Support for unmanaged deployments.

<a href="/2012/12/jboss-as7-console-1-5-0-released/unmanaged_deployment/" rel="attachment wp-att-416"><img src="/wp-content/uploads/2012/12/unmanaged_deployment-300x287.png" alt="unmanaged_deployment" width="300" height="287" class="aligncenter size-medium wp-image-416" /></a>

**Improved Expression Support**  
The web interface now supports expressions on all attributes and provides a tool to resolve expression values from any view.

<a href="/2012/12/jboss-as7-console-1-5-0-released/expression_resolver/" rel="attachment wp-att-417"><img src="/wp-content/uploads/2012/12/expression_resolver-300x231.png" alt="expression_resolver" width="300" height="231" class="aligncenter size-medium wp-image-417" /></a>

**Analytics Integration**  
To get a better idea, which tools matter most we&#8217;ve integrated analytics support.

<a href="/2012/12/jboss-as7-console-1-5-0-released/tool_usage/" rel="attachment wp-att-418"><img src="/wp-content/uploads/2012/12/tool_usage-300x146.png" alt="tool_usage" width="300" height="146" class="aligncenter size-medium wp-image-418" /></a>

Special thanks to *Harald Pehl* for his recent contributions. He did provide the topology overview and the deployments browser.

The full release notes can be found here:  
<http://jbossas.github.com/console/releases.html>

Merry Christmas,  
Heiko

 [1]: http://jbossas.github.com/console/index.html
 [2]: http://www.jboss.org/jbossas
 [3]: http://www.redhat.com/products/jbossenterprisemiddleware/application-platform/