---
layout: default
title: "Software Engineering: Project management_theory"
date: 2022-02-12 21:35:00
categories: Software Engineering
---

### Creating a viable software plan

- Software scope describes..

  - Fuctions and features to be delivered to end-user
  - Data I/O
  - Content presented to users of using the software
  - Performance, constraints, interfaces, and reliability that bound the system

- Scope is defined using one of two techiques
  - A narrative description of software scope is developed agter communication with all stakeholders
  - A set of use-cases is developed by end-user

<em> Problem-Based Estimation </em>

- Baseline productivity metrics: LOC (Line Of Code) and FP (Function Points) data are used in two ways during software project estimation:
  - As estimation variables to size each element of the software
  - As baseline metrics collected from past projects and used with other variable to develop cost and effort projections

### LOC-Based Estimation

- Represent the size of the problem

- Average productivity for the system: 620 LOC/pm
- Burdened labor rate $8000 per month
  =>
- Cost per line of code is $13 (Labor rate / AvProductivity)
- Based on LOC estimates and historical data
  - estimated project cost is ? $13 \* Estimated lines of code (33200) = $431000
  - estimated effort is ? 33200 / 620 = 53.54 = 54 months
    OR 431000/8000 = 53.875 = 54 months

### FP-Based Estimation

- To compute the FP equation:

count total _ [0.65 + 0.01 _ (The sum of complexity factors)]

e.g. FP count total is 320, The sum of the 14 complexity factors is 52
If the historic cost per FP is $1230,
total estimated project cost and estimated effort?

1. FP equation = count total _ [0.65 + 0.01 _ sum of the complexity factors]
   [0.65 + 0.01 * 52] = 1.17,
   320 \* 1.17 = 375

   \*_ total estimated project cost = FP equation _ historic cost per FP
   Estimated cost = total cost / Burdened labor rate

### Use-case point estimation

- Based on the use-case diagram of the project
- Good thing is that each use case represents your functions and scenario (whole scope of the project)

UCP (Use case point)

UUCW - Unadjusted sum of use case weights
UAW - Unadjusted sum of Actor Weight
TCF - Technical Comlexity 13 Factors
ECF - Environment Complexity 8 Factors

e.g.

16 complex use cases, 14 average use cases, 8 simple use cases, and infrastructure subsystem described with 10 simple use cases

UUCW = (16 x 15) + [(14 x 10) + (8 x 5)] + (10 x 5) = 470

There are 8 simple actors, 12 average actors, and 4 complex actors

UAX = (8 actors x 1) + (12 x 2) + (4 x 3) = 44

After evaluation of the technology and the environment,
T CF = 1.04
E CF = 0.94

UCP = (470 + 44) X 1.04 X 0.94 = 513

### Risk Management; How can we deal with the risk

Reactive Risk management (passive)

- When the risk happens, it affects to your project
  - Mitigation
  - Fix on failure
  - Crisis management

Proactive Risk Management

- Before the risk happens,

  - Minimize the effects even if the risk will happen

- Risk Identification
  Should consider....
  - Product size
  - Business impact
  - Customer chars; it is about the customer for buyer of your software
  - Process definition
  - developement environment; tools to be used to build the product
  - Technology to be built; 'newness' of the tech
  - Staff size and experience

### Risk Projection (risk estimation)

- Likelihood or probability that risk is real => Uncertainty (0 -1) may or may not happen
- Impact which is the cost -> Consequence of the problems associated with the risk

- Risk table
  PS: Project size risk
  BU : Business risk...

RMMM - Risk Mitigation Monitoring Management

### Risk Impact (Exposure)

RE = P X C

P: Probability of occurence for a risk
C: The cost to the project shoyld the risk occur

E.g.

- Risk Identification

  - Only 70% of the software components scheduled for reuse will be used, the rest will have to be custom developed

- Risk Probability = 80% (likely)
- Risk Impact

  - 60 reusable software components were planned. If only 70% can be used, 60 _ 30% = 18 component should be developed from scratch
    The average component is 100 LOC and the software engineering cost for each LOC is $14.00, te overall cost (impact) to develop the components is 18 _ (100 \* 18) = $25,200

- Risk exposure.
  RE = Risk Probability \_ overall cost
  RE = (0.80) \* $25,200 = $20,160
