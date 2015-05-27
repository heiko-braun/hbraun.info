---
title: AS7 Console performance improvements
author: hbraun
layout: post
permalink: /2011/06/as7-console-performance-improvements/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2011/06/as7-console-performance-improvements.html
categories:
  - Uncategorized
---
I did take a look at the components that serve the console files again and removed some really sloppy parts and tweaked the HTTP cache behavior a little bit. With some really interesting results.

This is what the average page loading time looked like, when client did access the console for the first time:

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://3.bp.blogspot.com/-C05kyKehBck/Tfdj63RKnSI/AAAAAAAAAK0/NA3fePFjSxI/s1600/Screen%2Bshot%2B2011-06-14%2Bat%2B3.36.19%2BPM.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 11px;" src="http://3.bp.blogspot.com/-C05kyKehBck/Tfdj63RKnSI/AAAAAAAAAK0/NA3fePFjSxI/s320/Screen%2Bshot%2B2011-06-14%2Bat%2B3.36.19%2BPM.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5618068923087494434" /></a>

This is what looks like after the improvements:

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://4.bp.blogspot.com/-75wXCg4ZmvA/TfdkOa3tASI/AAAAAAAAAK8/5iUIt9DQYuE/s1600/Screen%2Bshot%2B2011-06-14%2Bat%2B3.37.04%2BPM.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 12px;" src="http://4.bp.blogspot.com/-75wXCg4ZmvA/TfdkOa3tASI/AAAAAAAAAK8/5iUIt9DQYuE/s320/Screen%2Bshot%2B2011-06-14%2Bat%2B3.37.04%2BPM.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5618069259061887266" /></a>

It get&#8217;s even better, when a client does access the console subsequently:

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://3.bp.blogspot.com/-7qu7S2ybYBE/TfdkeniHneI/AAAAAAAAALE/W09fAkhMfVk/s1600/Screen%2Bshot%2B2011-06-14%2Bat%2B3.38.40%2BPM.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 13px;" src="http://3.bp.blogspot.com/-7qu7S2ybYBE/TfdkeniHneI/AAAAAAAAALE/W09fAkhMfVk/s320/Screen%2Bshot%2B2011-06-14%2Bat%2B3.38.40%2BPM.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5618069537338924514" /></a>

<span style="font-weight:bold;"> How can it be explained?</span>

Well the most notable improvement is probably the replacement of the sloppy IO parts. Hence the drastic page loading times from ~4sec to ~1sec. Furthermore the addition of an HTTP &#8220;Expires&#8221; header allows the browser to successfully cache the results, which drastically decreases the page loading size from ~750kb ~10kb. All tests have been run on a LAN connection.