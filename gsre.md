## Site Reliability Engineering: Measuring and Managing Reliability <img src="images/glogo.jpg" width="30px">

### Course Structure

- Targeting Reliability

- Operating for Reliability

- Choosing a Good SLI

- Developing SLOs and SLIs

- Quantifying Risks to SLOs

- Consequences of SLO Misses

#

### Course introduction: What is SRE? How does It differ from DevOps?

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

**Reliability in the cloud**

- 28-day error budget **99.9%** = 40 min

- 28-day error budget **99.99%** = 4 min

#

### Why are SLOs important for your organization?

**How SLOs help you balance operational and project work**

***Question:*** _What is the right level of reliability for the system you support?_

- SLOs with executive support turn arguments into data-driven decisions.

- SLOs can drive Ops response and long-term priorization.

#  

### Targeting Reliability

**Three Principles**

  1. What to promise to whom

  2. What metrics to measure

  3. How much reliability is good enough

#  

**SLOs vs SLAs**

- **SLA:** Service Level Agreement

  - Agreements with customers about the reliability of your service

- **SLO:** Service Level Objectives

  - Thresholds that catch an issue before it breaches your SLA

#

**The Happiness Test**

_There are many characteristics of reliable services. But the common theme is that users perceive a service to be unreliable
when it fails to meet their expectations, whatever those may be. Users whose expectations have not been met tend to get grumpy. So we think a good rule of thumb to help you set SLO targets is what we call the happiness test.
The test states that services need target SLOs that capture the performance and availability levels that if barely met would keep a typical customer happy. Simply put, if your service is performing exactly at its target SLOs, your average user would be happy with that performance. If it were any less reliable, you'd no longer be meeting their expectations and they would become unhappy. If your service meets target SLO, that means you have happy customers. If it misses the target SLO, that means you have sad customers._

<p align="center"><img src="images/sre-ht.png" width="400px"></p> 
