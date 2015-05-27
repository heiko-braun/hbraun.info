---
title: 'JBoss AS7: Tackling the next generation OA&#038;M feature set'
author: hbraun
layout: post
permalink: /2012/08/jboss-as7-tackling-the-next-generation-oam-feature-set/
dsq_thread_id:
  - 811913684
categories:
  - User Experience
  - Wildfly
---
### Lock step development

So far the management tools we ship with AS7 did build on strict requirements. The development did mostly move lock step with the management API enhancements, which allowed us to build, verify and improve the management layer as whole (CLI, Web, API) on a topic by topic base. 

If a new feature has been added to the API it has been implemented and thus verified by both the CLI and the web interface at almost the same time. Once it was sufficiently provided by all clients we did move on to the next topic. 

This model has been very successful and did yield excellent results. The different stakeholders did not drift apart too far, questions could be answered immediately and changes be implemented in a timely manner. 

### Succinct development topics

Thinking about future enhancements to the AS7 management layer, I think this model should be retained. It can be enhanced by creating more succinct topics to focus on. Some ideas that came up in the past, but not limited to that:

  * Initial server setup and customisation: choice of modules, subsystems, etc 
  * Application setup: preparing the runtime dependencies (datasources, queues, ets) and differences across environments (development, staging, production) 
  * Day to day administrative tasks: system health, etc 
  * Cloud/Domain use cases: challenges when hosts cannot be accessed (log files, etc) 

Putting an emphasis on development topics would greatly simplify collaboration across teams: product management, development, QA, docs. It would allow us to get from a requirement to minimum viable feature (ready for UAT) in a short amount of time, without much context switching required by any participant. IMO this is one of the main points that allowed to deliver AS7 in such a short amount time.

### Enhancing the OA&M feature set

Although this model would make sense for other engineering areas as well, I would like to focus on the OA&M feature set of AS7. When comparing AS7 to other vendors offerings or talking to customers we end up with a plethora of features that could be provided. The key point however is to figure the important ones that will actually improve real user needs. 

Product management does already a great job of figuring out what that could actually be, but I think it does as well require engineering feedback, UX input and especially verification if the features provided actually serve the users needs. 

The topic based approach would be simple, but efficient way to provide new features and verify if they fit their purpose. 

### Iterations and change requests

I am writing this from the point of view of the web management interface. Being the last item in the development food chain (dependencies) and a very exposed one at the same time, this model makes perfect sense. However it might not be the case for everyone else. Hence I would like to outline what it takes to add new management features to the platform from our point view: 

  1. A management use case is identified and described 
  2. A subsystem provides the management API to enable the use case 
  3. The tools represent the use case according to their capabilities and context (interacting the API) 
  4. UAT verifies if it serves the user need (community, engineering, sales, product management) 

Typically the transition between each of these steps identifies several issues that need to be fixed before moving on. If this happens in a timely manner it&#8217;s no big deal. But if that gap between handover and feedback becomes to big, stakeholders working on the previous step are already focusing on something else. The iterations become bigger, the context switch more expensive and the overall result can be verified very late in the game, if at all.

### Value and usability

If we turn around the way of looking at product development, the actual users needs should matter most. It&#8217;s not the amount of features neither the question if the competition does provide it, that makes a product useful. The questions are:

  * Does the product provide value to the user? 
  * Can the users tasks easily be accomplished? 
  * How hard is it to start using it? 
  * Do people like to use it? 

I believe that an ordered, topic based approach to the development of new management features is crucial to the overall success. It will guarantee that not only we enhance the current feature set, but we also improve on it. 

With that in mind: Let&#8217;s figure out what&#8217;s important to you.