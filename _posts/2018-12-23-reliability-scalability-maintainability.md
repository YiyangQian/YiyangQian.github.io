---
title: "Reliability, Scalability and Maintainability"
layout: post
date: 2018-12-23
# image: /assets/images/adsk.JPG
headerImage: false
tag:
- markdown
- components
- extra
category: blog
author: YY
description: Markdown summary with different options
---

# Reliability
Definition: The system should continues to work correctly even in the face of adversity(hardware or software faults, even human error.

### Hardware Faults
- Hard disk crash, RAM becomes faulty, power grid blackout, network cable got unplugged. 
- Response: Add redundancy to the individual hardware components in order to reduce the failure rate of the system.
    - disks being set up in a RAID configuration
    - servers have dual power supplies and hot-swappable CPUs
    - datacenters with batteries and diesel generators for backup power
- This approach cannot completely prevent hardware problems, but can often keep a machine running uniterrupted for years.

### Software Errors
- Software errors are hard to anticipate and because they are correlated across nodes, they tends to cause many more system failures than uncorrelated hardware faults. 
- Software erros are usually in cases when the software is making some kind of assumptions about its environment - and while the assumption is usually true, it eventually stops being true for some reason. 
- No quick solution for this problem. Lot of small things can help:
    - carefully think about assumptions and interactions in the system
    - testing
    - process isolation
    - allowing processes to crash and restart
    - measuring, monitoring and analysing system behavior in production 

### Human Errors
- Humans are known to be unreliable. 
- Approaches to solve: 
    - Design system that minimize opportunities for error. (well-designed abstractions, APIs and interfaces, but this will also restrict peopele, so it is tricky to balance).
    - Sandbox environments to explore safely, with real data without affecting real usres. 
    - Tests throughly at all levels, from unit tests to whole-system integration tests and manual tests. (tests for coner cases rarely arise are especially valuable).
    - Allow quick and easy recovery from human errors. 
    - Set up detailed and clear monitoring, such as performance metrics and error rates. Monitoring can show early warning signals and allow us to check whether any assumptions violated. 

# Scalability
Scalability means a system's ability to cope with increased load.

### Load
- Load can be described with a few numbers that we call load parameters. eg. 
     - requests per second to a web server
     - ratio of reads to writes in a database
     - number of simultaneously active users in a chat room
     - hit cate on a cache
- Twitter Example: user posts a tweert then it should appear in home timelines of his followers
    - Approach 1: global collection of all tweets, query for each timeline.
    - Approach 2: maintain a cache (mailbox) for each user's homeline, and diliver new tweets to followers' mailboxes.

### Performance
- When a system heandling many requests, the response time can vary a lot. Thus the response time is not a single number, but a distribution of values. 
    - Response time: what the client sees: service time + network delays + queueing delays.
    - Latency: duration that the request is waiting to be handled.
- Percentile
    - median is better than average: median shows that half of your requests return in less than 200ms, and half take longer. 50th, p50
    - higher percentiles helps figure out how bad the outliers are. eg 95th, 99th, 99.9th. Most of the response time are faster than this threshold.
        - Amazon describes response time requirements for internal service in terms of the 99.9th percentile. This is because slowest requests are usually from customer with most data, who have made many purchases, and are thus most valuable customers. 
    - percentiles are often used in service level ojectives and service level agreements. 
        - the service is considered to be up if it has a median response time of less than 200 ms and a 99th percentile under 1 s.

### Approaches for coping with load
- Scaling up: vertical scaling, moving to more powerful machine
- Scaling out: horizontal scaling, distribute the load across multiple smaller machines
- In reality, good architectures usually involve a gragmatic mixture: several fairly powerful machines can still be simpler and cheaper than a large number of small virtual machines. 
- It is conceivable that distributed data systems will become the default in the future, even for use cases that don't handle large volumes of data or traffic. 
- Architecture of systems that operate at large scale is usually highly specific to the application. 
- An architecture that scales well for a particular application is built around assumptions of its common operations - the load parameters.

# Maintainability

### Operability: making life easier to keep the system running smoothly
- "good operations can often work around the limitations of bad software, but good software cannot run reliably with bad operations"

### Simplicity: managing complexity
- Symptoms of complexity:
    - explosion of state space
    - tight coupling of modules
    - tangled dependencies
    - inconsistent naming and terminology
    - hacks aimed at solving performance problems
- In complex software, there is a greater risk of introducing bugs when making a change: 
    - hidden assumptions, unintended consequences, and unexpected interactions are more easily overlooked.
- Abastraction: one of the best tools for removing accidental complexity
    - high-level programming languages hide machine code, CPU registers, and syscalls.
    - SQL hides complex and on-disk and in-memory data structures, concurrent requests, and inconsistencies after crashes.

### Evolvability: making changes easier
- requirements for system will keep changing
- Agile 
    - tools and patterns helpful when working in a frequently changing environment
    - TDD, refactoring
