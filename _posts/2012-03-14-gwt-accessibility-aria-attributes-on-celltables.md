---
title: 'GWT Accessibility: Aria attributes on CellTables'
author: hbraun
layout: post
permalink: /2012/03/gwt-accessibility-aria-attributes-on-celltables/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2012/03/improving-gwt-aria-attributes-on.html
dsq_thread_id:
  - 675920710
categories:
  - Uncategorized
---
While working on the accessibility issues for the AS7 console, we&#8217;ve realized that the new CellTable implementation misses the [aria grid attributes][1]. For the ones of you new to this topic: [Aria][2] defines a way to make Web content and Web applications more accessible to people with disabilities. It especially helps with dynamic content and advanced user interface controls developed with Ajax, HTML, JavaScript, and related technologies.

We&#8217;ve already submitted a patch to the core GWT team. If this issue is important to you, please vote for it :

<http://code.google.com/p/google-web-toolkit/issues/detail?id=7245>

 [1]: http://www.w3.org/TR/wai-aria/roles#grid
 [2]: http://www.w3.org/WAI/intro/aria