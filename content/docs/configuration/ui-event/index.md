---
date: '2025-05-15T14:24:34+10:00'
draft: false
title: 'UI Events'
---

# Overview

A UI Event automates business logics on a Servicely Table’s form and/or
fields as they are loaded or as you interact with them on your web
browser, i.e. doing field updates or saving your changes on the form.

- It runs on the client side (your computer’s web browser)

- It can call <a href="System_controllers_custom_inbound_scripting_"
  data-linked-resource-id="2077524110" data-linked-resource-version="10"
  data-linked-resource-type="page">System controllers (custom inbound
  scripting)</a> to run server side functions (also refer to
  <a href="Table_API_Server_" data-linked-resource-id="2136834049"
  data-linked-resource-version="26" data-linked-resource-type="page">Table
  API (Server)</a> )

- It has access to the current record displayed on the form

- It has access to classes and functions within client accessible
  Application Properties (refer to
  <a href="Application_properties" data-linked-resource-id="1191510171"
  data-linked-resource-version="6"
  data-linked-resource-type="page">Application properties</a> )

Javascript knowledge is required

# Creating a UI Event

<table class="confluenceTable" data-table-width="1800"
data-layout="default"
data-local-id="1a2b0e99-f423-4c64-8890-1b9610147ce6">
<tbody>
<tr>
<th class="confluenceTh"><p><strong>Field name</strong></p></th>
<th class="confluenceTh"><p><strong>Field type</strong></p></th>
<th class="confluenceTh"><p><strong>Description</strong></p></th>
<th class="confluenceTh"><p><strong>Sample value</strong></p></th>
</tr>
&#10;<tr>
<td class="confluenceTd"><p>Name</p></td>
<td class="confluenceTd"><p>String</p></td>
<td class="confluenceTd"><p>Name of the UI Event for administrative
purposes</p></td>
<td class="confluenceTd"><p>Incident - Set Requested for based on
selected Requestor</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Event type</p></td>
<td class="confluenceTd"><p>Choice</p></td>
<td class="confluenceTd"><p>Whether the UI Event is to run based on a
field or a form:</p>
<ul>
<li><p>Field event</p></li>
<li><p>Form event</p></li>
</ul></td>
<td class="confluenceTd"><p>Field event</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Event name</p></td>
<td class="confluenceTd"><p>Choice</p></td>
<td class="confluenceTd"><p>Action taking place that should result in
this UI Event run:</p>
<p>If Event type is “Field event”, the valid events to choose from
are:</p>
<ul>
<li><p>On change - &lt;<em>runs when form is loading or when nominated
Field on UI event changes its value</em>&gt;</p></li>
<li><p>On relation update - &lt;<em>runs when a related list is updated
with entries added or removed</em>&gt;</p></li>
</ul>
<p>If Event type is “Form event”, the valid events to choose from
are:</p>
<ul>
<li><p>On form load - &lt;<em>runs when a form has finished
loading</em>&gt;</p></li>
<li><p>On form submit - &lt;<em>runs after you submit changes on the
form by pressing the Save button</em>&gt;</p></li>
</ul>
<p>Only for “On form submit”, your script can return either true or
false to decide whether or not to allow the form’s submission (create or
update of a record) to proceed.</p></td>
<td class="confluenceTd"><p>On change</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Active</p></td>
<td class="confluenceTd"><p>Boolean</p></td>
<td class="confluenceTd"><p>When active, the UI Event will be available
to run should it meets the configured events</p></td>
<td class="confluenceTd"><p>Yes</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Table</p></td>
<td class="confluenceTd"><p>Reference</p></td>
<td class="confluenceTd"><p>Table the UI Event applies to</p></td>
<td class="confluenceTd"><p>Incident</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Field</p></td>
<td class="confluenceTd"><p>Reference</p></td>
<td class="confluenceTd"><p>Available if Event type is “Field event”.
The UI Event runs when the Field’s value on the form has been
updated.</p></td>
<td class="confluenceTd"><p>Requestor</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Application</p></td>
<td class="confluenceTd"><p>Reference</p></td>
<td class="confluenceTd"><p>Application that the UI Event is packaged
under</p></td>
<td class="confluenceTd"><p>itsm</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Description</p></td>
<td class="confluenceTd"><p>String</p></td>
<td class="confluenceTd"><p>Provides more details about what the UI
Event is for, for administrative purposes</p></td>
<td class="confluenceTd"><p>When a Requestor is set on an Incident, copy
them across as an Incident’s Requested for if it isn’t set
already</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Script</p></td>
<td class="confluenceTd"><p>Script</p></td>
<td class="confluenceTd"><p>Client side script the UI Event runs. The
script has access to:</p>
<ol>
<li><p>The “current” object that represents the current record.</p></li>
<li><p>The “viewAspect” variable the represents the view aspect shown on
the form the UI Event runs on. Please refer to <a
href="Aspect_configuration" data-linked-resource-id="1191510219"
data-linked-resource-version="6" data-linked-resource-type="page">Aspect
configuration</a> for more information about view aspects.</p></li>
<li><p>The “isLoading” variable that returns true when the form is
loading</p></li>
</ol>
<div>
<div>
<p>For “On form submit” event:</p>
<p>Provide a <em>return false;</em> if you need to prevent a form’s
submission.</p>
<p>Not providing a return value is the same as providing a <em>return
true;</em> statement</p>
</div>
</div></td>
<td class="confluenceTd"><div class="code panel pdl"
style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb1"
data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence"
data-theme="Confluence"
style="brush: java; gutter: false; theme: Confluence"><pre
class="sourceCode java"><code class="sourceCode java"><span id="cb1-1"><a href="#cb1-1" aria-hidden="true" tabindex="-1"></a><span class="cf">if</span> <span class="op">(</span>current<span class="op">.</span><span class="fu">Requestor</span><span class="op">.</span><span class="fu">hasValue</span><span class="op">()</span> <span class="op">&amp;&amp;</span> <span class="op">!</span>current<span class="op">.</span><span class="fu">RequestedFor</span><span class="op">.</span><span class="fu">hasValue</span><span class="op">())</span> <span class="op">{</span></span>
<span id="cb1-2"><a href="#cb1-2" aria-hidden="true" tabindex="-1"></a>    current<span class="op">.</span><span class="fu">RequestedFor</span><span class="op">(</span>current<span class="op">.</span><span class="fu">Requestor</span><span class="op">.</span><span class="fu">value</span><span class="op">());</span></span>
<span id="cb1-3"><a href="#cb1-3" aria-hidden="true" tabindex="-1"></a><span class="op">}</span></span></code></pre></div>
</div>
</div>
<p>Please refer to the Examples section below for other examples/use
cases. This primarily uses the <a href="Table_API_Client_"
data-linked-resource-id="2280620096" data-linked-resource-version="4"
data-linked-resource-type="page">Table API (Client)</a> and <a
href="User_Object_Client_and_Server_"
data-linked-resource-id="2280423425" data-linked-resource-version="3"
data-linked-resource-type="page">User Object (Client and Server)</a>
(Client side only).</p></td>
</tr>
</tbody>
</table>

