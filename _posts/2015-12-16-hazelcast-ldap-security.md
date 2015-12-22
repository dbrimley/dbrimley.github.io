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

Hazelcast has the ability to authenticate users of a cluster and then to authorise their access to data structures and operations based on roles held by a user.  This authentication and authorisation occurs within the cluster when a client connects for the first time.  

### Before we begin...

**You can find the full code samples at my [github repository](http://github.com/dbrimley/hazeldap)**

These features are present in Hazelcast Enterprise, to get started you'll have to grab yourself a trial version from [hazelcast.com](https://hazelcast.com/hazelcast-enterprise-download/trial/).

You'll get two things from the website...

1. A license key.
2. The Hazelcast Enterprise JARS.

#### Configure the License Key

The project samples and hazelcast are bootstrapped using Spring, to configure the license you'll need to edit the **hazelcast-server/src/main/resources/application-context.properties** file.

{% highlight xml %}
hazelcast.group.config.name=hazeldap
hazelcast.group.config.password=hazeldap-password
hazelcast.license.key=<!-- GET LICENCE FROM https://hazelcast.com/hazelcast-enterprise-download/trial/ -->
{% endhighlight %}

#### Add the Enterprise Jars to Maven Repo

Next you'll need to add the enterprise jars you downloaded and place them into your local maven repository.  You can do this using the **maven-install-plugin**

For example if you are installing the 3.5.4 jars to your local maven repo you would execute the following...

{% highlight xml %}
mvn org.apache.maven.plugins:maven-install-plugin:2.5.1:install-file 
-Dfile=/Users/dbrimley/Dev/hazelcast/hazelcast-enterprise-3.6-EA/lib/hazelcast-enterprise-client-3.5.4.jar 
-DgroupId=com.hazelcast 
-DartifactId=hazelcast-enterprise-client 
-Dversion=3.5.4 
-Dpackaging=jar 
-DlocalRepositoryPath=/Users/myName/.m2/repository

mvn org.apache.maven.plugins:maven-install-plugin:2.5.1:install-file 
-Dfile=/Users/dbrimley/Dev/hazelcast/hazelcast-enterprise-3.5.4/lib/hazelcast-enterprise-3.5.4.jar 
-DgroupId=com.hazelcast 
-DartifactId=hazelcast-enterprise 
-Dversion=3.5.4 
-Dpackaging=jar 
-DlocalRepositoryPath=/Users/myName/.m2/repository
{% endhighlight %}

### Introduction to Hazelcaast & JAAS

The entire process is handled with the help of [JAAS (Java Authentication and Authorization Service)](https://en.wikipedia.org/wiki/Java_Authentication_and_Authorization_Service) compliant interfaces.

At a high level a JAAS backed authorisation and authentication process would execute in the following manner...

1. The Subject(Hazelcast Client) attempts to connect to a service, in this case a Hazelcast Cluster.  The Subject provides Credentials when it initially connects.  These Credentials can be anything at all, for example a user name and password or maybe a Binary Token.  

2. The Credentials are passed to a LoginModule, this module is a JAAS interface that is executed by the Hazelcast Cluster when a new client connects.  The implementer of this module may then take the passed Credentials and firstly authenticate the user.  The authentication can be carried out against the security service of their choice.  This could just be a Database table of user names and password or it could be a corporate security solution like LDAP or Active Directory.

3. Once the user has been authenticated they can then be authorised to perform actions on data or execute distributed functions.  This authorisation takes the form of matching roles against actions in hazelcast, for example Joe Bloggs has the role of "Admin" therefore he can update all Maps in the cluster.  The roles are generally stored in the same "security backend" that carried out the Authentication steps.  Again maybe an LDAP or Active Directory store.

The following diagram describes these operations.

![Hazelcast LDAP Security Workflow](/assets/img/hazelcast-ldap-security.png)

## The Example LDAP Secured Hazelcast Cluster

### Client Credentials

When a Client initially connects to a Hazelcast Cluster an optional [Credentials](http://docs.hazelcast.org/docs/latest/javadoc/com/hazelcast/security/Credentials.html) object can be passed.  The Credentials object carries mandatory information such as the Endpoint which is usually the IP Address of the client.  As Credentials are usually passed over the network between a client and a cluster it needs to be serialized.

You can implement Credentials interface directly and then add extra information you wish to pass like a token or use one of the existing classes, such as [UsernamePasswordCredentials](http://docs.hazelcast.org/docs/latest/javadoc/com/hazelcast/security/UsernamePasswordCredentials.html).  We'll use this class for Credentials in our example project, it has the added advantage of implementing [Portable Serialization](http://docs.hazelcast.org/docs/latest/manual/html-single/index.html#portable).  

UsernamePasswordCredentials takes a String Username and a String Password.

**Make sure you use [SSL on client to cluster connections](http://docs.hazelcast.org/docs/latest/manual/html-single/index.html#ssl) when you are sending clear text passwords over the wire.**

{% highlight java %}
package com.hazelcast.security;

import java.io.Serializable;

public interface Credentials extends Serializable {
    String getEndpoint();

    void setEndpoint(String var1);

    String getPrincipal();
}
{% endhighlight %}

Now we have our Credentials object we need to pass it on with our initial Client connection into the Hazelcast cluster, the follow code samples demonstrates this...

{% highlight java %}
ClientConfig clientConfig = new ClientConfig();
clientConfig.setCredentials(new UsernamePasswordCredentials(username, password));
clientConfig.getCredentials().setEndpoint(thisClientIP);
HazelcastInstance hazelcastInstance = HazelcastClient.newHazelcastClient(clientConfig);
{% endhighlight %}

## Enter the JAAS LoginModule!

It's time to introduce the [LoginModule](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jaas/JAASLMDevGuide.html) and configure the Hazelcast Cluster to use it when a client connects.

You can have multiple LoginModules chained together, in this example we've configured just one using Spring Beans...

{% highlight xml %}
    <bean id="hazelcast.instance" class="com.hazelcast.core.Hazelcast" factory-method="newHazelcastInstance">
        <constructor-arg>
            <bean class="com.hazelcast.config.Config">
                ...
                <property name="securityConfig">
                    <bean class="com.hazelcast.config.SecurityConfig">
                        <property name="enabled" value="true"/>
                        <property name="clientLoginModuleConfigs">
                            <list>
                                <bean class="com.hazelcast.config.LoginModuleConfig">
                                    <property name="className"
                                              value="com.craftedbytes.hazelcast.security.ClientLoginModule"/>
                                    <property name="usage" value="REQUIRED"/>
                                    <property name="properties">
                                        <map>
                                            <entry key="userStore" value-ref="userStore"/>
                                        </map>
                                    </property>
                                </bean>
                            </list>
                        </property>
                        ...
                    </bean>
                </property>
            </bean>
        </constructor-arg>
    </bean>
{% endhighlight %}


#### Initialize

Hazelcast first calls the initialize method, this called when the client connection is detected.  Hazelcast passes 4 classes.

1. **Subject** : Is the class that will be populated with Principals (e.g. Roles) upon successful login.
2. **CallbackHandler** : Is used to retrieve the Credentials passed by the client.
3. **SharedState** : Is a Map that can be used to pass state between different LoginModules
4. **Options** : Is used in this instances to pass in helper classes tot he LoginModule, in our case we will be passing in the UserStore which in turn connects to our LDAP server.

{% highlight java %}
public void initialize(Subject subject, 
                       CallbackHandler callbackHandler, 
                       Map<String, ?> sharedState, 
                       Map<String, ?> options) {
    this.subject = subject;
    this.callbackHandler = callbackHandler;
    this.userStore = (UserStore) options.get("userStore");
}
{% endhighlight %}

### Lifecycle Phases

As mentioned above the LoginModule interface has distinct lifecycle methods that are called by Hazelcast.

1. login
2. commit
3. abort
4. logout

We'll look at each of these phases next.

















