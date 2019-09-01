# <img src="images/la.png" width="30px"> DevOps Essentials <img src="images/la.png" width="30px">

_Based on Linux Academy's Course DevOps Essentials_

## Introduction <img src="images/la.png" width="30px">

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

## DevOps Culture <img src="images/la.png" width="30px">

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

- _Traditional Silos - What Went Wrong?_

  - Dev and Ops are black boxes to each other, which leads to finger pointing:

    - Because Ops is a black box, Devs don´t really trust them

    - And Ops doesn´t really trust Dev

  - Dev and Ops have different priorities, which pits them against each other:

    - Ops views Devs as breaking stability

    - Devs see ops as an obstacle to delivering their code

  - Even if they WANT to work together:

    - Dev is measured by delivering features, which means deploying changes

    - Ops is measured by uptime, but changes are bad for stability

- _Downsides of Traditional Silos_

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

  - _DevOps - What Went Right?_

    - Dev and Ops worked together to build a robust way of changing code quickly and reliably:

      - Both Dev and Ops worked together to prioritize both speed of delivery and stability

    - Automation led to consistency:

      - Building, testing, and deploying happened the same way every time

      - Building, testing, and deploying happened much more quickly and more often

    - Good monitoring, plus the swift deployment process, ensured problems could be fixed even before users noticed them:

      - Dev and Ops worked together up front to build good processes

      - Even though a code change caused a problem, users experienced little or no downtime

  - _Why do DevOps?_

    - Happier teams:

      - Tech employees tend to be happier doing DevOps than under traditional silos

      - More time innovating and less time putting out fires

      - Devs don´t feel like they have to fight to get their work out there

      - Operations people don´t have to fight Dev to keep the system stable

    - Happier customers:

      - DevOps lets you give customers the features they want quickly

      - And you don´t have to sacrifice stability to do it

      <p align="center"><img src="images/devops-dev-ops.png" width="550px"></p>

## DevOps Concepts an Practices <img src="images/la.png" width="30px">

**Build Automation**

- _What is build automation?_

  - **Build automation:** automation of the process of preparing code for deployment to a live environment.

  - Depending on what languages are used, code needs to be compiled, linted, minified, transformed, unit tested, etc.

  - Build automation means taking these steps and doing them in a consistent, automated way using a script or tool.

  - The tools of build automation often differ depending on what programming languages and frameworks are used, but, they have one thing in common: **automation**!

- _What does build automation look like?_

  - Usually, build automation looks like running a command-line tool that builds code using configuration files and/or scripts that are treated as part of the source code.

  - Build automation is independent of an IDE.

  - Even if you can build within the IDE, it should be able to work the same way outside of the IDE.

  - As much as possiblem build automation should be agnostic of the configuration of the machine that it is built on.

  - Your code should be able to build on someone else's machine the same way it builds on yours.

- _Why do build automation?_

  - Build automation is **fast** - Automation handles tasks that would otherwise need to be done manually.

  - Build automation is **consistent** - The build happens the same way every time, removing problems and confusion that can happen with manual builds.

  - Build automation os **repeatable** - The build can be done multiple times with the same result. Any version of the source code can always be transfomed into deployable code in a consistent way.

  - Build automation is **portable** - The build can be done the same way on any machine. Anyone on the team can build on their machine, as well as on shared build server. Building code doesn't depend on specific people or machines.

  - Build automation is more **reliable** - There will be fewer problems caused by bad builds.

#

**Continuous Integration**

- _What is Continuous Integration?_

  - **Continuous Integration (CI):** the practie of frequently merging code changes done by developers.

  - Traditionally, developers would work separately, perhaps for weeks at a time, and the merge all of their work together at the end in one large effort.

  - Continuous integration means merging constantly throughout the day, usually with the execution of automated tests to detect any problems caused by merge.

  - Merging all the time could be a lot of work, so to avoid that it should be **automated**!

- _What does Continuous Integration look like?_

  - Continuous integration is usually done with the help of a **CI server**.

  - When a developer commits a code change, the CI server sees the change and automatically performs a build, also executing automated tests.

  - This occurs multiple times a day.

  - If there is any problem with the build, the CI server immediately and automatically notifies the developers.

  - If anyone commits code that "breaks the build" they are responsible for fixing the problem or rolling back their changes immediately so that other developers can continue working.

- _Why do Continuous Integration?_

  - **Early detection** of certain types of bugs - If code doesn't compile or an automated test fails, the developers are notified and can fix it immediately. The sooner the bugs are detected, the easier they are to fix.

  - **Eliminate the scramble** to integrate just before a big release - The code is constantly merged, so there is no need to do a big merge at the end.

  - Makes **frequent releases** possible - Code is always in a state that can be deployed to production.

  - Makes **continuous testing** possible - Since the code can always be run, QA testers can get their hands on it all throughout the development process, not just at the end.

  - Encourages **good coding practices** - Frequent commits encourages simple, modular code.

#

**Continuous Delivery and Continuous Deployment**

- _What is Continuous Delivery?_

  - **Continuous Delivery (CD):** the practice of continuously maintaining code in a deployable state.

  - Regardless of whether or not the decision is made to deploy, the code is always in a state that is able to be deployed.

  - Some use the terms continuous delivery and continuous deployment interchageably, or simply use the abbreviation CD.

- _What is Continuous Deployment?_

  - **Continuous Deployment:** the practice of frequently deploying small code changes to production.

  - Continuous delivery is keeping the code in a deployable state. Continuous deployment is actually doing the deployment frequently.

  - Some companies that do continuous deployment deploy to production multiple times a day.

  - There is no standard for how often you should deploy, but in general, the more often you deploy the better!

  - With continuous deployment, deployments to production are routine and commonplace. They are not a big, scary event.

- _What does Continuous Delivery and Continuous Deployment look like?_

  - Each version of the code goes through a series of stages such as automated build, automated testing, and manual acceptance testing. The result of this process is an artifact or package that is able to be deployed.

  - When the decision is made to deploy, the deployment is **automated**. What the automated deployment looks like depends on the architecture, but no matter what the architecture is, the deployment is automated.

  - If a deployment causes a problem, it is quickly and reliably **rolled back** using an automated process (hopefully before a customer even noices the problem!).

  - Rollbacks aren't a big deal because the developers can redeploy a fixed version as soon as they have one available.

  - No one grips their desk in fear during a deployment, even if the deployment does cause a problem.

- _Why do Continuous Delivery and Continuous Deployment?_

  - **Faster time-to-marke** - Get features into the hands of customers more quickly rather than waiting for a lengthy deployment process that doesn't happen often.

  - **Fewer problems caused by the deployment process** - Since the deployment process is frequently used, any problems with the process are more easily discovered.

  - **Lower risk** - The more changes are deployed at once, the higher the risk. Frequent deployments of only a few changes are less risky.

  - **Reliable rollbacks** - Robust automation means rollbacks are a reliable way to ensure stability for customers, and rollbacks don't hurt developers because they can roll forward with a fix as soon as they have one.

  - **Fearless deployments** - Robust automation plus the ability to rollback quickly means deployments are commonplace, everyday events rather than big, scary events.    
