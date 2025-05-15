---
date: '2025-05-15T08:01:20+10:00'
draft: true
title: Workflow
---

Servicely provides the ability to create complex custom workflows.

![](/images/2290581505/2291007491.png)

| **Activity Type** | **Icon**                               | **Description**                                                                                                                                                                                                                                                                                                                                           |
| ----------------- | -------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Comment           | ![](/images/2290581505/2290810926.png) | Allows the placing of comments onto Workflows                                                                                                                                                                                                                                                                                                             |
| User Action       | ![](/images/2290581505/2290974740.png) | Represents a status and a set of actions that are to be made available to users. Typically used to present a set of options to the user when the workflow is at a point where there are manual actions or decisions that must be made by the user. Available actions will be presented to the user on the form to allow the user to advance the workflow. |
| Approval          | ![](/images/2290581505/2291007497.png) | Allows approval steps to be added to a workflow.                                                                                                                                                                                                                                                                                                          |
| Complete          | ![](/images/2290581505/2291105793.png) | Represents the end/completion of a workflow.                                                                                                                                                                                                                                                                                                              |
| Scriptable        | ![](/images/2290581505/2290909211.png) | Provides the ability to run a custom script as part of the workflow. Designed to be a synchronous script that executes once per pass. Does not generate a Workflow Status by default, as the workflow does not pause here.                                                                                                                                |
| Scriptable Async  | ![](/images/2290581505/2290843688.png) | Provides the ability to run a custom script as part of the workflow. Designed to be used when the action is asynchronous (e.g. triggering an integration or awaiting other tickets/actions). Generates a Workflow Status so the associated record indicates the wait state.                                                                               |
| Timer             | ![](/images/2290581505/2290974746.png) | Allows a timer to be scheduled to progress the ticket (e.g. could be used for auto closure or any other time based progression).                                                                                                                                                                                                                          |
| If/Else           | ![](/images/2290581505/2290876445.png) | Provides the ability to branch the workflow based on a simple conditional query.                                                                                                                                                                                                                                                                          |
| Switch            | ![](/images/2290581505/2290810934.png) | Provides the ability to branch the workflow based on a custom script. Designed to be a synchronous script that executes once per pass. Does not generate a Workflow Status by default, as the workflow does not pause here.                                                                                                                               |
| Switch Async      | ![](/images/2290581505/2290810940.png) | Provides the ability to branch the workflow based on a custom script. Designed to be used when the action is asynchronous (e.g. triggering an integration or awaiting other tickets/actions). Generates a Workflow Status so the associated record indicates the wait state.                                                                              |
| Run Action        | ![](/images/2290581505/2290974754.png) | Provides the ability to Run an Intelligent Action.                                                                                                                                                                                                                                                                                                        |
| Exception         | ![](/images/2290581505/2290843694.png) | Provides the ability to respond to an exception anywhere in the workflow.                                                                                                                                                                                                                                                                                 |

# Implementation specifics

## User action

The User Action workflow activity provides the ability for end users to
control the workflow, by presenting the the user with multiple options
to progress the workflow status.

![](/images/2290581505/2291007519.png)

### Adding transition options

Press the ‘Add new transition’ button, an enter the new transition name:

![](/images/2290581505/2290909225.png)![](/images/2290581505/2291007531.png)

A transition can run a Before script for purposes such as making a field
to be mandatory before the status transition can take place. An example
is, to make the Assignee field on Incident table before moving the
Incident off from New to Work in Progress status.

You would code something like below:

![](/images/2290581505/2604073010.png?width=1402)

You will need to end the Before script with a return true; statement, so
that the rest of the form checks can run to completion.

### Linking to next activity

Drag from the circle in the Transition to the left most corner of the
target workflow activity.

![](/images/2290581505/2290909233.png)

## Approval

This activity requests approvals and will stop the records running the
workflow from proceeding any further.

![](/images/2290581505/2354216969.png?width=1020)

What you can configure:

