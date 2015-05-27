---
title: Web console architecture, future directions
author: hbraun
layout: post
permalink: /2012/09/web-console-architecture-future-directions/
dsq_thread_id:
  - 843466417
categories:
  - GWT
  - User Experience
  - Wildfly
---
With the monkey of our back it&#8217;s time to revisit some of the decisions that lead to the current console architecture and implementation. I would like to outline some of the challenges that lie ahead of us and provide entry points for subsequent discussions. 

[toc]

## Point of view

### Adding new functionality

On the road to 7.1 we had to make some sacrifices in terms of extensibility and the ability to adopt to core management configuration changes and enhancements. 

The DMR model wasn&#8217;t mature enough to fully rely on the meta data to generate UI components and the overall use cases and applicability wasn&#8217;t clear.

Since 7.1 we pretty much know what UI paradigms we need, the DMR schema is stable enough and we&#8217;ve collected a list of best practices how to work with the data at hand.

While I am still not convinced we should strive for a 1:1 mapping (auto magic) of the existing configuration schema and the UI, there is certainly room for improvement. We might reach a level of automation that allows us to more easily add extensions to the console, but there will always be the need for customisation and the ability to provide more advanced use cases manually.

I&#8217;ll outline possible approaches below, but first I would like to introduce some perspectives to look at the problem.

### Layered products

I do expect the majority of extended functionality within the console will be derived from requirements of layered products. Switchyard and Teiid are good examples as they already integrate with the core platform and the embedded console.

Integration covers providing subsystem extensions, customisation of the core server components and providing custom UI&#8217;s that are embedded within the console and JON.

### UX consistency

Consistent user experience is one of our main goals. Not only when moving between products, but also when switching from the embedded console to JON.

This involves UI paradigms, core interaction patterns and the look&feel. 

To certain degree we expect differences in the UI. They exist due to different value propositions and target audiences. But the overall impression should be that these tools are from the same company. 

Shared UI components and libraries would simplify the job, but style guides and UX reviews would be an alternative to reach consistency.

### Task based UI

Along the same conceptual lines and worth mentioning here are advanced use cases that we typically refer to as &#8220;task based UI&#8217;s&#8221;. A task in this sense is a sequence of management operations to reach a certain goal. 

Good examples are customised day-day management activities like checking the state of a certain runtime service. Or a company specific application setup that follows a certain order. The list of possible options is not restricted. 

Task are named and persisted. They are parametrized and provide a skeleton for subsequent executions.

Tasks can be represented in a wizard like fashion or aggregated on a kind of dashboard. 

We envision a repository of tasks, that will be pre-populated by descriptions that JBoss provides. But with the help of our community it can evolve to much bigger ecosystem. Similar to the growing number of CLI scripts that exist out there.

## Commonalities

So what do all these things have in common? 

  * They would benefit from the ability to generate the UI 
  * They deal with the question of modularity and composition 

If done well, a proper design could enable all of these aspects, eventually even layering atop of each other. 

An abstract model is required to describe the tasks. But it could also be used to specify extensions. 

We already carry a lot of usable meta data, but layout properties like spatial location, grouping of attributes, correlation of resources, etc are not given. This would need to be mixed in. 

Generation of the UI can easily enforce UX constraints and emphasise certain paradigms. But don&#8217;t expect it to be the silver bullet. It will nail down the modelling of uses cases to a fixed set of traits. 

Extension points for layered products are very likely to follow the same rules. Are they any different from tasks as described above? 

## Architectural choices

We do currently see two reasonable architectural approaches. 

### GWT Composition

That&#8217;s the model we currently use. It&#8217;s a build time extension mechanism that allows you to implement and provide UI extensions which are assembled at compile time. 

It&#8217;s a bare bone, lowest common denominator approach that provides the freedom to implement extension UI&#8217;s by arbitrary means. We ship a set of default components and building blocks, but the plumbing has to be done manually.

It&#8217;s currently used by Switchyard and Teiid to integrate with the AS7 console.

### Plugin descriptors

Based on an abstract model. Extensions are described by a fixed schema. This covers resource addresses, attribute meta data and layout properties. The magic UI kernel generates and embeds it into the interface.

Similar to JON plugin descriptors. Can provide a JON upstream if done properly. Upstream means reusing UI&#8217;s within JON. Thus both projects may eventually share interfaces that interact with the AS7 management layer.

Compared to the GWT composition, this puts the most constraints on extension points. But it will probably scale better. Especially considering the number of projects we have.

### Runtime extensions

Both architectures above can eventually be used to enable runtime extensions. This means dropping a Jar into a directory and restarting the server to extend the console. 

The plugin descriptor is very likely going to support this model, but the GWT composition requires further research. 

It basically means two distinct GWT compilations are served within the same host HTML page. We are currently prototyping this approach. 

## Get the ball rolling

We&#8217;d very much appreciate your feedback. AS8 is about to be planned. This should be a starting point for discussions around the future design and improvements of the embedded console. 

Let&#8217;s keep it high level and dive into the technical details once we&#8217;ve figured out the overall goals.