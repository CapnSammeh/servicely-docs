---
title: Intelligent Routing
draft: true
---
Intelligent Routing offers a means for administrators to define rules surrounding the automatic assignment of records (e.g., ITSM Requests and Incidents, Tasks, HR Cases, etc.) to Fulfillers or Agents based on predefined functional logic. 

![](/images/cleanshot-2025-05-14-at-15.01.57-2x.png "Servicely Intelligent Routing")

Intelligent Routing leverages Round-Robin assignment based on one of the below configurable routing rules:

* [Active Ticket Count](#active-ticket-count)
* [Ticket Priority Volumes](#ticket-Priority-Volumes)
* [Time since last Assignment](#Time-since-last-Assignment)
* [Static Routing](#Static-Routing)
* [Custom Routing](#Custom-Routing)

Intelligent Routing in Servicely allows Administrators to configure the Active State of the Rule, the Order of execution (considering other rules for the same table), the applicable Groups to perform routing within, and also respects the User's `assignment selectability` to ensure that only the appropriate users are routed tickets.

# Available Rules
## Active Ticket Count

## Ticket Priority Volumes

## Time since last Assignment

## Static Routing

## Custom Routing

---
## Creating a Routing Rule

1. As an *Administrator*, navigate to the `Intelligent Routing Rule` section of the main navigation. This menu item should direct you to the `intelligentroutingrule` table. 
2. Populate the fields on the from:
    * **Name**: An identifiable name for future reference.
    * **Short Description**: Provide a short overview for future reference.
    * **Table**: The Table Records we wish to automatically route. e.g., `ITSMRequest`.
    * **Routing Rule**: The specific Routing Rule. See the [Available Rules](#Available-Rules) section of this document for details.
    * **Active**: Set to True to ensure the Routing Rule is run when tickets are assigned.
    * **Order**: Set to `0` unless other rules should be evaluated *before* this rule.
    * **Groups**: Specify the groups this rule should be applied to.
    * **Respect Assignment Selectability**: Setting this to True will only route tickets to users where the Selectable for Assignment (`User.SelectableForAssignment`) is **true**.
