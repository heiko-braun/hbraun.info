---
title: 'JBoss AS7: Web Console 1.0.Final released'
author: hbraun
layout: post
permalink: /2012/02/jboss-as7-web-console-1-0-final-released/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2012/02/jboss-as7-web-console-10final-released.html
dsq_thread_id:
  - 685411100
categories:
  - Wildfly
---
After several month of work, we are very happy to announce the first final release of the JBoss AS 7 web management interface. It ships with [AS 7.1][1] and covers the following management use cases:

<span style="font-weight:bold;">Subsystem Management</span>

About **80% of the subsystems** are currently manageable through the console: 

<div>
  <div>
    <ul>
      <li>
        configadmin
      </li>
      <li>
        datasources
      </li>
      <li>
        deployment-scanner
      </li>
      <li>
        ee
      </li>
      <li>
        ejb3
      </li>
      <li>
        jacorb
      </li>
      <li>
        jca
      </li>
      <li>
        jmx
      </li>
      <li>
        jpa
      </li>
      <li>
        logging
      </li>
      <li>
        messaging
      </li>
      <li>
        naming
      </li>
      <li>
        osgi
      </li>
      <li>
        resource-adapters
      </li>
      <li>
        sar
      </li>
      <li>
        security
      </li>
      <li>
        threads
      </li>
      <li>
        transactions
      </li>
      <li>
        web
      </li>
      <li>
        webservices
      </li>
    </ul>
  </div>
  
  <p>
    </div> 
    
    <div>
      In the next few weeks we are going to provide the remaining ones: infinispan, mail, groups and mod cluster.
    </div>
    
    <div>
    </div>
    
    <div>
      <b>General Use Cases</b>
    </div>
    
    <div>
      <b><br /></b>
    </div>
    
    <div>
      Besides the subsystem configuration, the current web management interfaces allow you to carry out the following operations:
    </div>
    
    <div>
    </div>
    
    <div>
      - Full Domain Management (server groups, server configurations and hosts)
    </div>
    
    <div>
      - Manage Deployments (both across domains and standalone servers)
    </div>
    
    <div>
      - Configure socket bindings, network interfaces, JVM parameters and system properties
    </div>
    
    <div>
    </div>
    
    <div>
      <b>Runtime Status</b>
    </div>
    
    <div>
      <b><br /></b>
    </div>
    
    <div>
      Version 1.0 also provides you with the ability to quickly check the system health:
    </div>
    
    <div>
    </div>
    
    <div>
      - JVM Status (heap, threads, etc)
    </div>
    
    <div>
      - Transaction Manager (i.e. commit/rollback ratios)
    </div>
    
    <div>
      - Datasource usage (pools sizes, etc)
    </div>
    
    <div>
      - Web statistics (i.e. request/error count)
    </div>
    
    <div>
      - JMS metrics (topic/queue sizes, etc)
    </div>
    
    <div>
      - Persistence Units (cache usage, queries, etc)
    </div>
    
    <div>
    </div>
    
    <div>
      <b>Improved Look&Feel</b>
    </div>
    
    <div>
      <b><br /></b>
    </div>
    
    <div>
      We&#8217;ve put a lot of effort into the overall look&feel and tried to come up with a design that&#8217;s suitable for the job without getting in your way when you use it on day to day basis:
    </div>
    
    <p>
      <div>
        <a href="http://4.bp.blogspot.com/-_DBj3ZOCPpo/Tzt7YWyZaVI/AAAAAAAAAHo/1I1wJ8JVG8o/s1600/console_1.0.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 287px;" src="http://4.bp.blogspot.com/-_DBj3ZOCPpo/Tzt7YWyZaVI/AAAAAAAAAHo/1I1wJ8JVG8o/s320/console_1.0.png" border="0" alt="" id="BLOGGER_PHOTO_ID_5709292610986273106" /></a>
      </div>
      
      <div>
        <b>Contributors</b>
      </div>
      
      <div>
        <b><br /></b>
      </div>
      
      <div>
        Thanks to all the people that did help make it happen. Some people deserve special mentioning for their continuous support and contributions.
      </div>
      
      <div>
      </div>
      
      <div>
        - Stan Silvert
      </div>
      
      <div>
        - David Bosschaert
      </div>
      
      <div>
        - Pavel Slegr
      </div>
      
      <div>
        - Jan Martiska
      </div>
      
      <div>
        - James Cobb
      </div>
      
      <div>
        <span class="Apple-style-span"   style="  ;font-family:Helvetica;font-size:medium;"><br /></span>
      </div>
      
      <p>
        <b>What&#8217;s coming next?</b> 
        
        <div>
          <b><br /></b>
        </div>
        
        <div>
          We&#8217;ll keep improving and extending the web management interface. There are plenty of goodies on the roadmap:
        </div>
        
        <div>
        </div>
        
        <div>
          - Additional subsystems (infinispan, mail, jgroups, modcluster)
        </div>
        
        <div>
          - Management operation plans (store, load & execute complex management tasks)
        </div>
        
        <div>
          - Simplified clustering configuration
        </div>
        
        <div>
          - Additional metrics and statistics
        </div>
        
        <div>
        </div>
        
        <div>
          <b>Tell us what you think</b>
        </div>
        
        <div>
          <b><br /></b>
        </div>
        
        <div>
          If things don&#8217;t work as expected or you think certain functionality is missing, please drop us a note. Your feedback is important to us. The AS7 mailing list would be a good starting point:
        </div>
        
        <div>
        </div>
        
        <div>
          - <a href="https://lists.jboss.org/mailman/listinfo/jboss-as7-dev">https://lists.jboss.org/mailman/listinfo/jboss-as7-dev</a>
        </div>
        
        <div>
        </div>
        
        <div>
        </div>
        
        <div>
          Stay tuned, Heiko.</p>
        </div>

 [1]: http://www.jboss.org/jbossas/downloads/