---
title: Business Process Analytics using BPAF
author: hbraun
layout: post
permalink: /2010/03/business-process-analytics-using-bpaf/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2010/03/business-process-analytics-using-bpaf.html
dsq_thread_id:
  - 812124006
categories:
  - BAM
  - BPM
  - GWT
---
Over last 6 month I&#8217;ve been working on several components that will be assembled to a bigger business activity monitoring solution. I started off with a CEP based activity monitor (SAM) that allows for advanced correlation across heterogeneous event sources. After that I&#8217;ve spent some time integrating the BIRT reporting runtime with the BPM console, which allows you to run complex reports on process-related audit data. Only to realize that I&#8217;ve started on the wrong foot.

**Process analytics bottom to top**

I made a mistake to begin with the most complex components first, without realizing that the key to a successful BAM solution is underlying data model. Without a solid baseline the creation of report templates becomes a daunting task because the missing unification of audit data basically requires you to customize the report algorithms for any instrumented subsystem. Creating rules for the CEP component that fire when certain SLA&#8217;s are breached doesn&#8217;t get more simple either, when working on a heterogeneous event model.

I finally spend some time prototyping around an idea that has been in the wild for quiet some time: Baseline process-related audit data on [BPAF][1]: A WFMC standard that describes a data structure that enables the aggregation and correlation of audit data across multiple platforms. 

In the following sections I would like to walk through [a simple protoype][2], that already shows the benefits of this approach. It is really impressive how little code it requires to deliver a solution that already matches an important number of the use cases.

**Data model, storage and retrieval**

To begin with an implementation for storing and querying BPAF event data was needed. Fortunately JAXB and Hibernate made this a trivial task:

<pre><br />@XmlAccessorType(XmlAccessType.FIELD)<br />@XmlType(name = "", propOrder = {<br />    "eventDetails",<br />    "dataElement"<br />})<br />@XmlRootElement(name = "Event")<br />@Entity<br />@Table(name="BPAF_EVENT")<br />public class Event {<br /><br />  @XmlElement(name = "EventDetails", required = true)<br />  protected Event.EventDetails eventDetails;<br /><br />  @XmlElement(name = "DataElement")<br />  protected List&lt;tuple> dataElement;<br /><br />  /**<br />   * A globally unique identifier for the individual event<br />   */<br />  @XmlAttribute(name = "EventID", required = true)  <br />  protected long eventID;<br /><br />[...]<br /><br />}<br /></pre>

The [current implementation][3] allows two approaches for querying the BPAF data: Either leverage the default model and it&#8217;s persistence implementation, or adopt a proprietary audit data structure to the BPAF model when needed. For later use case the API fo querying is split from the default data model:

<pre><br />/**<br /> * @author: Heiko Braun &lt;hbraun@redhat.com><br /> * @date: Mar 10, 2010<br /> */<br />public interface BPAFDataSource<br />{<br />  /**<br />   * Get a list of distinct process definition ID's that are known to the system.<br />   * @return a collection of process definition ID's<br />   */<br />  List&lt;string> getProcessDefinitions();<br /><br />  /**<br />   * Get a list of distinct process instance ID's that are known to the system.<br />   * @return a collection of process instance ID's<br />   */<br /><br />  List&lt;string> getProcessInstances(String processDefinition);<br /><br />  /**<br />   * Get a list of distinct activity definition ID's that are known to the system.<br />   * @return a collection of activity definition ID's<br />   */<br /><br />  List&lt;string> getActivityDefinitions(String processInstance);<br /><br />[...]<br />}<br /></pre>

Now that we have components in place for storing and querying raw BPAF data, let&#8217;s move on to a more interesting topic: How to make sense of it. 

**Turning data into information**

The whole purpose of this exercise is to provide a way to gain insights about the execution characteristics of the processes that drive your business. While BPAF itself is a compact but still very expressive format (BPAF State Model) to store process-related audit data, it requires additional steps to turn it into consumable information that participants and decision makers can make sense of.

For the sake of this example we&#8217;ve added some algorithms that allow grouping and sorting of the underlying data, which will be used by the presentation layer.

Let&#8217;s take a look at the prototype UI ([yet another BPM Console plugin][4]) and see how much information can already be derived without going through hoops and loops.

**Presenting audit data to decision makers**

