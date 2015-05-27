---
title: 'BPM console: springtime cleaning'
author: hbraun
layout: post
permalink: /2009/04/bpm-console-springtime-cleaning/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2009/04/bpm-console-springtime-cleaning.html
dsq_thread_id:
  - 896068567
categories:
  - Uncategorized
---
<div id="since">
  Since 4.0.0.Beta2
</div>

The BPM console is approaching Beta3 and it was about time to tidy up. We&#8217;d been running on gwt-ext from the beginning, because it was easy to get started with the project. But due to some [license changes][1] in the gwt-ext project, we&#8217;d been forced to abandon that approach and chose [gwt-mosaic][2] as it&#8217;s successor. Mosaic works like charm and will eventually evolve as the default library for any JBoss GWT console.   
<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://2.bp.blogspot.com/_QxIFVLQdHS0/SfA5PDDj-PI/AAAAAAAAADA/ZN2UN2CnCGo/s1600-h/Picture1.png"><img style="float:left; margin:0 10px 10px 0;cursor:pointer; cursor:hand;width: 320px; height: 198px;" src="http://2.bp.blogspot.com/_QxIFVLQdHS0/SfA5PDDj-PI/AAAAAAAAADA/ZN2UN2CnCGo/s320/Picture1.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5327821289860364530" /></a>  
<br clear="all" />  
**Plugin-API and workspace composition**  
We are still looking into unification that allows composition of management interfaces across JBoss project within a single console. The BPM console already follows that approach, which has been explained in a [previous blog post][3]. Besides some minor refactorings in the [plugin-api][4], the concept did basically remain the same: A workspace is assembled at build-time. Editors (workspace plugins) are retrieved from the classpath (maven dependencies) and configured through a workspace configuration:

*workspace-default.cfg*  


<pre><br />org.jboss.bpm.console.client.process.ProcessEditor<br />org.jboss.bpm.console.client.task.TaskEditor<br /><br /># not yet implemented in jBPM4<br />#org.jboss.bpm.console.client.report.ReportEditor  <br /></pre>

**Proper MVC design**  
If you got the chance to look into the previous codebase, you&#8217;d probably realized that the model and view components have been tightly intermingled. It was a result of the early UI prototypes that simply survived across releases. But with migration to mosaic, we decided to clean it up was well. The current implementation uses [mvc4g][5], a GWT ready implementation of the [HMVC pattern][6]. As a result the plugin-api does leverage that pattern by default:  
<br clear="all" />  
<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://1.bp.blogspot.com/_QxIFVLQdHS0/SfAxrsdgmnI/AAAAAAAAACw/9xEXnhrFcTg/s1600-h/v2_patterns.jpg"><img style="float:left; margin:0 10px 10px 0;cursor:pointer; cursor:hand;width: 320px; height: 252px;" src="http://1.bp.blogspot.com/_QxIFVLQdHS0/SfAxrsdgmnI/AAAAAAAAACw/9xEXnhrFcTg/s320/v2_patterns.jpg" border="0" alt=""id="BLOGGER_PHOTO_ID_5327812985918364274" /></a>

<br clear="all" />  
If you now look at the sources, you&#8217;ll find a clean and easy to understand separation of editors, actions and views:  
<br clear="all" />  
<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://4.bp.blogspot.com/_QxIFVLQdHS0/SfAzIG7pTYI/AAAAAAAAAC4/mG1RwmfXgL8/s1600-h/src-layout.png"><img style="float:left; margin:0 10px 10px 0;cursor:pointer; cursor:hand;width: 221px; height: 320px;" src="http://4.bp.blogspot.com/_QxIFVLQdHS0/SfAzIG7pTYI/AAAAAAAAAC4/mG1RwmfXgL8/s320/src-layout.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5327814573572050306" /></a>  
<br clear="all" />

**Improved error handling**  
One of the major complaints we received about previous console versions, was the fact that, sometimes it got stuck without any indication of what has been going wrong. With the latest refactorings, any HTTP request handling has been delegated to the core GWT RequestBuilder classes. This gives us more fine grained control, including request timeouts and http status codes as well as standardized error reporting.

**New look and feel**  
Mosaic is more close to the actual GWT sources and hence less fancy. But the actual Widgets are less error prone and do render faster then gwt-ext:

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://2.bp.blogspot.com/_QxIFVLQdHS0/SfA5PX9uQII/AAAAAAAAADQ/51dRG9z_iq0/s1600-h/Picture3.png"><img style="float:left; margin:0 10px 10px 0;cursor:pointer; cursor:hand;width: 320px; height: 114px;" src="http://2.bp.blogspot.com/_QxIFVLQdHS0/SfA5PX9uQII/AAAAAAAAADQ/51dRG9z_iq0/s320/Picture3.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5327821295473016962" /></a>  
<br clear="all" />  
Stay tuned. Now that we got the codebase in good shape for this summer, we&#8217;ll proceed with functional enhancements: Task forms and reporting.

Join the discussion in the [console dev forum][7].

 [1]: http://extjs.com/forum/showthread.php?t=33096
 [2]: http://code.google.com/p/gwt-mosaic/
 [3]: http://jboss-overlord.blogspot.com/2009/01/developing-bpm-console-plugins.html
 [4]: http://anonsvn.jboss.org/repos/jbpm/projects/gwt-console/trunk/plugin-api/src/main/java/org/jboss/bpm/console/client/
 [5]: http://code.google.com/p/mvc4g/
 [6]: http://code.google.com/p/mvc4g/wiki/HmvcWithMvc4g
 [7]: http://www.jboss.org/index.html?module=bb&#038;op=viewforum&#038;f=295