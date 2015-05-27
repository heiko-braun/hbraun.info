---
title: 'Managing JBoss7: Staging Applications'
author: hbraun
layout: post
permalink: /2011/04/managing-jboss7-staging-applications/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2011/04/managing-jboss7-staging-applications.html
dsq_thread_id:
  - 1053545955
categories:
  - Wildfly
---
Your colleagues are all stressed out, because the new build of your b2b app needs to be put on a staging server for your external partner to verify the recent API changes. How to get this setup and running without interfering with the existing production system? It&#8217;s fairly simple. I&#8217;ll show you &#8230;

### Step1: Create a dedicated server group for your staging servers

<a href="http://1.bp.blogspot.com/-vWGkPsxGtIE/TabZbufmjoI/AAAAAAAAAIo/SS3IJNGXXVs/s1600/step1.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 311px; height: 320px;" src="http://1.bp.blogspot.com/-vWGkPsxGtIE/TabZbufmjoI/AAAAAAAAAIo/SS3IJNGXXVs/s320/step1.png" border="0" alt="" id="BLOGGER_PHOTO_ID_5595398657414696578" /></a>

### Step2: Prepare a staging server-configuration

A custom server-group separates our staging environment from the production servers.  
<a href="http://1.bp.blogspot.com/-d_PJHjzqyfM/TabZvXELqFI/AAAAAAAAAIw/ZGqiD9q8Ups/s1600/step2.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 311px; height: 320px;" src="http://1.bp.blogspot.com/-d_PJHjzqyfM/TabZvXELqFI/AAAAAAAAAIw/ZGqiD9q8Ups/s320/step2.png" border="0" alt="" id="BLOGGER_PHOTO_ID_5595398994723055698" /></a>

### &#8230; with a specific port offset 

You need to remember this, in order to connect to the server instances later on.  
<a href="http://4.bp.blogspot.com/-BNuHWMiEc4I/TabaEd82E8I/AAAAAAAAAI4/6qRz6vQ7GrQ/s1600/step3.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 311px; height: 320px;" src="http://4.bp.blogspot.com/-BNuHWMiEc4I/TabaEd82E8I/AAAAAAAAAI4/6qRz6vQ7GrQ/s320/step3.png" border="0" alt="" id="BLOGGER_PHOTO_ID_5595399357348582338" /></a>

### Launch a server instance

So we can connect to it.  
<a href="http://2.bp.blogspot.com/-rQ72KEpuvZ8/TabaS9Ja8FI/AAAAAAAAAJA/wGrKL8YzVF8/s1600/step4.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 311px; height: 320px;" src="http://2.bp.blogspot.com/-rQ72KEpuvZ8/TabaS9Ja8FI/AAAAAAAAAJA/wGrKL8YzVF8/s320/step4.png" border="0" alt="" id="BLOGGER_PHOTO_ID_5595399606240997458" /></a>

### Deploy your application

In this case a simple web application.  
<a href="http://4.bp.blogspot.com/-7nKZFen8R0A/Tabadvc5HkI/AAAAAAAAAJI/FfSp44xm4Ws/s1600/step5.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 311px; height: 320px;" src="http://4.bp.blogspot.com/-7nKZFen8R0A/Tabadvc5HkI/AAAAAAAAAJI/FfSp44xm4Ws/s320/step5.png" border="0" alt="" id="BLOGGER_PHOTO_ID_5595399791543131714" /></a>

### &#8230; to the staging server-group

Domain deployments are always associated with server-groups.  
<a href="http://4.bp.blogspot.com/-uoDr17AiliM/TabarBeXJlI/AAAAAAAAAJQ/yrH4--vnhzw/s1600/step6.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 311px; height: 320px;" src="http://4.bp.blogspot.com/-uoDr17AiliM/TabarBeXJlI/AAAAAAAAAJQ/yrH4--vnhzw/s320/step6.png" border="0" alt="" id="BLOGGER_PHOTO_ID_5595400019719431762" /></a>

<a href="http://4.bp.blogspot.com/--OCPPuRN8SE/TabbDC2Dx9I/AAAAAAAAAJY/EAPDGllwOFA/s1600/step7.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 294px; height: 320px;" src="http://4.bp.blogspot.com/--OCPPuRN8SE/TabbDC2Dx9I/AAAAAAAAAJY/EAPDGllwOFA/s320/step7.png" border="0" alt="" id="BLOGGER_PHOTO_ID_5595400432404121554" /></a>

### Verify it has been deployed successfully

<a href="http://1.bp.blogspot.com/-KM4ybyCMHeE/TabbLffDJjI/AAAAAAAAAJg/89ka3gD4eJY/s1600/step8.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 165px;" src="http://1.bp.blogspot.com/-KM4ybyCMHeE/TabbLffDJjI/AAAAAAAAAJg/89ka3gD4eJY/s320/step8.png" border="0" alt="" id="BLOGGER_PHOTO_ID_5595400577531192882" /></a>

### Grab a coffee and relax

Fairly simple, no?