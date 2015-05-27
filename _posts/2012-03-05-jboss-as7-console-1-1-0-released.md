---
title: 'JBoss AS7: Console 1.1.0 released'
author: hbraun
layout: post
permalink: /2012/03/jboss-as7-console-1-1-0-released/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2012/03/jboss-as7-console-110-released.html
dsq_thread_id:
  - 688882365
categories:
  - Uncategorized
---
We&#8217;ve added four additional subsystems, that are manageable through the console now.

<span style="font-weight:bold;">New Subsystem Support</span>

- mail  
- modcluster  
- infinispan  
- jgroups

This completes the number of manageable subsystems the full-ha profile offers.

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://1.bp.blogspot.com/-AJKMDkIGBUQ/T1SvnVytgvI/AAAAAAAAAIE/Kj2IVeLXRtk/s1600/Screen%2BShot%2B2012-03-05%2Bat%2B1.20.17%2BPM.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 224px;" src="http://1.bp.blogspot.com/-AJKMDkIGBUQ/T1SvnVytgvI/AAAAAAAAAIE/Kj2IVeLXRtk/s320/Screen%2BShot%2B2012-03-05%2Bat%2B1.20.17%2BPM.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5716386917439603442" /></a>

In order to access the new functionality, the server needs to be running the full-ha profile:

<tt><br />./bin/standalone.sh --server-config=standalone-full-ha.xml<br /></tt>

<span style="font-weight:bold;">Environment Properties</span>

This is a feature that has been requested by the community several times: The possibility to view the environment properties (ENV, -Dfoo=bar, etc) that have been set when the server was started. 

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://4.bp.blogspot.com/-82PDSkx4UTE/T1SvPJ9BOzI/AAAAAAAAAH4/ohEepu8BWMo/s1600/Screen%2BShot%2B2012-03-05%2Bat%2B1.18.46%2BPM.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 184px;" src="http://4.bp.blogspot.com/-82PDSkx4UTE/T1SvPJ9BOzI/AAAAAAAAAH4/ohEepu8BWMo/s320/Screen%2BShot%2B2012-03-05%2Bat%2B1.18.46%2BPM.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5716386501944752946" /></a>

Rock on´