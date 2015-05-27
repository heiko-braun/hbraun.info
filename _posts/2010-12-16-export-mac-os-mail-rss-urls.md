---
title: 'Export Mac OS Mail RSS URL&#8217;s'
author: hbraun
layout: post
permalink: /2010/12/export-mac-os-mail-rss-urls/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2010/12/export-mac-mail-rss-urls.html
dsq_thread_id:
  - 1048501249
categories:
  - Uncategorized
---
Neat and simple: 

pubsub &#8211;client com.apple.mail list | cut -f3 | sed -ne &#8216;3,$p&#8217;