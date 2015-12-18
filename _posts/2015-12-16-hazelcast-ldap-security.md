---
layout: post
title: "Hazelcast LDAP Security"
modified:
categories: blog
excerpt: Hazelcast has the ability to authenticate users of a cluster and then to authorise their access to data structures and operations based on roles held by a user.
tags: []
comments: true
image: ldap.png
date: 2015-12-16T13:33:13+00:00
---

## Introduction

Hazelcast has the ability to authenticate users of a cluster and then to authorise their access to data structures and operations based on roles held by a user.  This authentication and authorisation occurs within the cluster when a client connects for the first time.

The entire process is handled with the help of [JAAS (Java Authentication and Authorization Service)](https://en.wikipedia.org/wiki/Java_Authentication_and_Authorization_Service) compliant interfaces.

At a high level a JAAS backed authorisation and authentication process would execute in the following manner...

1. The Subject(Hazelcast Client) attempts to connect to a service, in this case a Hazelcast Cluster.  The Subject provides Credentials when it initially connects.  These Credentials can be anything at all, for example a user name and password or maybe a Binary Token.  

2. The Credentials are passed to a LoginModule, this module is a JAAS interface that is executed by the Hazelcast Cluster when a new client connects.  The implementer of this module may then take the passed Credentials and firstly authenticate the user.  The authentication can be carried out against the security service of their choice.  This could just be a Database table of user names and password or it could be a corporate security solution like LDAP or Active Directory.

3. Once the user has been authenticated they can then be authorised to perform actions on data or execute distributed functions.  This authorisation takes the form of matching roles against actions in hazelcast, for example Joe Bloggs has the role of "Admin" therefore he can update all Maps in the cluster.  The roles are generally stored in the same "security backend" that carried out the Authentication steps.  Again maybe an LDAP or Active Directory store.

The following diagram describes these operations.

![Hazelcast LDAP Security Workflow](/images/hazelcast-ldap-security.png)

## The Example LDAP Secured Hazelcast Cluster

### Client Credentials

When a Client initially connects to a Hazelcast Cluster an optional [Credentials](http://docs.hazelcast.org/docs/latest/javadoc/com/hazelcast/security/Credentials.html) object can be passed.