### Approval Mechanisms
| Item                 | Description | Example |
| -------------------- | ----------- | ------- |
| Approval requirement | testing     | test    |

## Scriptable Activity

The ‘Scriptable’ activity allows the Workflow author to run arbitrary
code. This activity is typically transient and does not have a Workflow
status associated with the Activity.

![](/images/2290581505/2290810979.png)

### Script context

The ‘Scriptable Activity’ receives the following script context items:

| **Item**  | **Description**                                                                       |
| --------- | ------------------------------------------------------------------------------------- |
| `current` | A TableRecord object representing the object associated with the Workflow             |
| `context` | A plain JSON Map object which can be used to store state associated with the Workflow |
| `log`     | A Script Logger that allows logs to be written to the WorkflowHistory log             |

## Scriptable Async Activity

The ‘Scriptable Async’ activity allows the Workflow author to run
arbitrary code. Usage is similar to the ‘Scriptable Activity’ with the
primary difference being that this activity is designed to be used when
the result of the script is asynchronous (i.e. the activity needs to
wait on something external happening). This activity creates an
associated Workflow Status.

![](/images/2290581505/2291236869.png)

The Scriptable Async activity exposes two scripts: an Initialization
Script and an Evaluation script.

The initialization script is called once when the Activity is initiated,
and is designed to be used to perform any initialization associated with
the activity (initiate an integration, raise subtasks, etc.).

The evaluation script is called asynchronously to determine whether the
activity has completed. This needs to be performed by an external action
(e.g. on completion of an integration). A convenience method is
available to automatically evaluate paused workflows for related tickets
(e.g. for subtasks or other related information).

| **Table Property**            | **Description**                                                                                                                                                                  | **Example**                                                                                                                        |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| workflow.trigger.parent.field | A Table property that specifies a relationship that will trigger an asynchronous workflow evaluation of the related record. Can also be a comma delimited list of relationships. | On the HRCaseTask table, specifying the value “ParentHRCase” will enable the evaluation of the Workflow related to HRCase records. |

![](/images/2290581505/2291269665.png)

### Script context

The ‘Scriptable Async Activity’ receives the following script context
items:

<table class="confluenceTable" data-table-width="1800"
data-layout="default"
data-local-id="b577d388-d26a-4177-8e6e-5d744a1c9049">
<tbody>
<tr>
<th class="confluenceTh"><p><strong>Item</strong></p></th>
<th class="confluenceTh"><p><strong>Description</strong></p></th>
</tr>
&#10;<tr>
<td class="confluenceTd"><p><code>current</code></p></td>
<td class="confluenceTd"><p>A TableRecord object representing the object
associated with the Workflow</p></td>
</tr>
<tr>
<td class="confluenceTd"><p><code>context</code></p></td>
<td class="confluenceTd"><p>A plain JSON Map object which can be used to
store state associated with the Workflow</p></td>
</tr>
<tr>
<td class="confluenceTd"><p><code>log</code></p></td>
<td class="confluenceTd"><p>A Script Logger that allows logs to be
written to the WorkflowHistory log</p></td>
</tr>
<tr>
<td class="confluenceTd"><p><code>ActivityOptions</code></p></td>
<td class="confluenceTd"><p>Constants used for the return value or other
items within the script.</p>
<p>Scriptable Async Actions that have not yet completed their
requirements should return the value:
<code>ActivityOptions.DELAY_EVALUATION</code></p>
<p>Scriptable Async Actions that <strong>have</strong> completed their
requirements should return <code>true</code></p></td>
</tr>
</tbody>
</table>

# Execution

## Order

When there are multiple workflows for the same table, e.g. ITSM Request
table having multiple workflows for different catalog items, please
ensure that they are ordered accordingly. This is necessary for the use
case where the workflow is attached to the table not because of service
catalog, e.g. raising ITSM Request directly. When a record such as ITSM
Request is directly created, Servicely will select the Workflow with
lowest Order number. This means a workflow with Order of 10 will take
precedence over the one with Order of 20.