# Examples

**Make Assignee required only when status is not new for a viewAspect
called “ServiceDesk”**

<table class="confluenceTable" data-table-width="1800"
data-layout="default"
data-local-id="6150721e-9ccf-4d23-89a6-3de79cd819c6">
<tbody>
<tr>
<th class="confluenceTh"><p><strong>Field</strong></p></th>
<th class="confluenceTh"><p><strong>Value</strong></p></th>
</tr>
&#10;<tr>
<td class="confluenceTd"><p>Name</p></td>
<td class="confluenceTd"><p>Incident - Always for ServiceDesk
aspect</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Event type</p></td>
<td class="confluenceTd"><p>Form event</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Event name</p></td>
<td class="confluenceTd"><p>On form load</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Active</p></td>
<td class="confluenceTd"><p>Yes</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Table</p></td>
<td class="confluenceTd"><p>Incident</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Description</p></td>
<td class="confluenceTd"><p>When viewAspect is “Service Desk” and status
is not new, always set the assignee to be required. Otherwise keep
optional. Keep hidden for all other aspects.</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Script</p></td>
<td class="confluenceTd"><div class="code panel pdl"
style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb1"
data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence"
data-theme="Confluence"
style="brush: java; gutter: false; theme: Confluence"><pre
class="sourceCode java"><code class="sourceCode java"><span id="cb1-1"><a href="#cb1-1" aria-hidden="true" tabindex="-1"></a><span class="cf">if</span> <span class="op">(</span>viewAspect <span class="op">==</span> “ServiceDesk” <span class="op">&amp;&amp;</span> current<span class="op">.</span><span class="fu">WorkflowStatus</span><span class="op">()</span> <span class="op">!=</span> “new”<span class="op">)</span> <span class="op">{</span></span>
<span id="cb1-2"><a href="#cb1-2" aria-hidden="true" tabindex="-1"></a>    current<span class="op">.</span><span class="fu">Assignee</span><span class="op">.</span><span class="fu">visible</span><span class="op">(</span><span class="kw">true</span><span class="op">);</span></span>
<span id="cb1-3"><a href="#cb1-3" aria-hidden="true" tabindex="-1"></a>    current<span class="op">.</span><span class="fu">Assignee</span><span class="op">.</span><span class="fu">required</span><span class="op">(</span><span class="kw">true</span><span class="op">);</span></span>
<span id="cb1-4"><a href="#cb1-4" aria-hidden="true" tabindex="-1"></a><span class="op">}</span> <span class="cf">else</span> <span class="op">{</span></span>
<span id="cb1-5"><a href="#cb1-5" aria-hidden="true" tabindex="-1"></a>    current<span class="op">.</span><span class="fu">Assignee</span><span class="op">.</span><span class="fu">required</span><span class="op">(</span><span class="kw">false</span><span class="op">);</span></span>
<span id="cb1-6"><a href="#cb1-6" aria-hidden="true" tabindex="-1"></a>    <span class="cf">if</span> <span class="op">(</span>viewAspect <span class="op">!=</span> <span class="st">&quot;ServiceDesk&quot;</span><span class="op">)</span> <span class="op">{</span></span>
<span id="cb1-7"><a href="#cb1-7" aria-hidden="true" tabindex="-1"></a>        current<span class="op">.</span><span class="fu">Assignee</span><span class="op">.</span><span class="fu">visible</span><span class="op">(</span><span class="kw">false</span><span class="op">);</span></span>
<span id="cb1-8"><a href="#cb1-8" aria-hidden="true" tabindex="-1"></a>    <span class="op">}</span></span>
<span id="cb1-9"><a href="#cb1-9" aria-hidden="true" tabindex="-1"></a><span class="op">}</span></span></code></pre></div>
</div>
</div></td>
</tr>
</tbody>
</table>

