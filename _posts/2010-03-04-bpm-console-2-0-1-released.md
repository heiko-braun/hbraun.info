---
title: BPM Console 2.0.1 released
author: hbraun
layout: post
permalink: /2010/03/bpm-console-2-0-1-released/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2010/03/bpm-console-201-released.html
dsq_thread_id:
  - 844030545
categories:
  - BPM
---
I am glad to announce the BPM Console 2.0.1. Although it doesn&#8217;t include many new functional enhancements, architecturally it&#8217;s still a major step forward. Let&#8217;s take a look at the most prominent changes first:

<span style="font-weight:bold;">Workspace API consolidation</span>

This is probably one of the most important steps. Something that we had on the roadmap for quiet some time. Before 2.0.x the BPM build on it&#8217;s own workspace API, which is fully merged with [errai-workspaces][1]. Not only does this consolidate the web tooling efforts within JBoss, but it also allows building of true federated toolsets using the errai bus and workspaces modules as a foundation.

This allows us to easily integrate tools from other JBoss projects into a custom workspace build. I.e. something that we are currently thinking about is integrating the [Apache Juddi][2] web console as part of the [Riftsaw console][3] offering. 

<span style="font-weight:bold;">Improved performance and development tools</span>

We&#8217;ve been running the console on GWT 1.5.3 for quiet some time but now it leverages [GWT 2.0][4]. Probably the most important changes for the BPM console are support for code splitting and declarative UI&#8217;s.

<span style="font-weight:bold;">JBoss system theme</span>

We started working on a custom theme, that should apply to JBoss web tooling in general. It&#8217;s still in the early stages, but already included in the recent release. We are aiming for a design that&#8217;s clean, concise and doesn&#8217;t get in your way:

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://1.bp.blogspot.com/_QxIFVLQdHS0/S4-w1lVNQVI/AAAAAAAAAFw/WTu5w5040RQ/s1600-h/process.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 256px;" src="http://1.bp.blogspot.com/_QxIFVLQdHS0/S4-w1lVNQVI/AAAAAAAAAFw/WTu5w5040RQ/s320/process.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5444764909114835282" /></a>

<span style="font-weight:bold;">Role based authorization</span>

Since we migrated to errai-workspaces the BPM console now has [support for role based authorization][5]. This means you can easily restrict access to certain tools (i.e. admin vs. user) or use this mechanism to create customized profiles according to a users role (i.e. sales vs. marketing)

<pre><br />@LoadTool(name = "Deployments", group = "Runtime")<br />@RequireRoles({"administrator"})<br />public class DeploymentModule implements WidgetProvider<br />{<br />  [...]<br />}<br /></pre>

<span style="font-weight:bold;">History and perma links</span>

One feature that has been requested a lot, was support for linking to tools from an external application. I.e. when a email notification is send for an outstanding task. This is now built into errai-workspaces. The same mechanism that allows you to use the default browser history navigation, can now be used to reference tools from external applications.

<span style="font-weight:bold;">Report parameter preferences</span>

The console supports parametrized [report templates][6] since version 1.3. What has been added is the ability to store report parameters for each template as part of the console preferences. Imagine a report that requires you to enter a certain time period for rendering. This data is now store within as part of console preferences, so can easily switch between report templates without having to provide that data over and over again.

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://1.bp.blogspot.com/_QxIFVLQdHS0/S4-2sVj6TJI/AAAAAAAAAF4/DVBpdX-Olmo/s1600-h/Screen+shot+2010-03-04+at+2.33.13+PM.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 226px;" src="http://1.bp.blogspot.com/_QxIFVLQdHS0/S4-2sVj6TJI/AAAAAAAAAF4/DVBpdX-Olmo/s320/Screen+shot+2010-03-04+at+2.33.13+PM.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5444771347332484242" /></a>

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://4.bp.blogspot.com/_QxIFVLQdHS0/S4-2z4Iv1CI/AAAAAAAAAGA/Fol3QoTFfEo/s1600-h/Screen+shot+2010-03-04+at+2.32.49+PM.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 58px;" src="http://4.bp.blogspot.com/_QxIFVLQdHS0/S4-2z4Iv1CI/AAAAAAAAAGA/Fol3QoTFfEo/s320/Screen+shot+2010-03-04+at+2.32.49+PM.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5444771476872877090" /></a>

<span style="font-weight:bold;">Roadmap</span>

In the next few weeks we&#8217;ll focus on the toolset for the [Riftsaw BPEL Engine][7]. Areas that need improvement are activity monitoring tools and tools for maintaining WS endpoint references, like the [UDDI browser][8]. 

<span style="font-weight:bold;">Contributions</span>

As I said earlier, 2.0.x was an important step regarding maintainability and API consolidation. We now have everything in place for you to [get your hands on the errai-workspaces module and start developing][9] plugins for the BPM console in particular or the JBoss SOA platform in general. In case you are interested, don&#8217;t hesitate to get in touch with us:

IRC: errai@irc.freenode.net  
Mail: <http://jboss.org/errai/MailingLists.html>

 [1]: https://www.jboss.org/errai/ErraiWorkspaces
 [2]: http://ws.apache.org/juddi/
 [3]: http://www.jboss.org/riftsaw
 [4]: http://code.google.com/webtoolkit/doc/latest/ReleaseNotes.html
 [5]: http://download.jboss.org/errai/docs/1.0.0.GA/userguide/index.html#rolebased
 [6]: http://community.jboss.org/wiki/BPMConsole-Reporting
 [7]: http://jboss.org/riftsaw
 [8]: http://docs.jboss.com/riftsaw/2.0-CR2/userguide/html/uddi.html
 [9]: http://download.jboss.org/errai/docs/1.0.0.GA/userguide/index.html#using-workspaces