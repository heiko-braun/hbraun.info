---
title: Bela Ban at JBUG Munich, 08.03.2010
author: hbraun
layout: post
permalink: /2010/03/bela-ban-at-jbug-munich-08-03-2010/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2010/03/bela-ban-at-jbug-munich-08032010.html
categories:
  - Uncategorized
---
Bela talks about ReplCache:

<span style="font-weight:bold;">Memory is the new disk, disk is the new tape</span>

ReplCache is a tool to store data in a cluster. It is essentially a hashmap spanning multiple hosts in a cluster.

There are put(), get() and remove() methods which distribute data over the cluster.

The unique feature of ReplCache is that it allows to define a replication count per element, e.g. how many times should an element be stored (on different nodes) for redundancy. When the cluster changes, e.g. due tonew nodes joining or nodes crashing, elements are automatically rebalanced to satisfy replication counts.

Given enough nodes and the assumption that not all nodes ever crash at the exact same time, we can get rid of our database, and use the aggregated memory as our large virtual memory-based database!

(For the paranoid folks, we can still stream the data away to disk/DB).

We will also discuss the architectural approach for applications leveraging ReplCache and which for which kind of application this architecture will be suitable.

[Details can be found here][1]

 [1]: http://www.jbug-munich.org/