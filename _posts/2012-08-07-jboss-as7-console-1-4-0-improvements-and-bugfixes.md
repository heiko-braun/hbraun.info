---
title: 'JBoss AS7 Console 1.4.0: Improvements and bugfixes'
author: hbraun
layout: post
permalink: /2012/08/jboss-as7-console-1-4-0-improvements-and-bugfixes/
dsq_thread_id:
  - 796063025
categories:
  - Wildfly
---
We just released an updated version of the [AS7 console][1]. Besides several [bug fixes and minor improvements][2] this release also contains a number of notable changes that I would like to outline in this post.

## Revamped deployments in domain mode

We&#8217;ve been getting a lot of requests for enhancement from the community. Hence we took some time to revisit the domain deployment use cases within the console.

They basically boil down to two approaches:

&#8211; Managing the contents in the repository  
&#8211; Assigning deployments to server groups

While the former has been provided in a reasonable way, the later has been really awkward to use. With the new user interface you can now chose to approach deployments from either the content repository or a server group. In both cases you&#8217;ll find the ability to assign and remove deployments to and from server groups.

Atop of that we&#8217;ve added some filename filters that should greatly simplify working with a large set of deployments.

[<img class="aligncenter size-medium wp-image-212" title="Domain Deployments" src="/wp-content/uploads/2012/08/Screen-Shot-2012-08-07-at-1.50.42-PM-300x243.png" alt="" width="300" height="243" />][3]

## Configuration Browser

The configuration browser is the first all purpose tool we are throwing into the mix. It allows you to browse the actual model descriptions easily (learning purposes) and to inspect actual configuration values of node within the tree. We had this pending for quiet some time and it can be considered a first step towards something like an expert mode within the console (imagine forms being added). But we think it&#8217;s valuable on it&#8217;s own, hence we added it to 1.4.0.

[<img class="aligncenter size-medium wp-image-215" title="Configuration Browser" src="/wp-content/uploads/2012/08/Screen-Shot-2012-08-07-at-1.55.54-PM-300x243.png" alt="" width="300" height="243" />][4]

&nbsp;

## Expression Resolver

We&#8217;ve had support for [expression values][5] as part of the model for quiet some time, but the ability to resolve the actual values has been missing so far. To complement expression support we&#8217;ve added a tool that allows you to resolve expressions from within the console.

[<img class="aligncenter size-medium wp-image-227" title="Expression Values" src="/wp-content/uploads/2012/08/expression_value-300x100.png" alt="" width="300" height="100" />][6]

It&#8217;s opened directly from attributes that carry expression values (i.e. &#8220;${tx.node:1}&#8221;) and will automatically resolve values on all servers (in case you are running domain mode).

[<img class="aligncenter size-medium wp-image-228" title="Expression Resolver" src="/wp-content/uploads/2012/08/resolved-300x238.png" alt="" width="300" height="238" />][7]

 [1]: https://github.com/jbossas/console
 [2]: https://github.com/jbossas/console/wiki/1.4.0-Release-Notes
 [3]: /wp-content/uploads/2012/08/Screen-Shot-2012-08-07-at-1.50.42-PM.png
 [4]: /wp-content/uploads/2012/08/Screen-Shot-2012-08-07-at-1.55.54-PM.png
 [5]: https://docs.jboss.org/author/display/AS71/Expressions
 [6]: /wp-content/uploads/2012/08/expression_value.png
 [7]: /wp-content/uploads/2012/08/resolved.png