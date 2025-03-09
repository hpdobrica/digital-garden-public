---
title: Fault
notetype: feed
date: 04-02-2025
---

Anything that can go wrong with software (or hardware) is called a fault. A systems that anticipates faults and can cope with them is called a fault-tolerant or resilient system.

It's important to note that faults are always expected and it's impossible to have a system which doesn't experience faults at some level. Because of this, we should aim for our systems to be able to deal with faults when they arise, so that we can prevent the faults to grow into [[Software Failure]].

If a system is designed to be fault tolerant, it might be a good idea to continually introduce deliberate faults to make sure that it's able to deal with them in a proper way.

Hardware faults are mitigated by redundancy (e.g. mutliple hard disks in RAID setup), but further even loss of entire machines can be mitigated with software fault-tolerance techniques (think [[K8S Node]] dying).

Software faults can be more tricky to detect and mitigate as they can happen across the whole system (vs on a faulty node). They are caused by software making some assumption about its environment which at one point stops being true. This allows such bugs to be dormant for a long time before they start causing trouble, making them even harder to debug.

Operation errors like misconfiguration are the leading cause of failures, while software and hardware faults take up only 10-25% market share. Designing systems that are resilient against human error is done by focusing on minimizing the opportunities for error during human operation. Think of interfaces that guide user towards doing the right thing, and away from doing the wrong thing. It's important to be aware that if a system's interface is too restrictive, pesky operators will find ways to circumvent the limitations, leading to possibly more danger of error, so the solution might require finding the right balance between restriction and power.

Another powerful strategy to prevent human faults leading to failures is to isolate the place where fault is most likely to happen from the place where the fault is most likely to cause a failure. In other words, well-maintained, isolated non-production environments can give operators a safe place to experiment without causing an outage.

For dealing with human errors that can't be prevented, we need to have systems in place to mitigate the potential failures as fast as possible. Examples of this are easy rollbacks of configuration changes and gradual rollouts of new code.

-----

Status: #📥

References:
- [[Book - Designing Data Intensive Applications]] ([Source](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321))