The prototype UI demos a simple use case: &#8220;How did the processes execute in the past?&#8221; Although a simple question, it already implies a lot of fine grained functionality a user might expect:

  * Selecting a relevant process 
      * Restricting the query to a certain time period 
          * Scrolling through business related events that occurred over a period of time 
              * Zooming in and out on a time scale (hourly, daily, weekly, etc)</ul> 
                <a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://4.bp.blogspot.com/_QxIFVLQdHS0/S7OiMl80QWI/AAAAAAAAAGQ/s39x43bWrs4/s1600/fullscreen.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 295px;" src="http://4.bp.blogspot.com/_QxIFVLQdHS0/S7OiMl80QWI/AAAAAAAAAGQ/s39x43bWrs4/s320/fullscreen.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5454881910905127266" /></a>
                
                **Concepts represented by the prototype UI**
                
                For the sake of simplicity the current implementation (at the time of this writing) is limited in functionality. Nevertheless I would like to walk you through the current features and explain some of the key concepts.
                
                To begin with a user selects the <tt>Process Defintion</tt> and the relevant time period:
                
                <a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://1.bp.blogspot.com/_QxIFVLQdHS0/S7Ojxoj9e6I/AAAAAAAAAGY/5jVluEQOuUw/s1600/process_selection.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 294px; height: 137px;" src="http://1.bp.blogspot.com/_QxIFVLQdHS0/S7Ojxoj9e6I/AAAAAAAAAGY/5jVluEQOuUw/s320/process_selection.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5454883646772968354" /></a>  
                <a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://3.bp.blogspot.com/_QxIFVLQdHS0/S7Ojx3k65XI/AAAAAAAAAGg/74ZnmgejsmA/s1600/timeperiod.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 264px; height: 110px;" src="http://3.bp.blogspot.com/_QxIFVLQdHS0/S7Ojx3k65XI/AAAAAAAAAGg/74ZnmgejsmA/s320/timeperiod.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5454883650803524978" /></a>
                
                The time period offers a set of commonly used intervals, like &#8220;Last Week&#8221;, &#8220;Last Quarter&#8221; or &#8220;Last 24 Hours&#8221;.
                
                The BPAF data is loaded and grouped according to the time period and presented in an interactive chart:
                
                <a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://4.bp.blogspot.com/_QxIFVLQdHS0/S7Okx0Tj3aI/AAAAAAAAAGw/40A6uPt9t7w/s1600/chrono1.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 206px;" src="http://4.bp.blogspot.com/_QxIFVLQdHS0/S7Okx0Tj3aI/AAAAAAAAAGw/40A6uPt9t7w/s320/chrono1.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5454884749437033890" /></a>  
                <a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://3.bp.blogspot.com/_QxIFVLQdHS0/S7Okxsf_o_I/AAAAAAAAAGo/06F4A5G0qBk/s1600/chrono2.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 252px;" src="http://3.bp.blogspot.com/_QxIFVLQdHS0/S7Okxsf_o_I/AAAAAAAAAGo/06F4A5G0qBk/s320/chrono2.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5454884747341702130" /></a>
                
                The charts allow you to zoom in on the time scale (i.e. &#8220;1 day, 5 day, max&#8221;) and scroll through the event data on each level.  
                (Shout-Outs to [the chronoscope project][5])
                
                You can comment on the information and create markers on business relevant points that either require clarification or otherwise mark notable changes in the execution of a process:
                
                <a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://3.bp.blogspot.com/_QxIFVLQdHS0/S7OmGBz98KI/AAAAAAAAAHA/kJoesWMhUi8/s1600/comment_create.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 63px;" src="http://3.bp.blogspot.com/_QxIFVLQdHS0/S7OmGBz98KI/AAAAAAAAAHA/kJoesWMhUi8/s320/comment_create.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5454886196171632802" /></a>  
                <a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://1.bp.blogspot.com/_QxIFVLQdHS0/S7OmFtYpD4I/AAAAAAAAAG4/fkNhm0oW34s/s1600/markers.png"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 286px; height: 320px;" src="http://1.bp.blogspot.com/_QxIFVLQdHS0/S7OmFtYpD4I/AAAAAAAAAG4/fkNhm0oW34s/s320/markers.png" border="0" alt=""id="BLOGGER_PHOTO_ID_5454886190688309122" /></a>
                
                **Conclusion and next steps**
                
                As you see, this simple prototype already covers important features that you would expect from such an implementation.  
                And we didn&#8217;t yet touch sophisticated topics like comparison of process executions or creation of key performance indicators that trigger notifications (do the markers ring a bell?). 
                
                In the next few month you can expect this approach to be married to SAM, our CEP based BAM component that allows correlation and execution on process activities close to real time.
                
                Stay tuned, now that we have a common baseline for representing and querying process-related audit data we&#8217;ll look into more advanced topics.

 [1]: http://www.bpm-research.com/wp-content/uploads/2009/02/2009-02-20-wfmc-tc-1015-business-process-analytics-format-r1.pdf
 [2]: http://anonsvn.jboss.org/repos/soag/activity-monitor/trunk/
 [3]: http://anonsvn.jboss.org/repos/soag/activity-monitor/trunk/model/
 [4]: http://www.jboss.org/errai/ErraiWorkspaces
 [5]: http://timepedia.org/chronoscope/