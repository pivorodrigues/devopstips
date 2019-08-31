# DevOps Essentials

_Based on Linux Academy's Course DevOps Essentials_

#

## Introduction

**What is DevOps?**

- Defining DevOps

  - DevOps = **Dev** (Development) + **Ops** (Operations)

  - Different people define DevOps in a variety of ways

  - _"DevOps is a software engineering Culture and Practice that aims at unifying software development (Dev) and software operation (Ops)..."_

  - _DevOps aims at shorter development cycles, increased deployment frequency, more dependable releases, in close alignment with business objectives."_ (Wikipedia, 2018)

  - DevOps is first a **Culture** of colaboration between developers and operations people

  - This culture has given rise to a set of **Practices**

  - DevOps is a grassroots movement, by practitioners, for practitioners

#

**DevOps Is NOT...**

- DevOps is NOT tools, but **Tools** are essential to success in DevOps

- DevOps is NOT a standard

- DevOps is NOT a product

- DevOps is not a job title

#

**Agile Software Development**

- DevOps grew out of Agile software development movement

- Agile seeks to develop software in small, frequent cycles in order to deliver functionality to customers quickly and quickly respond to changing business goals

- DevOps and Agile often go hand-in-hand

#

## DevOps Culture

**The Goals of DevOps**

- DevOps Culture

  - DevOps Culture is about **collaboration** between Dev and Ops.

  - Under the traditional separation between Dev and Ops, Dev and Ops have **different** and **opposing** goals.

  - With DevOps, Dev and Ops work together and share the same goals.

- With DevOps:

  - Dev and Ops are playing on the same team

  - Dev and Ops share the same goals

  - The goals include things like:

    - Fast time-to-market (TTM)

    - Few production failures

    - Immediate recovery from failures

- DevOps is about Dev and Ops work together.

- In a DevOps culture, devs care about stability as well as speed, and ops care about speed as well as stability.

- The traditional roles of developers and operational engineers can even become blurred under DevOps.

- Instead of "throwing code over the wall", dev and ops work together to create and use tools and processes that support both speed and stability.

- DevOps recognizes that dev and ops are more powerfull when they are together.

#

**A Story of DevOps vs Traditional Silos**

- The Story of Some Code: **Traditional Silos**

  - Devs write code

  - _"throw it over the wall"_ to QA

  - Code bounces back and forth between Dev and QA as QA discovers problems and Devs fix them

  - Finally, it is ready for production

  - QA/Dev _"throws the code over the wall"_ to Operations

  - Oh No! There´s a problem. Ops throws it back over the wall to Dev

    - Each group´s domain is a "black box" to the other groups

    - _"Our systems are fine; It´s your code!"_

    - _"But the code works on my machine!"_

- Traditional Silos - What Went Wrong?

  - Dev and Ops are black boxes to each other, which leads to finger pointing:

    - Because Ops is a black box, Devs don´t really trust them

    - And Ops doesn´t really trust Dev

  - Dev and Ops have different priorities, which pits them against each other:

    - Ops views Devs as breaking stability

    - Devs see ops as an obstacle to delivering their code

  - Even if they WANT to work together:

    - Dev is measured by delivering features, which means deploying changes

    - Ops is measured by uptime, but changes are bad for stability

- Downsides of Traditional Silos

  - "Black boxes" lead to finger pointing

  - Lengthy process means slow time-to-market

  - Lack of automation means things like builds and deployments are inconsistent

  - It takes a long time to identify and fix problems

  <p align="center"><img src="images/devops-traditional-silos.png" width="550px"></p>

- The Story of Some Code: **DevOps**

  - Devs write code

  - Code commit triggers automated build, integration, and tests

  - QA can get their hands on it almost immediately

  - Once it is ready, kick off an automated deployment to production

  - Since everything is automated, it is much easier to deploy while keeping things stable

  - Deployments can occur much more frequently, getting features into the hands of customers faster

  - Oh no! The latest development broke something in production!

    - Fortunately, automated monitoring notified the team immediately

    - The team does a rollback by deploying the previous working version, fixing the problem quickly

    - An hour later, the dev team was able to deploy a fixed version of the new code

  - DevOps - What Went Right?

    - Dev and Ops worked together to build a robust way of changing code quickly and reliably:

      - Both Dev and Ops worked together to prioritize both speed of delivery and stability

    - Automation led to consistency:

      - Building, testing, and deploying happened the same way every time

      - Building, testing, and deploying happened much more quickly and more often

    - Good monitoring, plus the swift deployment process, ensured problems could be fixed even before users noticed them:

      - Dev and Ops worked together up front to build good processes

      - Even though a code change caused a problem, users experienced little or no downtime

  - Why do DevOps?

    - Happier teams:

      - Tech employees tend to be happier doing DevOps than under traditional silos

      - More time innovating and less time putting out fires

      - Devs don´t feel like they have to fight to get their work out there

      - Operations people don´t have to fight Dev to keep the system stable

    - Happier customers:

      - DevOps lets you give customers the features they want quickly

      - And you don´t have to sacrifice stability to do it

      <p align="center"><img src="images/devops-dev-ops.png" width="550px"></p>

#

## DevOps Concepts an Practices

**Build Automation**

- What is build automation?

  - **Build automation:** automation of the process of preparing code for deployment to a live environment.

  - Depending on what languages are used, code needs to be compiled, linted, minified, transformed, unit tested, etc.

  - Build automation means taking these steps and doing them in a consistent, automated way using a script or tool.

  - The tools of build automation often differ depending on what programming languages and frameworks are used, but, they have one thing in common: **automation**!

- What does build automation look like?  

  - Usually, build automation looks like running a command-line tool that builds code using configuration files and/or scripts that are treated as part of the source code.

  - Build automation is independent of an IDE.

  - Even if you can build within the IDE, it should be able to work the same way outside of the IDE.

  - As much as possiblem build automation should be agnostic of the configuration of the machine that it is built on.

  - Your code should be able to build on someone else's machine the same way it builds on yours.

- Why do build automation?

  - Build automation is **fast** - Automation handles tasks that would otherwise need to be done manually.

  - Build automation is **consistent** - The build happens the same way every time, removing problems and confusion that can happen with manual builds.

  - Build automation os **repeatable** - The build can be done multiple times with the same result. Any version of the source code can always be transfomed into deployable code in a consistent way.

  - Build automation is **portable** - The build can be done the same way on any machine. Anyone on the team can build on their machine, as well as on shared build server. Building code doesn't depend on specific people or machines.

  - Build automation is more **reliable** - There will be fewer problems caused by bad builds.
