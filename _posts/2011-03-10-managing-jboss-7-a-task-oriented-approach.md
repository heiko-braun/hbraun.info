---
title: 'Managing JBoss 7: A task oriented approach'
author: hbraun
layout: post
permalink: /2011/03/managing-jboss-7-a-task-oriented-approach/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2011/03/managing-jboss-7-task-oriented-approach.html
dsq_thread_id:
  - 799498195
categories:
  - Wildfly
---
It&#8217;s been several weeks now, since we started working on the management web interface for JBoss 7. Time to outline some of the general ideas and concepts the console is build on. If you are not familiar with [domain management approach][1] that has been introduced in 7.0, you should [make yourself familiar with it][1] before reading any further.

Conceptually the domain model consists of three different levels, that we tried to reflect within the user interface: Configuration profiles, server groups and host specific settings.

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://1.bp.blogspot.com/-TbvOLFcDSqE/TXiRCyS_aOI/AAAAAAAAAAM/nScqY75VC9M/s1600/Screen%2Bshot%2B2011-03-10%2Bat%2B9.35.42%2BAM.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 88px;" src="http://1.bp.blogspot.com/-TbvOLFcDSqE/TXiRCyS_aOI/AAAAAAAAAAM/nScqY75VC9M/s320/Screen%2Bshot%2B2011-03-10%2Bat%2B9.35.42%2BAM.png" border="0" alt="" id="BLOGGER_PHOTO_ID_5582371215172921570" /></a>

If you think of these levels as being layered atop of each other, then <span style="font-style:italic;">Profiles</span> would be the bottom most configuration level that acts as a blueprint for the layers atop of it. <span style="font-style:italic;">Profiles</span> consist of subsystem specific settings (i.e. JCA, TX, etc) and are referenced by <span style="font-style:italic;">Server Groups</span>.

<span style="font-style:italic;">Server Groups</span> on the other hand specify configuration properties for a set of <span style="font-style:italic;">Servers</span> that run on different <span style="font-style:italic;">Hosts</span>.

A <span style="font-style:italic;">Host</span> is the top most and most detailed level. It runs <span style="font-style:italic;">Server Instances</span> that belong to a particular <span style="font-style:italic;">Server Group</span>.  
While there are numerous ways to organize the information accessible through the web interface, we used a few simple questions to guide our decisions: 

<div>
</div>

<div>
  - &#8220;What are the <b>primary tasks</b>?&#8221;
</div>

<div>
  - &#8220;At what <b>frequency</b> to these task occur?&#8221;
</div>

<div>
  - &#8220;What&#8217;s the <b>impact </b>on related configuration elements?&#8221;
</div>

<div>
</div>

<div>
  The primary tasks already seem to be represented by the different levels described above: Changes to and requests of host specific information is something we expect to occur quiet regularly. This does cover use cases like starting server instances and requesting runtime state information (i.e. metrics).
</div>

<div>
</div>

<div>
  Creation and modification of Server Groups will probably happen less often, except one specific use case, which is application deployment. Deployments are associated with server groups.
</div>

<div>
</div>

<div>
  The least likely changes are going to happen on the profile level. I.e the modification of a thread pool size is something you probably wont do very often.
</div>

<div>
</div>

The outermost categorization looks as follows:

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://3.bp.blogspot.com/-WVJNA08_d_M/TXi_oObcEjI/AAAAAAAAAAc/R6HFrtLzirg/s1600/task_groups.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 290px; height: 320px;" src="http://3.bp.blogspot.com/-WVJNA08_d_M/TXi_oObcEjI/AAAAAAAAAAc/R6HFrtLzirg/s320/task_groups.png" border="0" alt="" id="BLOGGER_PHOTO_ID_5582422435914584626" /></a> 

<div>
</div>

<div>
  Now while this coarse grained organization nicely groups the primary tasks and allows you to focus on the goal you want to achieve, it doesn&#8217;t give you any clues which configuration properties are inherited from lower levels. Some elements can be specified on a lower and be replaced on higher level (i.e. System Properties in profiles and server groups).
</div>

<div>
</div>

<div>
  This problem has two sides: On the one hand you need to know where an inherited property comes from in order to change it, on the other hand need to know what impact a modification might have on higher levels (Think of a JVM property on the profile level that impacts all server groups).
</div>

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://2.bp.blogspot.com/-CckLATLb7Pg/TXjM7Hj_EyI/AAAAAAAAAAk/BHfUP4cpJTk/s1600/impact.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 228px;" src="http://2.bp.blogspot.com/-CckLATLb7Pg/TXjM7Hj_EyI/AAAAAAAAAAk/BHfUP4cpJTk/s320/impact.png" border="0" alt="" id="BLOGGER_PHOTO_ID_5582437054140060450" /></a> 

<div>
</div>

<div>
  This problem isn&#8217;t solved yet. We are still working on visual distinction that allows you to clearly identify the source level of a configuration property and cross reference it accordingly. It might look like this:
</div>

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://1.bp.blogspot.com/-gf_hEACXjqU/TXjTUgq4ZmI/AAAAAAAAAAs/5QW6ScSTXTw/s1600/properties.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 92px;" src="http://1.bp.blogspot.com/-gf_hEACXjqU/TXjTUgq4ZmI/AAAAAAAAAAs/5QW6ScSTXTw/s320/properties.png" border="0" alt="" id="BLOGGER_PHOTO_ID_5582444087446365794" /></a> 

<div>
  <b>Call for participation</b> 
  
  <div>
    There are plenty of other related topics that we can talk about, but that&#8217;s it for today. If you want to participate, I would suggest you take a look at the following resources and let us know to what degree the suggested categorization makes sense.
  </div>
  
  <div>
  </div>
  
  <div>
    - <a href="https://community.jboss.org/wiki/DomainManagementModelDesign">DomainManagementModelDesign</a>
  </div>
  
  <div>
    <a href="https://community.jboss.org/wiki/DomainManagementModelDesign"></a>- <a href="https://github.com/jbossas/jboss-as/blob/master/controller/src/main/resources/schema/jboss_7_0.xsd">jboss_7_0 schema</a>
  </div>
  
  <div>
  </div>
  
  <div>
    <a href="https://github.com/jbossas/jboss-as/blob/master/controller/src/main/resources/schema/jboss_7_0.xsd"></a>Stay tuned, we keep you posted.
  </div>
  
  <div>
  </div>
</div>

 [1]: https://community.jboss.org/wiki/DomainManagementModelDesign