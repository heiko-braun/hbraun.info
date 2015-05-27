---
title: 'jBPM Task Management: A look at the participation model'
author: hbraun
layout: post
permalink: /2009/03/jbpm-task-management-a-look-at-the-participation-model/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2009/03/jbpm-task-management-look-at.html
dsq_thread_id:
  - 721385312
categories:
  - Uncategorized
---
<div id="since">
  Since 4.0.0.Beta1
</div>

The revisited task management model in jBPM introduces a new concept: task participation. The participation model describes identities (user or groups) and the type of involvement in the actual completion of task:

<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://2.bp.blogspot.com/_QxIFVLQdHS0/SdDNEjfRblI/AAAAAAAAACo/-WXy3CulUr0/s1600-h/participation.jpg"><img style="float:left; margin:0 10px 10px 0;cursor:pointer; cursor:hand;width: 320px; height: 306px;" src="http://2.bp.blogspot.com/_QxIFVLQdHS0/SdDNEjfRblI/AAAAAAAAACo/-WXy3CulUr0/s320/participation.jpg" border="0" alt=""id="BLOGGER_PHOTO_ID_5318976638054133330" /></a>

<br clear="all" />

<span style="font-weight:bold;">Example 1: User and business administrator participation</span>  
A common use case where this model fit&#8217;s quiet nicely is the distinction between a user that actually performs the task and a business administrator monitoring progress. Depending on the participation type some principals will actually do the work, while others make sure tasks are executed within given constraints (i.e. priority, duedate, etc).

<span style="font-weight:bold;">Example 2: Task stakeholders with different participation types</span>  
Another example could be stakeholders monitoring the actual outcome of task, or delegation between different participants that co-operate on a task. In this case a &#8220;initiator&#8221; of task, a &#8220;candidate&#8221; performing the work and the &#8220;final recepient&#8221; might be different participation types.

The TaskService API already reflects those changes:

<pre><br /><br />org.jbpm.TaskService <br />{<br />   [...]<br />/**<br />   * retrieves a list of tasks for a user<br />   * and a particular {@link org.jbpm.task.Participation} type<br />   *<br />   * @see org.jbpm.TaskQuery<br />   */<br />  List&lt;task> findTasksByParticipation(String participation, UserRef user);<br /><br />  /**<br />   * retrieves a list of tasks for a group<br />   * and a particular {@link org.jbpm.task.Participation} type<br />   *<br />   * @see org.jbpm.TaskQuery <br />   */<br />  List&lt;task> findTasksByParticipation(String participation, GroupRef... groups);<br />}<br /></pre>

Currently we ship some default participation types, out of which only type &#8216;candidate&#8217; is supported, but you can expect this to be extended in the near future. 

<pre><br />org.jbpm.task.Participation<br />{<br />   [...]<br /><br />  String CANDIDATE = "candidate";<br /><br />  IdentityRef getIdentityRef();<br />  <br />  /** see constants for default participations */<br />  String getType();<br />}<br /><br /></pre>

Stay tuned.