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

- The Story of Some Code: Traditional Silos

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
