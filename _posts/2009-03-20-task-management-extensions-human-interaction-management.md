---
title: 'Task management extensions: Human interaction management'
author: hbraun
layout: post
permalink: /2009/03/task-management-extensions-human-interaction-management/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2009/03/task-management-extensions-human.html
dsq_thread_id:
  - 1290541890
categories:
  - Uncategorized
---
<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://2.bp.blogspot.com/_QxIFVLQdHS0/ScOThkaKcnI/AAAAAAAAACg/zHGzWmDzhnE/s1600-h/Extensions.jpg"><img style="float:left; margin:0 10px 10px 0;cursor:pointer; cursor:hand;width: 320px; height: 182px;" src="http://2.bp.blogspot.com/_QxIFVLQdHS0/ScOThkaKcnI/AAAAAAAAACg/zHGzWmDzhnE/s320/Extensions.jpg" border="0" alt=""id="BLOGGER_PHOTO_ID_5315254190145696370" /></a>

<br clear="all" />

a) Application: Some process being executed that hits a task activity

b) Task Mgr: The current jBPM4 base model for managing tasks. It includes assignments, variables, etc.

c) Notification Mgr: Decouples the notification features. I.e. email, ical,etc. The idea is borrowed from the latest code contribution.   
How and if the task management does notifications will be pluggable. We will probably provide a smtp notification mechanism as the default.

d) Form Mgr: Interfacing the outside world. Formost use would be HTML forms of some kind, but can be a WS interface as well. The Form Mgr relies on the variables and resources associated with a process.