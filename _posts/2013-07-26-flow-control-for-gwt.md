---
title: Flow Control for GWT
subtitle: 'A re-usable GWT module that provides an API for managing asynchronous control flow.'
author: hbraun
layout: post
permalink: /2013/07/flow-control-for-gwt/
dsq_thread_id:
  - 1533243385
categories:
  - GWT
  - Wildfly
tags:
  - cuted
---
**tl;dr**

> Within Ajax applications you need to manage a lot of interaction and RPC related asynchronous events. The control flow structures become hard to understand and yield unpredicatable results.
> 
> We created a re-usable GWT module that provides some higher order control structures that you can use to tame the asynchronous callback beast. It&#8217;s been inspired by <a href="https://github.com/caolan/async" title="Async.js" target="_blank">Async.js</a>, but aligns with the core GWT API&#8217;s more naturally. 

**Control Flow API**


~~~
package org.jboss.gwt.flow.client;

import com.google.gwt.core.client.Scheduler;

/**
 * Flow control functions for GWT.
 * Integrates with the default GWT scheduling mechanism.
 *
 * @author Heiko Braun
 * @date 3/8/13
 */
public class Async<C>
{

    /**
     * Run an array of functions in series, each one running once the previous function has completed.
     * If any functions in the series pass an error to its callback,
     * no more functions are run and outcome for the series is immediately called with the value of the error.
     *
     * @param outcome
     * @param functions
     */
    public void series(final Outcome outcome, final Function... functions)
    {
       [...]
    }

    /**
     * Runs an array of functions in series, working on a shared context.
     * However, if any of the functions pass an error to the callback,
     * the next function is not executed and the outcome is immediately called with the error.
     *
     * @param context
     * @param outcome
     * @param functions
     */
    public void waterfall(final C context, final Outcome<C> outcome, final Function<C>... functions)
    {
        [...]
    }

    /**
     * Run an array of functions in parallel, without waiting until the previous function has completed.
     * If any of the functions pass an error to its callback, the outcome is immediately called with the value of the
     * error.
     *
     * @param outcome
     * @param functions
     */
    public void parallel(final Outcome outcome, final Function... functions)
    {
        [...]
    }

    /**
     * Repeatedly call function, while condition is met. Calls the callback when stopped, or an error occurs.
     *
     * @param condition
     * @param outcome
     * @param function
     */
    public void whilst(Precondition condition, final Outcome outcome, final Function function)
    {
        [...]
    }

}

/**
 * An execution delegate able to control the outcome.
 *
 * @author Heiko Braun
 * @date 3/8/13
 */
public interface Function<C> {
    void execute(Control<C> control);
}

/**
 * Execution control handle passed into functions
 *
 * @author Heiko Braun
 * @date 3/8/13
 */
public interface Control<C> {

    void proceed();
    void abort();
    C getContext();
}

/**
 * The final outcome of the controlled flow.
 *
 * @author Heiko Braun
 * @date 3/8/13
 */
public interface Outcome<C> {

    void onFailure(C context);

    void onSuccess(C context);

}
~~~

**Example: Waterfall Execution**

Runs an array of functions in series, working on a shared context. However, if any of the functions pass an error to the callback, the next function is not executed and the outcome is immediately called with the error.

~~~
private void runWaterfall()
    {

        final Function foo = new SpecificFunction("first");    (1)
        final Function bar = new SpecificFunction("second");   (2)

        final Outcome<StringBuffer> outcome = new Outcome<StringBuffer>() (3)
        {
            @Override
            public void onFailure(StringBuffer sb)
            {
                Window.alert("Outcome is failure");
            }

            @Override
            public void onSuccess(StringBuffer sb)
            {
                Window.alert("Outcome is success: " + sb);

            }
        };

        new Async<StringBuffer>().waterfall(new StringBuffer(), outcome, foo, bar); (4)

    }
~~~

Step by Step

  1. Create some executable command (aka Function)
  2. Create a command that should be run once the first one finishes
  3. The final callback to be invoked when the waterfall execution finishes. The StringBuffer acts as a shared context object 
  4. Invoke the waterfall execution, providing a shared context (StringBuffer) and a number of function to be executed

**Sources &#038; Maven Coordinates**

The sources for the control API can be found at github:

<https://github.com/hal/core/tree/master/flow/core>

The maven artefacts resides with the JBoss repositories:

~~~
<dependency>
  <groupId>org.jboss.as</groupId>
  <artifactId>jboss-as-console-flow</artifactId>
  <version>1.6.3.Final</version>
</dependency>
~~~

**GWT Module Setup**

~~~
<module rename-to="your_module">
    [...]
    <inherits name="org.jboss.gwt.flow.Flow"/>
</module>
~~~