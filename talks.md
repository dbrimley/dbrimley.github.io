---
layout: default
title: talks
---

### Talks

I've been lucky enough to speak at a number of conferences and user groups around the world. I usually speak about In Memory Data Grids like Hazelcast and JCache (JSR107). I can also give talks on the IMDG product landscape comparing and contrasting Hazelcast, Coherence and Gemfire.

Below you'll find links to my talks, some with video.

___

# Docklands London Java User Group (November 2015) - Distributed Java Systems in Minutes with 

[Slides](http://www.docklandsljc.uk/presentations/2015/DavidBrimley-Hazelcast.pdf)
[Video](http://www.docklandsljc.uk/presentations/2015/DavidBrimley-Hazelcast.mp4)

Do you want to have quick access to a Java Map that can store terabytes of data? How about if we make the Map partitioned across multiple JVM for fault tolerance and scalability? We’ll also make it in-memory so access is fast.

In this talk we’ll look at how you can use familiar data structures and services such as Maps, Sets, Lists, Queues and Topics in a distributed and highly scalable manner. We’ll be using Hazelcast, which is an open-source, Apache 2 licensed, in-memory data grid. Hazelcast has a very shallow learning curve, we’ll have a distributed system running in minutes. You'll find that the API is a piece of cake. It is regular Java Collections and Concurrency API, but distributed. Now all your data is stored in memory you'll also discover how to run various distributed compute operations over it, such as Query, Aggregations and Map Reduce.

I also gave this talk at 1 other user group :-

#### Brighton Java User Group - July 2015.

___

# Devoxx UK 2015 : Gimme Caching - The Distributed JCache(JSR107) Way

[Parleys Video](https://www.parleys.com/tutorial/gimme-caching-distributed-jcache-jsr107-way)

Howdy Folks, let me tell you a story.

Once upon a time, we're talking about the year 2001, a few people had an amazing idea. They were thinking about something that would change the world, it would make the world easy and give programmers almost unlimited power! It was simply referred to as JSR 107, one of the least things to change in the future. But these dreamers were way ahead of their time and nothing really happened. So time passed by and by and by and over the years it was buried in the deep catacombs of the JCP. Eventually, in 2011 two brave knights took on the fight and worked themselves through all the riddles, to complete their quest in 2014. You'll know what I'm talking about, they called it the "Java Caching API" or in short "JCache".

A software system cannot possibly be imagined without Caching today and it was time for a standard. No matter if you want to cache database, HTML or results of long running calculations, new systems have to reach a critical mass to be successful. Elevator pitch : JSR107 does for Caching what JDBC did for Database lock-in. Now dev to JSR107 and choose the Caching provider of your choice. Lets take a look together with coding samples.

I also gave this talk at 2 other conferences :-

#### QCon UK 2015 : JCache(JSR107) The standard for Java Caching, It's finally here!

[Slides Keynote](http://qconlondon.com/london-2015/system/files/presentation-slides/JCache%20-%20It's%20Finally%20Here.key)

#### Java Barcelona Conference 2015 : Java Caching API:  JCache

___

# Devoxx UK 2014 : High Performance In-Memory Java with Open Source

[PowerPoint Slides](https://www.parleys.com/tutorial/high-performance-in-memory-java-open-source)
[Parleys Video](https://www.parleys.com/tutorial/high-performance-in-memory-java-open-source)

In 2005 Moore’s Law effective came to an end for single Von Neumann processor architecture, and the industry shifted to massively multicore. How do we tap into hundreds of distributed cores without breaking the elegant programming model of the Java VM? As Java advances, we improve the balance between speed, power and simplicity and more advanced technologies become available in open source. NoSQL has been a revolutionary movement both against the closed and proprietary nature of SQL databases as well as a direct attack on the complexity of navigating the impedance mismatch between Java Objects and Relational Databases. What if there were an open source way to get distributed in-memory performance and elastic scalability delivered as a Java Library which you could use with Hadoop, NoSQL, Traditional SQL RDBMS, Standalone (no DB) or in any architecture of your choice?

Whether you are building big data analytics applications or elastically scalable web apps, this talk will demonstrate how to parallelize in memory data processing using Hazelcast and it’s underlying distributed data structures. With a quick introduction into the different terms and some short live coding examples we will make the journey into distributed computing. We use Hazelcast as an example as it is a Java based Open Source, Apache 2 licensed project.




