---
title: 'JBoss 7 Web Console: 1.0.0.Beta3'
author: hbraun
layout: post
permalink: /2011/03/jboss-7-web-console-1-0-0-beta3/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2011/03/jboss-7-web-console-100beta3.html
dsq_thread_id:
  - 857002158
categories:
  - Wildfly
---
<div>
</div>

<div>
</div>

<div>
  Beta3 is the version that will be shipped with <a href="http://www.jboss.org/jbossas/downloads">JBoss 7.0.0.Beta2</a> end of this week.
</div>

<div>
  <span class="Apple-style-span"   style="  -webkit-border-horizontal-spacing: 2px; -webkit-border-vertical-spacing: 2px; font-family:tahoma, verdana, sans-serif;font-size:12px;"><br /> 
  
  <h2>
    1.0.0.Beta3 Release Notes
  </h2></p> 
  
  <h3>
    Functional scope
  </h3>
  
  <p>
    Most of the work in this release has been done on the framework level, creating re-usable components that are needed to implement the remaining management use cases: 
    
    <ul>
      <li>
        Form databinding & validation
      </li>
      <li>
        Integration with the domain controller
      </li>
      <li>
        General UI framework (MVP)
      </li>
    </ul>
    
    <p>
      Functionally this release does focus on the outermost domain management use cases, that act as POC for the building blocks listed above. 
      
      <ul>
        <li>
          Start/Stop server instances
        </li>
        <li>
          Create server groups and server configurations
        </li>
        <li>
          Configure server groups and configurations
        </li>
      </ul>
      
      <p>
        The standalone server Web UI doesn&#8217;t contain any reasonable functionality at this point.
      </p>
      
      <p>
        The work on management use cases that relate to subsystems has not begun yet. There are merely two examples (Datasource and JMS) that act as a preview and should give you an idea where things are going.
      </p>
    </p>
    
    <h3>
      Browser compatibility
    </h3>
    
    <p>
      This release has been tested on Chrome, Firefox and Safari. Internet Explorer has not been verified yet, but we don&#8217;t expect it to work properly in releases before IE8.
    </p>
    
    <h3>
      Feedback
    </h3>
    
    <p>
      Your feedback is greatly appreciated. Tell us what you think about the current way the content is organized within the UI. Identify the top three things that don&#8217;t make sense to you or that you couldn&#8217;t find easily in the console. Send these issues to: 
      
      <ul>
        <li>
          <a href="https://lists.jboss.org/mailman/listinfo/jboss-as7-dev">jboss-as7-dev@lists.jboss.org</a>
        </li>
      </ul>
      
      <p>
        In case you run into a bug, don&#8217;t hesitate and file an issue here: (<i>Don&#8217;t forget to include your OS/Browser description</i>) 
        
        <ul>
          <li>
            <a href="https://issues.jboss.org/browse/JBAS">https://issues.jboss.org/browse/JBAS</a> (JBoss 7, Component &#8220;Web Console&#8221;)
          </li>
        </ul>
        
        <p>
          </span></div>