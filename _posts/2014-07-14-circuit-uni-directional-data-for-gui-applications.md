---
title: 'Circuit: Uni-directional data flow model for GUI applications'
subtitle: Uni-directional data flow model for GUI applications.
author: hbraun
layout: post
permalink: /2014/07/circuit-uni-directional-data-for-gui-applications/
header-img: 'wp-content/uploads/2014/07/circuit.png'
dsq_thread_id:
  - 2842537343
categories:
  - GWT
  - Wildfly
---
[Circuit][1] provides an uni-directional data flow model for GUI applications. It&#8217;s intended to be used with GWT, but can be leveraged in any Java GUI framework. 

It resembles the ideas of the [Flux Architecture][2] that can be found in the [React.js][3] framework, but adds certain semantics to the data flow model.

For a general introduction and problem statement we&#8217;d recommend to look at the Flux documentation first. The specifics of the Circuit implementation will be explained in the following sections.

## <a class="anchor" href="#core-components" name="user-content-core-components"></a>Core Components

### <a class="anchor" href="#data-flow-model" name="user-content-data-flow-model"></a>Data Flow Model

View components (presenters in this case) dispatch actions through central dispatcher. The dispatcher coordinates the processing of actions across stores. Stores process the data or state change associated with an action and emit change events once they are done. Interested parties (presenters) read the data of the store and update the views accordingly.

[<img src="http://hbraun.info/wp-content/uploads/2014/07/circuit-300x227.png" alt="circuit data flow" class="aligncenter size-large wp-image-510" />][4]

### <a class="anchor" href="#actions" name="user-content-actions"></a>Actions

Actions represent behaviour, data and state within an application. They signal state changes to the dispatcher, which in turn coordinates the processing of actions across stores.

Actions are most often initiated from user interaction, but they are not limited to that. It&#8217;s also possible that the underlying framework or the service backend creates and dispatches actions.

### <a class="anchor" href="#dispatcher" name="user-content-dispatcher"></a>Dispatcher

The dispatcher acts as a central hub for processing actions. Any action passes through the dispatcher and the dispatcher delegates it to the Stores, that do ultimately process the Action.

The Dispatchers main responsibility is to coordinate the processing of Actions across Stores.

### <a class="anchor" href="#stores" name="user-content-stores"></a>Stores

Stores keep the application state and act as proxies to the data model used by an application. Most often stores interact with service backends to read and modify a persistent data model, which they in turn expose in a read-only fashion to the actual view (or presenter-view tuples in MVP).

Stores are registered with the Dispatcher for Actions they are interested in. They can directly rely on the data passed with an Action, or listen for state changes in other parts of the data model.

Stores do emit Change Events to interested parties that rely on the data or state managed by a particular Store.

### <a class="anchor" href="#presenter-as-in-mvp" name="user-content-presenter-as-in-mvp"></a>Presenter (as in MVP)

The Presenter (or presenter-view tuple as in MVP) creates and dispatches Actions. This happens on behalf of a user interaction, due to framework events or another signal from the service backend.

Presenters listen to Store Change Events and in turn read data from Stores and update the views accordingly.

Presenters do only have read-only access to Stores and the data they maintain. Any modification to the data or state of an application has to be driven by Actions.

## <a class="anchor" href="#processing-semantics" name="user-content-processing-semantics"></a>Processing Semantics

One of the core problems Circuit addresses are cascading effects of event based applications.

In a typical GUI application an event triggers some business logic, model update or state change, most often as a result of user interaction. Events can trigger other events, which leads to unpredictable data flow, hard to diagnose problems and unclear application semantics.

The guiding principal in Circuit (and Flux) is provide a framework with deterministic behaviour that allows you to hook into the data flow at any point and know exactly what steps will executed next.

The uni-directional data flow described above already provides a good baseline, but Circuit adds some specific semantics to the contract between the core components, which will be described in the next sections.

### <a class="anchor" href="#action-sequences" name="user-content-action-sequences"></a>Action Sequences

Any Action flows through the Dispatcher and the dispatcher coordinates how the Stores process the actions. In Circuit we use a sequencing dispatcher, that ensures only one Action will be processed at a time.

If two Actions are dispatched simultaneously the later one will be queued. All Stores that are registered for a particular Action type will process the Action and once the group completes the next Action will be taken of the queue.

This way Actions don&#8217;t create race conditions when updating the state or data of an application.

### <a class="anchor" href="#store-interdependencies" name="user-content-store-interdependencies"></a>Store Interdependencies

Typically a single Store maintains a particular segment of the data or domain model in an application and the relevant state associated with it. On most applications Stores don&#8217;t exist in isolation, but depend on other model parts to perform their work.

Circuit allows you to express dependencies between Stores on the level of an Action type.

### <a class="anchor" href="#preparation-and-completion-phase" name="user-content-preparation-and-completion-phase"></a>Preparation and Completion phase

The Circuit Dispatcher processes Actions in two phases: a preparation and a completion phase.

During the preparation phase Stores signal interest in a particular Action type and any dependencies they have on other Stores for a particular Action type.

The Dispatcher creates a dependency graph for each action type and invoke the Stores in an ordered way, one at a time.

This way Stores can safely rely on the State of other Stores during the processing of an Action.

Upon completion a Store emits Change Events to signal interested parties that the data or state of the application has changed. Since Stores process the Action in an ordered way, the change notifications follow that pattern.

#### <a class="anchor" href="#action-acknowledgement" name="user-content-action-acknowledgement"></a>Action Acknowledgement

Many Store implementations rely on asynchronous invocations to the service backend. Circuit was build to provide support for asynchronous flow control in Stores.

When Stores complete the processing of an Action, they acknowledge the Action they processed. This signals the Dispatcher that the next Store can start processing the Action.  

## References

 [1]: https://github.com/hal/circuit
 [2]: http://facebook.github.io/react/docs/flux-overview.html
 [3]: http://facebook.github.io/react/index.html
 [4]: http://hbraun.info/wp-content/uploads/2014/07/circuit.png