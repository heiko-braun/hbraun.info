---
title: Updated management console in Wildfly 8.2
subtitle: We’ve updated Wildfly Master to include the most recent 2.4.0 Final of the HAL management console.
author: hbraun
layout: post
permalink: /2014/10/updated-management-console-in-wildfly-8-2/
dsq_thread_id:
  - 3122396753
categories:
  - Wildfly
---
We&#8217;ve updated [Wildfly Master][1] to include the most recent 2.4.0 Final of the [HAL][2] management console.

The  improvements at a glance:

  * Updated look & feel. Now follows the [Patternfly][3] styles.
  * Improved information architecture: Domain management, deployments and runtime views have been relocated/consolidated
  * Extended/complete subsystem configuration: EE, [Undertow][4], Messaging, IO and Batch
  * Updated model browser: supports inline editing of resources
  * Log Viewer: Tail log files from within the console
  * Picketlink extension: The GUI now ships the [picketlink][5] management parts (enabled on demand)
  * Improved runtime monitoring: The charts and data tables have been cleaned up
  * Over 50 [bugfixes][6]

#### Updated visual appearance

The look and feel now builds on [Patternfly][3]. With more and more JBoss projects moving to patternfly, this will provide a more consistent look&feel across the portfolio.

[<img class="aligncenter size-medium wp-image-553" src="http://hbraun.info/wp-content/uploads/2014/10/patternfly-300x282.png" alt="patternfly" width="300" height="282" />][7]

#### Changes to the information architecture

We&#8217;ve moved things around a bit:

  * &#8216;Deployments&#8217; are a top level category in their own (used to be under &#8216;Runtime&#8217;)
  * &#8216;Domain Overview&#8217; moved to &#8216;Domain&#8217; (used to be under &#8216;Runtime&#8217; as well)

This allows to us to better address certain edge cases when configuring domains and has a clearer affordance when managing to specific server instances.

[<img class="aligncenter size-medium wp-image-555" src="http://hbraun.info/wp-content/uploads/2014/10/ia-300x214.png" alt="ia" width="300" height="214" />][8]

#### Extended Subsystem Support

The following subsystems have been revamped or completed:

  * EE
  * Undertow
  * Messaging
  * IO
  * Batch

Most of them have been either incomplete or missing and the new implementation provides access to the full subsystem configuration options.

#### New Model Browser

The model browser (Footer > Tools > Model Browser) has been completely revamped. It&#8217;s value/purpose has not been quiet clear in the past. I guess most people simply used to look up the management model documentation and get a general overview. However it now supports editing resources directly and a much better interaction and visual appearance.

[<img class="aligncenter size-medium wp-image-556" src="http://hbraun.info/wp-content/uploads/2014/10/model_browser-300x249.png" alt="model_browser" width="300" height="249" />][9]

On it&#8217;s own it might be used as a minimal GUI for Wildfly.Core at some point.

#### Ability to view logs form the console

Harald Pehl did a great job implementing this one with support from James Perkins. The log viewer (&#8216;Runtime&#8217; > &#8216;Platform&#8217; > &#8216;Log Viewer&#8217;) allows you to browse through or tail server logs. It&#8217;s a feature that&#8217;s been missing for a long time and I am happy to see it included in Wildfly 8.2. It will become especially useful when managing domains.

[<img class="aligncenter size-medium wp-image-557" src="http://hbraun.info/wp-content/uploads/2014/10/logviwer-300x213.png" alt="logviwer" width="300" height="213" />][10]

#### Picket Link Integration

The picket link management UI is now part of the default distribution. That means any Wildfly instance that uses the Picketlink subsystem can now be managed by default.

#### Improved runtime monitoring

The &#8216;Runtime&#8217; category has been revisited and cleaned up. We&#8217;ve added new attributes and improved those views that didn&#8217;t have a clear purpose.

#### Plenty of bug fixes

This release does include over 50 bugfixes spread across the whole UI. You might not have noticed all of them but this will certainly improve the overall user experience when working with the management console. Thanks to everybody reporting and fixing these issues.

&nbsp;

 [1]: https://github.com/wildfly/wildfly
 [2]: https://github.com/hal/core
 [3]: https://www.patternfly.org/
 [4]: http://undertow.io/
 [5]: http://picketlink.org/
 [6]: https://issues.jboss.org/issues/?filter=12322272
 [7]: http://hbraun.info/wp-content/uploads/2014/10/patternfly.png
 [8]: http://hbraun.info/wp-content/uploads/2014/10/ia.png
 [9]: http://hbraun.info/wp-content/uploads/2014/10/model_browser.png
 [10]: http://hbraun.info/wp-content/uploads/2014/10/logviwer.png