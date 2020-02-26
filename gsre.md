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

- These quantifiable metrics become our SLIs. Ideally, you wanted to define SLIs that have a predictable, mostly linear relationship with happiness of your users. The predictability of the relationship is crucial because you'll be making important engineering decisions based on this data.

<p align="center"><img src="images/sre-sli-graph.png" width="400px"></p>

#

**The properties of a good SLI metrics**

- Bad metrics:

  - :x: System metrics

  - :x: Internal state

- Good metrics

  - :white_check_mark: Has predictable relationship with user happiness.

  - :white_check_mark: Shows service is working as users expect it to.

  - :white_check_mark: Expressed as: _good events/valid events_.

  - :white_check_mark: Aggregated over a long time horizon.

- Why is the lower metric better for use as an SLI than the upper one?  

<p align="center"><img src="images/sre-metrics-graph.png" width="500px"></p>

#

**Ways of measuring SLIs**

- The accuracy of your measurement of that experience increases the closer you get to a user's interactions with your system.
So a key engineering decision underlying any SLI is the choice of where and how to measure it. Broadly speaking, there are five ways to measure an SLI and each has their own set of advantages and disadvantages. We'll talk about them in the order of increasing proximity to the user.

<p align="center"><img src="images/sre-measuring-ways.png" width="400px"></p>

- The client-side instrumentation provides far and away the most accurate measure of your user experience and can even help you gauge the reliability of the third parties like CDNs or payment providers in your user journeys. So why isn't this is the default approach? Adjusting the telemetry from your clients can incur significant measurement latency, especially for mobile clients where waking the radio every few seconds to report home, is detrimental to both battery life and user trust. Just like logs processing, this latency makes SLIs based on client instrumentation unsuitable for triggering a short-term operational response. Measuring from the client's perspective also captures a lot of factors that are outside of your direct control, which can lower the signal to noise ratio of prospective SLIs. To give an example, you might be interested to know that mobile clients suffer poor latency and higher error rates, but because you can't do a whole lot about it, you have to relax your SLO targets to accommodate it instead.

#

**Commonly Used SLIs**

**The SLI Menu**

- :arrows_counterclockwise: **Request/Response**

  - Availability

  - Latency

  - Quality

- :clock1: **Data Processing**

  - Coverage

  - Correctness

  - Freshness

  - Throughput

- :inbox_tray: Storage

  - Durability

#

**The SLI Equation**

- **SLI:** **good** events / **valid** events

- :white_check_mark: SLIs fall between 0 and 100%

- :white_check_mark: Consistency makes building common tooling easier

#

**Request/Response SLIs**

- **Availability**

  - The proportion of valid requests served successfully

  - The proportion of minutes a virtual machine was booted and accessible

- **Latency**

  - The proportion of work-queue tasks are completed faster than a threshold

  - The proportion of valid requests served faster than a threshold

<p align="center"><img src="images/sre-latency.png" width="350px"></p>

- **Quality**

  - The proportion of valid requests served without degrading quality

  <p align="center"><img src="images/sre-quality.png" width="350px"></p>

#

**Data processing SLIs**

- **Freshness**

  - The proportion of valid data updated more recently than a threshold

  <p align="center"><img src="images/sre-freshness-batch.png" width="350px"></p>

  <p align="center"><img src="images/sre-freshness-continuous.png" width="350px"></p>

  <p align="center"><img src="images/sre-freshness-shards.png" width="350px"></p>

- **Correctness**

  - The proportion of valid data producing correct output

  <p align="center"><img src="images/sre-correctness.png" width="350px"></p>


- **Coverage**

  - The proportion of valid data processed successfully  

  <p align="center"><img src="images/sre-coverage.png" width="350px"></p>

- **Throughput**

  - The proportion of time where the data processing rate is faster than a threshold

  <p align="center"><img src="images/sre-throughput.png" width="350px"></p>

#

**Managing Complexity**

**"But my system is really complex!"**

You should aim to only have **one to three SLIs** covering each user journey, even if your system and user journeys are relatively complex.

:x: Not all metrics make good SLIs.

:x: More SLIs result in higher cognitive load.

:x: More SLIs lower signal-to-noise ratio...

... and can drive up time to resolution.

- Your metrics still have value!

  - **SLIs:** Something is broken!

  - **Metrics:** _This thing_ is broken!

#

**Managing complexity with aggregation**

<p align="center"><img src="images/sre-ag-table.png" width="350px"></p>

:white_check_mark: Simple aggregation works much of the time

:x: Except when request rates differ significantly

#

**Managing Complexity with bucketing**

<p align="center"><img src="images/sre-buckets.png" width="350px"></p>

#

**Setting Reliable Targets**

**Achievable SLOs**

<p align="center"><img src="images/sre-slo-sli.png" width="350px"></p>

<p align="center"><img src="images/sre-ue.png" width="350px"></p>

:white_check_mark: It's OK to wait and gather data before setting targets!

:white_check_mark: **Achievable** SLOs are ones based on historical data...

:x: ...but assume that users are happy with the status quo...

:astonished: ...without any **evidence** to back up this claim!

#

**Aspirational SLOs**
