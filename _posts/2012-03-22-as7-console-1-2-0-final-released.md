---
title: AS7 Console 1.2.0.Final released
author: hbraun
layout: post
permalink: /2012/03/as7-console-1-2-0-final-released/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2012/03/as7-console-120final-released.html
dsq_thread_id:
  - 688882862
categories:
  - Uncategorized
---
<div>
  <b>Accessibility Improvements</b>
</div>

<div>
</div>

<div>
  In this iteration we&#8217;ve been concentrating on improving general usability and accessibility (<a href="http://www.section508.gov/">508 compliance</a>).
</div>

<div>
</div>

<div>
  The overall UI has been updated so that most elements are keyboard accessible and the core widgets (trees, tables, etc) can be navigated using the keyboard only. In addition to that, we&#8217;ve added <a href="http://www.w3.org/WAI/intro/aria">W3C Aria</a> landmarks, properties and state attributes.
</div>

<div>
</div>

<div>
  <b>Internet Explorer Updates</b>
</div>

<div>
</div>

<div>
  We&#8217;ve also fixed some nasty CSS bugs in IE8 and IE9 which caused the console to render without stylesheets being applied.</p>
</div>

<div>
  <b>All Issues</b>
</div>

<div>
  Here&#8217;s the complete list of issues that are included in<a href="https://issues.jboss.org/browse/AS7-4257"> 1.2.0.Final</a>: 
  
  <div style="font-size:11pt">
    <ul style="padding;2px;">
      <li>
        AS7-4255 Help Panels can not be closed on IE9
      </li>
      <li>
        AS7-4233 Interface editor doesn&#8217;t cancel operation upon click
      </li>
      <li>
        AS7-4231 Admin console: unable to remove security module if it has properties defined
      </li>
      <li>
        AS7-4227 Fix network interface management problems
      </li>
      <li>
        AS7-4164 Aria attributes on CellTables
      </li>
      <li>
        AS7-4106 Admin console &#8211; management of infinispan caches &#8211; unable to change attributes
      </li>
      <li>
        AS7-4045 Accessibility improvements: keyboard navigation and main aria attributes core widgets and overall layout
      </li>
      <li>
        AS7-3743 Sporadic IE 8&9 failure: stylesheets do not load
      </li>
      <li>
        AS7-4234 Timeout when uploading large deployment through the console
      </li>
      <li>
        AS7-4250 Failed to modify cache container transport settings
      </li>
      <li>
        AS7-4104 Admin console &#8211; Missing validation of infinispan resources&#8217; JNDI names
      </li>
      <li>
        AS7-3930, AS7-1779 Infinispan screens require descriptions
      </li>
    </ul>
    
    <div>
    </div>
    
    <p>
      </div> </div>