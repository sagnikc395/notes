---
title: Reliable, Scalable and Maintainable Applications 
tags:
  - ddia
  - scalable-applications
  - maintainibility
date: 13/1/25
---
### Primer:
- A data intensive application is typically built from standard building blocks that provide commonly needed functionality. Eg:
    - Store data so that they,or another application, can find it again later -> *(databases)*.
    - Remember the result of an expensive operation, to speed up reads -> *(caches)*.
    - Allow users to search data by keyboard of filter it in various ways -> *(search indexes)*.
    - Send a message to another process, to be handled asynchronously -> *(steam processing)*.
    - Periodically crunch a large amount of accumulated data -> *(batch processing)*.

- There are many database systems with different characteristics, because different applications have different requirements. There are various approaches to caching, several ways of building search indexes, and so on. When building an application, we still need to figure out which tools and which approaches are the most appropriate for the task at hand.

### Thinking about Data Systems:
- Many new tools for data storage and processing have emerged in recent years. They are optimized for a variety of different use caes, and they no longer neatly into traditional categroies.
    - Eg: datastores that are also used as message queues(Redis), and there are message queues with database-like durability gurantees (Apache Kafka). Boundaries between the cateories are becoming blurred.

- Increasingly many applications now have such demanding or wide-ranging requirments that a single tool can no longer meet all of its data processing and storage needs. Instead , he work is broken down into tasks that can be performed efficiently on a single tool, and those different tools are stitched together using application code.
    - Eg: If we have an application-managed caching layer(Memcached), or a full-text search server(ElasticSearch), seperate from your main database, it is normally the application code's responsibility to keep those caches and indexes in sync with the main db.

- When we combine several tools in order to provide a service, the service's API usually hides those implementations details from clients.Now we have essentially created a new , special-purpose data system from smaller, general-purpose components.

### Factors Influencing Design of a Data System:
- Many factors that may influence the design of a data system, including the skills and experience of the people involved, legacy system dependencies, the timescale for delivery, our organization's tolerance of different kinds of risk.

- We focus on 3 concerns that are important in most software systems:
    - *Reliability* -> System should continue to work correctly(performing the correct function at the desired level of performance) even in the face of adversity.
    - *Scalability* -> As the system grows(in data volumes, traffic volumes, or complexity), there should be reasonable ways of dealing with that growth.
    - *Maintainibility* -> Over time, many different people will work on the system and they should all be able to work on it productively.

### Reliability:
- Everybody has a intuitive idea of what it means for something to be reliable or unreliable. For software , typically:
    - The application performs the function that the user expected.
    - It can tolerate the user making mistakes or using the software in unexpected ways.
    - Its performance is good enough for the required use case, under the expected load and data volume.
    - The system pervens any unauthorized access and abuse.

- Things that can go wrong are called faults, and systems that anticipate faults and can cope with them are called as fault-tolerant or resilient. A fault is usually defined as one component of the system deviating from its spec, whereas a failure is when the system as a whole stops providing the required service to the user.

- It is impossible to reduce the probability of a fault to zero; therefore it is usually best to design fault-tolerance mechanism that prevents faults from causing failures.

- Counterintuitively, many critical bugs are actually due to poor error handling, by deliberately inducing faults, we ensure that the fault-tolerance machinery is continually exercised and tested, which can incease our confidence that faults will be handled correctly when they occur naturally.Eg: Choas Monkey from Netflix.

### Hardware Faults:
- Hard Disks crash, RAM becomes faults, power grid has a blackout,someone unplugs wrong network cable. Anyone who has worked with large datacents, can tell that this happens all he time when we have a lot of machines.

- Hard disks are reported as having a mean time to failure(MTTF) of about 10-50 years. Thus,on storage clsuter with 10k disks, we should expect on avg one disk to die per year.

- First reponse:
    - add redundancy to the individual hardware component in order to reduce the failure rate of the system. Disks may be set up in a RAID confiuration, servers may have dual power supplies and hot-swappable CPUs and datacenters may have battries and diesel generators for backup power.

- However , as data volumes and application's computing demands have increased, more application have begun using larger number of machines, which proportionally increases the rate of hardware faults. Moreoever, in some cloud platrofmrs like AWS it is fairly common for vitual machine instances to become unavailable without warning, as the platforms are designed to priorize flexibility and elasticity over single-machine reliablity.

- Move towards a system that can tolerate the loss of entire machines, by usin software fault-tolerance techniques in preference or in addition to hardware redundancy. Such systems also have operational advantages: a single-server system requires planned downtime if we need to reoot the machine, whereas a system that can tolerate machine failure can be patched one node at a time, without downtime of the entire system.

### Software Errors:
- 