**Default an Incident’s Location based on Requestor’s location data,
using a controller**

This requires the use of a Controller as we need to query an Incident’s
Requestor user record and get their Location.

<table class="confluenceTable" data-table-width="1800"
data-layout="default"
data-local-id="b3410cc3-4f83-41f1-873f-83c9898bdfa4">
<tbody>
<tr>
<th class="confluenceTh"><p><strong>Field</strong></p></th>
<th class="confluenceTh"><p><strong>Value</strong></p></th>
</tr>
&#10;<tr>
<td class="confluenceTd"><p>Name</p></td>
<td class="confluenceTd"><p>Incident - Default Location based on
Requestor</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Event type</p></td>
<td class="confluenceTd"><p>Field event</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Event name</p></td>
<td class="confluenceTd"><p>On change</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Active</p></td>
<td class="confluenceTd"><p>Yes</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Table</p></td>
<td class="confluenceTd"><p>Incident</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Field</p></td>
<td class="confluenceTd"><p>Requestor</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Description</p></td>
<td class="confluenceTd"><p>Once a Requestor is selected/updated, if an
Incident’s Location is blank, set the Location based on that user
record</p></td>
</tr>
<tr>
<td class="confluenceTd"><p>Script</p></td>
<td class="confluenceTd"><div class="code panel pdl"
style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb1"
data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence"
data-theme="Confluence"
style="brush: java; gutter: false; theme: Confluence"><pre
class="sourceCode java"><code class="sourceCode java"><span id="cb1-1"><a href="#cb1-1" aria-hidden="true" tabindex="-1"></a><span class="co">//Assuming there is a Requestor, form is not loading, Location is not already set</span></span>
<span id="cb1-2"><a href="#cb1-2" aria-hidden="true" tabindex="-1"></a><span class="cf">if</span> <span class="op">(!</span>isLoading <span class="op">&amp;&amp;</span> current<span class="op">.</span><span class="fu">Requestor</span><span class="op">.</span><span class="fu">hasValue</span><span class="op">()</span> <span class="op">&amp;&amp;</span> <span class="op">!</span>current<span class="op">.</span><span class="fu">Location</span><span class="op">.</span><span class="fu">hasValue</span><span class="op">())</span> <span class="op">{</span></span>
<span id="cb1-3"><a href="#cb1-3" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-4"><a href="#cb1-4" aria-hidden="true" tabindex="-1"></a>    <span class="co">//Create a parameter object to provide with our request to the controller</span></span>
<span id="cb1-5"><a href="#cb1-5" aria-hidden="true" tabindex="-1"></a>    <span class="dt">var</span> requestObj <span class="op">=</span> <span class="op">{};</span></span>
<span id="cb1-6"><a href="#cb1-6" aria-hidden="true" tabindex="-1"></a>    requestObj<span class="op">.</span><span class="fu">userId</span> <span class="op">=</span> current<span class="op">.</span><span class="fu">Requestor</span><span class="op">();</span></span>
<span id="cb1-7"><a href="#cb1-7" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-8"><a href="#cb1-8" aria-hidden="true" tabindex="-1"></a>    <span class="co">//Call the server with the information required.</span></span>
<span id="cb1-9"><a href="#cb1-9" aria-hidden="true" tabindex="-1"></a>    WS<span class="op">.</span><span class="fu">controller</span><span class="op">(</span><span class="st">&quot;UserInfoController&quot;</span><span class="op">,</span> requestObj<span class="op">)</span></span>
<span id="cb1-10"><a href="#cb1-10" aria-hidden="true" tabindex="-1"></a>        <span class="op">.</span><span class="fu">done</span><span class="op">(</span><span class="fu">function</span><span class="op">(</span>response<span class="op">)</span> <span class="op">{</span></span>
<span id="cb1-11"><a href="#cb1-11" aria-hidden="true" tabindex="-1"></a>            current<span class="op">.</span><span class="fu">Location</span><span class="op">(</span><span class="bu">String</span><span class="op">(</span>response<span class="op">.</span><span class="fu">data</span><span class="op">.</span><span class="fu">locationID</span><span class="op">));</span></span>
<span id="cb1-12"><a href="#cb1-12" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-13"><a href="#cb1-13" aria-hidden="true" tabindex="-1"></a>            <span class="co">//If there was an error, add it to the console log.</span></span>
<span id="cb1-14"><a href="#cb1-14" aria-hidden="true" tabindex="-1"></a>        <span class="op">}).</span><span class="fu">fail</span><span class="op">(</span><span class="fu">function</span><span class="op">(</span>response<span class="op">)</span> <span class="op">{</span></span>
<span id="cb1-15"><a href="#cb1-15" aria-hidden="true" tabindex="-1"></a>            console<span class="op">.</span><span class="fu">log</span><span class="op">(</span><span class="st">&quot;UserInfoController: Start Error&quot;</span><span class="op">);</span></span>
<span id="cb1-16"><a href="#cb1-16" aria-hidden="true" tabindex="-1"></a>            console<span class="op">.</span><span class="fu">log</span><span class="op">(</span>response<span class="op">);</span></span>
<span id="cb1-17"><a href="#cb1-17" aria-hidden="true" tabindex="-1"></a>            console<span class="op">.</span><span class="fu">log</span><span class="op">(</span><span class="st">&quot;UserInfoController: End Error&quot;</span><span class="op">);</span></span>
<span id="cb1-18"><a href="#cb1-18" aria-hidden="true" tabindex="-1"></a>        <span class="op">});</span></span>
<span id="cb1-19"><a href="#cb1-19" aria-hidden="true" tabindex="-1"></a><span class="op">}</span></span></code></pre></div>
</div>
</div>
<p>Refer to below for sample of the Controller.</p></td>
</tr>
</tbody>
</table>

<a href="System_controllers_custom_inbound_scripting_"
data-linked-resource-id="2077524110" data-linked-resource-version="10"
data-linked-resource-type="page">Controller</a> “UserInfoController”
Script referenced in the UI Event’s script in above example, can look
like the following (variable “locationID” is what the Controller returns
and the UI Event makes use of):

``` java
answer = {};

// Query the User table for the record with the provided userId parameter.
if (userId) {
    let userRec = Table("User", userId);
    if (userRec) {
        if (userRec.Location.hasValue()) {
            answer.locationID = userRec.Location.value();
        }        
    }
}

answer;
```

**Default an Incident’s Location based on Requestor’s location data,
using a REST call**

The UI Event can be configured the same way per the above example with a
Controller, but the UI Event script should look like the following
instead:

``` java
//Assuming there is a Requestor, form is not loading, Location is not already set
if (!isLoading && current.Requestor.hasValue() && !current.Location.hasValue()) {
    REST.get("User", current.Requestor(), { fields: "Location" })
        .then(response => {
            current.Location(response.data.Location);
        });
}
```