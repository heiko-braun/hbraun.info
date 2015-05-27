---
title: Contributing to the JBoss 7 Management Console
author: hbraun
layout: post
permalink: /2011/03/contributing-to-the-jboss-7-management-console/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2011/03/contributing-to-jboss-7-management.html
dsq_thread_id:
  - 988001102
categories:
  - Uncategorized
---
You want to contribute to the management web interface for JBoss ? Then this should get you going.

<span class="Apple-style-span"  style=" font-weight: bold; font-size:19px;">Codebase</span>

Everything is hosted at [github][1], The best way is to [create a fork][2] of either one of the codebases listed below and work on that one.

- Authoritative master: <a class="jive-link-external-small" href="https://github.com/jbossas/console" style="font-size: 12px; color: #355491;" target="_blank">https://github.com/jbossas/console</a>  
- Most recent: <a class="jive-link-external-small active_link" href="https://github.com/heiko-braun/as7-console" style="font-size: 12px; color: #355491;" target="_blank">https://github.com/heiko-braun/as7-console</a>

### Prerequisites

The console it self is developed using the [Google Web Toolkit][3]. You would need to make yourself familiar with the basics before we et going. The GWT SDK will be installed as part of the maven build. No need to fetch it on it&#8217;s own. If you plan to work with Eclipse, then you should consider the development tools for GWT that are provided by Google. But please don&#8217;t ask how things are setup correctly in Eclipse. We baseline on maven and that&#8217;s it.

### Things you need to know

<span style="text-decoration: underline;">Widgets</span>

We build on GWT 2.2 without any dependencies on external widget libraries. However these is a growing number of widgets ([org.jboss.as.console.client.widgets][4]) that should be reused. We aim for keeping the overall number of widgets to a minimum. 

But if you need anything that doesn&#8217;t exist, take a look at the [SmartGWT showcase][5], tell us about it and we&#8217;ll then consider implementing it.

<span style="text-decoration: underline;">MVP Pattern</span>

But one of the cornerstones is the GWT Platform library, which nicely abstracts the MVP pattern. It act&#8217;s as a blueprint for the console design. A good [introduction can be found here][6]. (This is a &#8220;must read&#8221;)

<span style="text-decoration: underline;">AutoBeans</span>

<span style="text-decoration: underline;"></span>Internal model representations are build as [AutoBean&#8217;s][7]. They align well with the default GWT API and have build-in serialization support. A general guideline: Any domain representation that&#8217;s used within the console needs to be provided as an AutoBean abstraction. This means that beyond the integration layer (backend calls to the AS 7 domain) entities need to be adopted.

This is necessary to provide a baseline for the data binding used across widgets. Take a look at the form abstractions, then you&#8217;ll know what I mean. The [CellList and CellTable API&#8217;s][8] are another example.

### Discussions

We are using the AS7 mailing lists and/or IRC for discussions of technical matters, improvements, proposed patches, etc: 

- <https://lists.jboss.org/mailman/listinfo/jboss-as7-dev>

[][9]- irc.freenode.net#jboss-as7

 [1]: http://help.github.com/
 [2]: http://help.github.com/fork-a-repo/
 [3]: http://code.google.com/webtoolkit/overview.html
 [4]: http:/
 [5]: http://www.smartclient.com/smartgwt/showcase/
 [6]: http://code.google.com/p/gwt-platform/wiki/GettingStarted#Using_GWTP
 [7]: http://code.google.com/p/google-web-toolkit/wiki/AutoBean
 [8]: http://google-web-toolkit.googlecode.com/svn/javadoc/latest/index.html?overview-summary.html
 [9]: https://lists.jboss.org/mailman/listinfo/jboss-as7-dev