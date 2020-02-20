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

#

**How do we measure reliability?**

- Measuring Reliability - Example: Netflix Service

  - Time to start playing

  - No interruptions or issues with playback

- Time to start playing = Latency

  - SLIs, like request latency, are a quantitative measurement or metric of a user experience.

- Error rate = ratio errors or successes/total requests

or

- Error rate = errors or successes/throughput

- SLI: **good** events / valid events

- _How do you set SLOs for your SLIs?_

  - An SLO is just a target that you get to pick, so once you've decided on that target, you measure the performance of the SLIs against it over a period of time. Such as 28 days, last quarter, etc. Depending on what our target SLO is, our SLI will instantly tell us whether or not a certain point in time was good or bad.

#

**How Reliable Should a Service Be? Setting Targets for Reliability**

- **100% is Wrong**

  - If you're trying to run your service much more reliably than it needs to be, you're slowing down development velocity for features that will make your customers happier, for a minor increase in reliability.

  <p align="center"><img src="images/sre-measure-slo.png" width="400px"></p>

- **Iteration of SLOs is important**

  <p align="center"><img src="images/sre-iteration-slo.png" width="400px"></p>

#

### Operating for Reliability

**When Do We Need to Make a Service More Reliable? Error Budgets**

  - An Error Budget is basically the inverse of availability, and it tell us how unreliable your service is **allowed** to be.

  - 99.9% success = 0.1% failure

  - Tolerable errors accommodate:

    - Rolling out new software versions

    - Releasing new features

    - Planned Downtime

    - Inevitable hardware failures

  - 0.1% unavailability x 28 days = 40.32 mins (downtime per month)

  - ***Benefits:***

    - Common incentives for Devs and SREs :white_check_mark:

    - Dev team can self-manage risk :white_check_mark:

    - Unrealistic goals become unattractive :white_check_mark:

#

**Trading off Reliability Against Features**

**Everything is a trade-off**

- 99% reliability :arrow_right: (10x effort) 99.**9**% :arrow_right: (10x effort) :arrow_right: 99.9**9**%

- Align Incentives

  - :white_check_mark: Devs can take risks and push more quickly

  - :white_check_mark: SRE team can work more proactively

- Effective SLOs

  - :white_check_mark: Have executive buy-in

  - :white_check_mark: Have consequences

  - :white_check_mark: Are accurately measured?

#

**Error budgets: advanced concepts**

**Advanced Techniques**

- :white_check_mark: Dynamic release cadence

  - _Based on remaining error budget_

- :white_check_mark: "Rainy Day" fund

  - _Covers unexpected events_

- :white_check_mark: Error budget-based alerts

  - _Exhaustion rate drives alerting_

- :white_check_mark: "Silver Bullets"

  - _For critical new features_

#

**How Do We Make a Service More Reliable**

**Axes of improvement**

<p align="center"><img src="images/sre-ttd-ttr.png" width="600px"></p>

<p align="center"><img src="images/sre-formula.png" width="400px"></p>

- Improve reliability by:

  **1.** Reducing detection time

    - :arrow_down: time-to-detect / TTD

  **2.** Reducing repair time

    - :arrow_down: time-to-resolution / TTR

  **3.** Reducing impact %

    - :arrow_down: users/functionality

  **4.** Reducing frequency

    - :arrow_down: time-to-failure/TTF

#

**Operational approach to increase reliability**

- Report on uneven error budget spend

- Provide input on achieving targets

- Standardize Infrastructure

- Consult on system design

- Build safe release and rollback

- Author postmortens

- Use phased rollouts

#

**Module Summary**

1. Define your problem space: SLO and SLIs.

2. Make your system as reliable as it must be, but no more.

3. Error budgets are your primary basis of communication.

4. SLOs are not set in stone forever.

5. The team relationship has to be strong to make this work.

#

### Choosing a Good SLI

**Metrics and Measurement**

**User happiness in metric form**

- If we can find a way of quantifying the website does not load or this website is too slow from our monitoring data, we can use this data to approximate how happy or unhappy our users are in aggregate.

<p align="center"><img src="images/sre-happy-unhappy.png" width="400px"></p>

- 
