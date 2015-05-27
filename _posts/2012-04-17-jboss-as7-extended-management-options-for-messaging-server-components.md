---
title: 'JBoss AS7: Extended management options for messaging server components'
author: hbraun
layout: post
permalink: /2012/04/jboss-as7-extended-management-options-for-messaging-server-components/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2012/04/jboss-as7-extended-management-options.html
dsq_thread_id:
  - 677364433
categories:
  - Wildfly
---
We just finished a bunch of updates that complete the management options of the [hornetq server][1] components. With [7.1.2][2] you&#8217;ll get important management features that have been missing from the previous releases:

&#8211; [hornetq transports][3]  
&#8211; [connection factories][4]  
&#8211; [bridges, diverts, etc][5]

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://4.bp.blogspot.com/-p5Q8zPYuDDI/T41qsVKPd3I/AAAAAAAAAIg/Ies3QKr95GA/s1600/msg-acceptors.png"><img id="BLOGGER_PHOTO_ID_5732355210539399026" style="display: block; margin: 0px auto 10px; text-align: center; cursor: hand; width: 320px; height: 298px;" src="http://4.bp.blogspot.com/-p5Q8zPYuDDI/T41qsVKPd3I/AAAAAAAAAIg/Ies3QKr95GA/s320/msg-acceptors.png" alt="" border="0" /></a>

 [1]: http://www.jboss.org/hornetq
 [2]: https://issues.jboss.org/browse/AS7
 [3]: http://docs.jboss.org/hornetq/2.2.5.Final/user-manual/en/html/configuring-transports.html
 [4]: http://docs.jboss.org/hornetq/2.2.5.Final/user-manual/en/html/using-jms.html#using-jms.configure.factory.types
 [5]: http://docs.jboss.org/hornetq/2.2.5.Final/user-manual/en/html/jms-bridge.html