---
title: "Work Application"
date: 2025-05-15T14:19:50+10:00
draft: true
---

# Structure

![](/images/1191510305/2185330689.png)

# Purpose

Servicely's base build has been designed to make application development
efficient and consistent.  This is done by the way that the initial
tables have been structured to ensure that the majority of fields that
are used for every process (such as assignment group, assignee, short
description) all have the same field name.  This allows them to
integrate and talk to each other much easier.  When coming up with a new
process within Servicely, it is important to determine if it should be
made within its own application.  As can be seen in the diagram below,
each business unit should have it's own parent table, its own roles and
its own table.  This allows you to segregate the security of the
application much easier. 

For example, imagine that a new OHS application needed to be developed. 
The recommended approach would to be to first make a OHSWork table,
where Work is the parent table.  On the OHSWork table, any fields that
are specific to OHS that should appear in all OHS tables should be added
on this level.  This way any fields, relationships or otherwise that are
consistent across the OHS business area, only has to be done once in one
level.

It is not recommended that if something is made for a specific business
unit an existing role is used.  Instead, a new agent, manager and
administrator role is recommended, to allow differing layers of
permissions for the same application, without impacting other
applications.  If someone in IT for example works in the OHS work area,
you would not change the permissions on the OHS application for the ITSM
roles, you would instead give that user the ohs_agent role.

Due to this reason, the only people who should have access to the Work
table, should be the system administrator.

Although the concept of application specific self service roles was
considered, it was seen as unnecessary, as if it is a specific sub set
of users within your organization, calling them self service may confuse
the grander concept of self service within the system.  To be
consistent, using the same language across the system ensures that when
other business units talk to each other, they use the same language, as
something as simple as calling the short description something else in
another business unit, may cause confusion when trying to communicate
about the same concept.