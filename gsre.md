## Site Reliability Engineering: Measuring and Managing Reliability <img src="images/glogo.jpg" width="30px">

### Course Structure

- Targeting Reliability

- Operating for Reliability

- Choosing a Good SLI

- Developing SLOs and SLIs

- Quantifying Risks to SLOs

- Consequences of SLO Misses

#

### What is SRE? How does It differ from DevOps?

**Whats the difference between DevOps and SRE? (class SRE implements DevOps)**

- **DevOps Objectives:**

  - Reduce Organization Silos

  - Accept Failure as Normal

  - Implement Gradual Change

  - Leverage Tooling and Automation

  - Measure Everything

- **SRE Objectives:**

  - Share ownership

  - SLOs and Blameless PMs

  - Reduce costs of failure

  - Automate this year's job away

  - Measure toil and reliability

#

### Who are CREs (Customer Reliability Engineering)? How can they help you be more reliable?

**CRE's Three Reliability Principles**

- **1.** Reliability is the most important feature

- **2.** Users, not monitoring, decide reliability

- **3.** Well-engineered...

  - _software_ = 99.9%

  - _operations_ = 99.99%

  - _business_ = 99.999%

The Customer Reliability Engineering team was formed to fulfill this goal by taking the lessons learned across many SRE teams at Google, and helping customers apply them to their own organizations and systems.

The foundation of CRE rests on three guiding principles, which we want to convince you of in this course.
Our first principle is that the most important feature of any system is its reliability. We think this is probably the easiest one to convince you of. After all, if your customers are unable to use the services you're providing, they can't take advantage of any of the features you've so painstakingly built forth.
On the other hand, this doesn't mean that the system should never fail it's users. This is a costly and often unreachable target to set.

A more realistic goal is that the system should meet the expectations of its users and strive to maintain their trust.
Most people are used to, and will happily put up with, a small amount of isolated failure from internet facing systems.
Due to the nature of modern networks, it is often very difficult for a consumer to pinpoint where the failure occurred.
But a widespread or repeated outages can quickly draw unwanted notoriety. You can easily lose the trust and respect of your user base, and in turn, this can have disastrous consequences for your business as competitors snap up dissatisfied current users,
and poor reputation slows or even halts the acquisition of new ones.
If your system must show it is meeting its users expectations of reliability, then you have to measure their experience of its reliability. If your users perceive your service to be unreliable, then it is not meeting their expectations, no matter what your logs and metrics say.

Imagine your support team trying to tell an unhappy user that their problem didn't actually exist because your monitoring systems
had not detected anything wrong with your system. That's not a conversation that's ever going to end well. Our second principle states this clearly. Our monitoring does not decide our reliability, our users do. Our third and final principle concerns the pursuit of ever increasing reliability. We believe that architecting a system carefully and following best practices for reliability, like running in multiple globally distributed regions, means that the system has the potential to achieve three nines over a long time horizon. To reach four nines, it's not enough to have talented developers and well-engineered software.
You also need an operations team whose primary goal is to sustain system reliability through both reactive, like well-trained incident response and proactive engineering, things like removing bottlenecks, automating processes, and isolating failure domains. Everyone assumes that they'll need five nines at first. After all, reliability is the most important feature of a system. But reaching these levels of reliability actually requires sacrificing many other aspects of the system, like flexibility and release velocity. Every component must be automated such that changes are rolled out gradually and failures are detected quickly and rolled back without human involvement. Each additional nine makes your system 10 times more reliable than before. But as a rough rule of thumb, it also costs your business 10 times more. Engineering a system to have reliability as its top priority means making many hard choices with wide ranging consequences to the business, and in most cases, the cost-benefit analysis just doesn't add up. In the next video, we'll talk through how these principles and the inexorable consequences of downtime math,
combined with cloud services, led to the creation of CRE. 

**Reliability in the cloud**

- 28-day error budget **99.9%** = 40 min

- 28-day error budget **99.99%** = 4 min

#

### Why are SLOs important for your organization

**How SLOs help your business make decisions**

- _SLO: Service Level Objective_

#  
