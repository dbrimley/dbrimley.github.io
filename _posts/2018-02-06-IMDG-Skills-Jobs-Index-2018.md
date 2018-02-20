---
layout: post
title: "IMDG Skills and Jobs Index 2018"
modified:
categories: blog
excerpt: It's been a year since I last looked at the state of the IMDG job market along with the numbers of reported skilled IMDG engineers. The good news for IMDG vendors are that job postings are up, indicating more business are turning to In Memory Data Grids.
comments: true
image: careers.jpg
date: 2018-02-06T21:34:21+00:00
---

### 2018 In Memory Data Grids resurgent.

IMDG (In Memory Data Grids) have been around for well over a decade now and sit in a product sector that slightly overlaps NoSQL functionality.  IMDGs initially came to the market in the early nougties when web sessions needed to scale past one sticky web-server, these were the days of what was then known as [Tangosol Coherence](https://www.crunchbase.com/organization/tangosol). Since then the main use case for IMDGs has become general in memory caching and compute, where the IMDG sits between a slower persistent store like an RDBMS/Mainframe (or even a NoSQL Database) and the business application. IMDGs also allow distributed computation where functions run in parallel against the data that is distributed across the IMDG cluster.

IMDGs are seeing something of a resurgence in popularity over the past few years as people discover the shortcomings of NoSQL solutions such as [Apache Cassandra](http://cassandra.apache.org/) or [Redis](http://redis.io), IMDGs are much easier to scale on demand and generally provide faster access times than NoSQL products. IMDGs also allow [near caches](http://docs.hazelcast.org/docs/latest-development/manual/html/Performance/Near_Cache/index.html) of data to be stored in the client application that is kept in sync with the central cluster, something that NoSQL does not provide. In many of these cases architects are now placing IMDGs over the top of the NoSQL store. Another area of growth for IMDGs has been as a hub for [Microservices](https://martinfowler.com/articles/microservices.html). IMDGs it turns out are a perfect fit for Microservices that wish to store state and also message between each other.

Last year I was curious to find out about the health of the IMDG job market and also which of the IMDG products were the most popular not only among businesses but also with engineers. I published those February 2017 results in a blog post you can find [here]({{ site.baseurl }}{% post_url 2017-02-16-IMDG-Skills-Jobs-Index-2017 %})

I've run the same searches again on LinkedIn. One where I search for an IMDG product and the number of jobs listed for it worldwide, the other I search for the number of people on LinkedIn who have the IMDG product name somewhere on their profile.

The total numbers of jobs and also people listed with IMDG skills has risen over my 2017 numbers. Now this is not necessarily an accurate way of judging the market place, for example it's possible more business are advertising over last year or possibly LinkedIn indexing and search has become more accurate. That said, the skills count increase should provide at least some direction as to the way IMDG products are headed. So, anecdotally it appears as if IMDG software has become more popular with businesses in the last year.

Onto the findings, it seems as if there is some heavy momentum behind [Hazelcast](http://www.hazelcast.org) as it jumps above [Oracle Coherence](http://www.oracle.com/technetwork/middleware/coherence/overview/index.html) to become the most popular IMDG skill. Hazelcast has seen 1,500 additional people list it on their LinkedIn Profile since last year. Oracle Coherence loses its top spot on this ranking to drop to third, with [Pivotal Gemfire](https://pivotal.io/pivotal-gemfire) / [Apache Geode](http://geode.apache.org/) taking second spot.

Job Postings are up on 2017 with Hazelcast retaining its top spot with nearly double the jobs on offer to its nearest rival Pivotal Gemfire / Apache Geode.

There's nothing scientific about the actual searches performed and they're all easily reproduced for verification.  I've made no attempt to find duplicates in terms of job postings, I've not merged results/counts where an IMDG product is known under two names, an open source and a commercial version.  For example Pivotal Gemfire and Apache Geode. This could give a slight boost to these products.

I've chosen what I consider to be the top 5 IMDG, Four of them are open source and one is proprietary, closed source.

* Hazelcast
* Oracle Coherence
* Gemfire / Apache Geode
* GridGain / Apache Ignite
* JBoss Data Grid / Infinispan

### IMDG Products mentioned in LinkedIn Profiles.

An important statistic and a good indicator of an IMDGs popularity with engineers and businesses alike. This is an indicator of the available talent pool, an important consideration when weighing up IMDG products against each other. This metric alone can have a strong influence on IMDG product selection within businesses.

The big change over last year is the loss of top spot for Oracle Coherence as the most popular IMDG in LinkedIn profiles. It falls to third despite adding a modest number of new profiles. It is overtaken by Hazelcast which rises from second to first, adding 1,500 new profiles to its count, a near 50% increase since 2017. In second up from third comes Pivotal Gemfire / Apache Geode adding 600 new profiles.

![IMDG Profiles Count](/assets/img/imdg-linkedin-profiles.png)

![IMDG Profiles Bar](/assets/img/imdg-linkedin-profiles-bar.png)

![IMDG Profiles Pie](/assets/img/imdg-linkedin-profiles-pie.png)


**Notes:** _Search conducted on 5th February 2018.
Something strange has happened on searches for "apache ignite" on LinkedIn, it only returns 1 profile, where last year there were more than this. Therefore rather than reduce the figures I've left them as per 2017 which was 550 profiles. I'm guessing there is something strange going on with LinkedIn here rather than a decrease in Apache Ignite popularity. The commercial product "gridgain" returned 176 profiles. Try it for yourself, if LinkedIn fixes this I'll change it in this blog post at a future date._

### IMDG Product Job Listings

Job listings are another great indicator of IMDG popularity and as mentioned, this metric is up from 2017 for all of the IMDG products we searched. No movement at the top, with Hazelcast staying in place as the IMDG with most job opportunities. Pivotal Gemfire / Apache Geode retains its second spot with Oracle Coherence in third. Anecdotally I'm seeing many more FTSE 100 and Fortune 500 companies advertising for IMDG positions now over 2017.

![IMDG Jobs Count](/assets/img/imdg-linkedin-jobs.png)

![IMDG Jobs Bar](/assets/img/imdg-linkedin-jobs-bar.png)

![IMDG Jobs Pie](/assets/img/imdg-linkedin-jobs-pie.png)

Notes : LinkedIn Search for jobs mentioning the product keywords. Where a product is known by 2 names results have been combined. This could advantage these products as the same job may be double counted. Jobs could be listed more than twice if they being advertised by agencies.

Search conducted on 5th February 2018

### Conclusion

In conclusion most of the IMDG vendors should feel very happy, it looks as if demand is increasing for In Memory Data Grids. There are many reasons for the increase, the drive towards micro-service architectures and the need for flexible cloud based systems to name two. It could also be the realization that NoSQL Databases are not quite the one stop data solution they were thought to be. It appears as if IMDGs are now taking a place in hybrid architectures that include NoSQL Databases alongside Messaging and Streaming products such as [Apache Kafka](https://kafka.apache.org/) and [Hazelcast Jet](http://jet.hazelcast.org)

Let me know what you think in the comments section below. Does this all tally with your current experiences of the IMDG job market? If you're an Architect, how are you using In Memory Data Grids?




