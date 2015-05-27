---
title: 'Developer notes: How does data binding and model conversions work in the AS 7 console?'
author: hbraun
layout: post
permalink: /2011/09/developer-notes-how-does-data-binding-and-model-conversions-work-in-the-as-7-console/
blogger_blog:
  - relative-order.blogspot.com
blogger_author:
  - 
blogger_permalink:
  - /2011/09/developer-notes-how-does-data-binding.html
dsq_thread_id:
  - 850851338
categories:
  - Wildfly
---
The JBoss AS 7 management layer works on a detyped, tree like mode structure to represent subsystem and server configuration options. The big benefit is that management clients don&#8217;t depend on statically typed model, but instead rely on a fairly small API that&#8217;s not subject to change. The model itself can easily be converted to and from JSON, which opens the management layer to variety of scripting environments and alternate management implementations.

As many of you know, the management web interface is implemented in GWT. The means we cross compile from Java to Javascript, but all development is done in Java. Many of the default [GWT components like tables, trees and lists][1] expect a strongly typed Java model, since this would be logical choice for most GWT implementations. For us, working on the management web interface this means we have to bridge the gap between the detyped model the application server uses and the strongly typed model the GWT components rely on.

In this post I am going to explain some of the building blocks we use within the management interface, to reduce the amount of boilerplate we have to provide converting between the two model representations.

**The detyped model**

A typical model representation we get from the AS management layer looks like this:

<pre><br />[domain@localhost:9999 /] /subsystem=datasources/data-source=ExampleDS:read-resource<br />{<br />    "outcome" => "success",<br />    "result" => {<br />        "connection-url" => "jdbc:h2:mem:test;DB_CLOSE_DELAY=-1",<br />        "driver-name" => "h2",<br />        "enabled" => true,<br />        "jndi-name" => "java:jboss/datasources/ExampleDS",<br />        "jta" => true,<br />        "password" => "sa",      <br />        "use-ccm" => true,<br />        "user-name" => "sa",<br />    }<br />}<br /><br /></pre>

In this case we are looking at a data source.  
In order create and modify datasource, the management client would need to send a detyped representation like the one above and will get a response of the same content type.

**GWT entities**

Entities in GWT are represented as Java interfaces with getter and setter methods ([AutoBean API][2]). The corresponding representation for the data source above, would look like this:

<pre><br />@Address("/subsystem=datasources/data-source={0}")<br />public interface DataSource {<br /><br />    @Binding(detypedName = "jndi-name")<br />    String getJndiName();<br />    void setJndiName(String name);<br /><br />    @Binding(detypedName = "user-name")<br />    String getUsername();<br />    void setUsername(String user);<br /><br />    String getPassword();<br />    void setPassword(String password);<br /><br />    [...]<br />}<br /></pre>

**Coverting between two models**

Converting between the two model representation is the job of the EntityAdapter. An EntityAdapter works on the meta data declared on the entity class (@Address &#038; @Binding annotations). The metadata itself is extracted during the compile time phase ([deferred binding][3]) . 

The current meta data structure is divided into two distinct concepts: Entity addressing and the property binding. The address is required to perform operations on the detyped model (&#8220;/subsystem=datasource/data-source=ExampleDS:read-resource&#8221;). The property binding is used to get and set values within both models. 

Let&#8217;s take a look at an example:

<pre><br /><br />// Create an EntityAdapter for a specific type<br />EntityAdapter&lt;dataSource> adapter = new EntityAdapter&lt;dataSource>(DataSource.class, metaData);<br /><br />// Convert from entity to DMR representation<br />DataSource datasource = ...;<br />ModelNode operation = adapter.fromEntity(datasource);<br /><br />// execute the operation (HTTP request) ...<br /><br /></pre>

First of all, we create an EntityAdapter for the DataSource.class type. This adapter allows us to convert an entity instance (DataSource datasource) into a ModelNode (detyped) representation. We can use this model to execute an operation against the AS management layer (HTTP Post).

Let&#8217;s do it vice versa: Reading a detyped model and convert it into an entity.

<pre><br />// Create an EntityAdapter for a specific type<br />EntityAdapter&lt;dataSource> adapter = new EntityAdapter&lt;dataSource>(DataSource.class, metaData);<br /><br />ModelNode detyped = ...; // HTTP response<br /><br />// Convert form DMR to entity<br />DataSource datasource = adapter.fromDMR(detyped);<br /><br />// Work on the entity ....<br /><br /></pre>

**Addressing of resources**

As you can see in the above example, the entity carries an @Address annotation. In order to read from or write the management layer you would need to know how to address a resource properly. For datasources this would be:

<pre><br />/subsystem=datasources/data-source=ExampleDS<br /></pre>

There are many cases where we need an address. It makes sense to associate this information with the entity itself and use it as a template for subsequent requests. I.e an address template like &#8220;@Address(&#8220;/subsystem=datasources/data-source={0}&#8221;)&#8221;

<pre><br /><br />AddressBinding address = metaData.getBeanMetaData(DataSource.class).getAddress();<br />ModelNode operation = address.asSubresource("ExampleDS");<br /><br />// further specify the operation (OP, RECURSIVE,ETC)<br />operation.get(OP).set(READ_RESOURCE);<br /><br />// execute the operation (HTTP request) ...<br /></pre>

**What&#8217;s next?**

We have seen how two specific problems are solved: Addressing of resources and converting between two model types. In the next part of this series, I am going to explain how the actual data binding (mapping to HTML forms) actually works.

 [1]: http://www.google.de/url?sa=t&#038;source=web&#038;cd=1&#038;sqi=2&#038;ved=0CB8QFjAA&#038;url=http%3A%2F%2Fcode.google.com%2Fwebtoolkit%2Fdoc%2Flatest%2FDevGuideUiCellTable.html&#038;ei=ltuCTrePH42A-waTkciqDw&#038;usg=AFQjCNGTu-9zVEmMd7PGX-v46t_km6QSmg&#038;sig2=RzmiKuyfSmWkead7XL5jrQ
 [2]: http://code.google.com/p/google-web-toolkit/wiki/AutoBean
 [3]: http://code.google.com/webtoolkit/doc/latest/DevGuideCodingBasicsDeferred.html