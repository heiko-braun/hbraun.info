---
title: BPM Console 1.1.2 released
author: hbraun
layout: post
permalink: /2009/08/bpm-console-1-1-2-released/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2009/08/bpm-console-112-released.html
categories:
  - Uncategorized
---
BPM Conosle 1.1.2 carries minor enhancements, probably the most notable change is the switch from HTTP Basic Auth to form based authentication and session management (BPMC-12). Here&#8217;s the complete changelog:

**Release Notes &#8211; BPM Console &#8211; Version BPM Console 1.1**

  * [BPMC-7] &#8211; url is wrong in the resources page for jbpm profile 
      * [BPMC-1] &#8211; Make tasks the default editor 
          * [BPMC-2] &#8211; Move settings to the bottom 
              * [BPMC-3] &#8211; Split rendering directives and process variables in form processor 
                  * [BPMC-5] &#8211; Tomcat Lite doesn&#8217;t pickup profile changes 
                      * [BPMC-9] &#8211; Form processing requires access to principal doing the call 
                          * [BPMC-10] &#8211; Pick JAAS domain for server module from build profile 
                              * [BPMC-8] &#8211; Set the correct log for RESTEasy in JBoss As. 
                                  * [BPMC-12] &#8211; Switch to form based authentication and session management 
                                      * [BPMC-13] &#8211; Remove TX demarcation inPluginMgr</ul>