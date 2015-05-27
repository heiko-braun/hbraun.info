---
title: 'RFC: Process deployment use cases'
author: hbraun
layout: post
permalink: /2009/03/rfc-process-deployment-use-cases/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2009/03/rfc-process-deployment-use-cases.html
dsq_thread_id:
  - 1045260803
categories:
  - Uncategorized
---
This is a request for comments. 

<div id="since">
  Since 4.0.0.Beta1
</div>

  * What deployment use cases do we want to cover? 
      * What constraints should apply for each use case?</ul> 
        The matrix below shows the constraints for the deployment policies that are currently implemented:
        
        <a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://3.bp.blogspot.com/_QxIFVLQdHS0/SbeuSoy7sJI/AAAAAAAAACQ/QFBYBZeRYaE/s1600-h/deployment_use_cases.jpg"><img style="float:left; margin:0 10px 10px 0;cursor:pointer; cursor:hand;width: 320px; height: 224px;" src="http://3.bp.blogspot.com/_QxIFVLQdHS0/SbeuSoy7sJI/AAAAAAAAACQ/QFBYBZeRYaE/s320/deployment_use_cases.jpg" border="0" alt=""id="BLOGGER_PHOTO_ID_5311905920718712978" /></a>
        
        <br clear="all" />
        
        Explanation:
        
        There is currently four properties that are taken into consideration when processes get deployed:  
        the process name and version (part of jpdl.xml), the artifact name (i.e OrderProcess.par) and the artifact timestamp.  
        Process name, version and artifact name are the main properties that distinguish process deplyoments, the timestamp basically just acts as a fallback when no version is given and leads a version auto-increment.
        
        Possible combinations of those properties lead to matrix above.