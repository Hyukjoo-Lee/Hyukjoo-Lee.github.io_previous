---
layout: default
title: "Software Engineering: Theorical notes"
date: 2022-01-28 20:00:00
categories: Software Engineering
---

## 1. Introduction - Software engineering

### Software is

1. Instructions that provides desired features, function, and performance
2. Data structures that enable the programs to adequately manupulate information
3. Doc that describes the operation and use of the programs
4. Software is developed and engineered / not manufactured in the classical sense
5. Does not wear out, it does deteriorate
6. Domains - System, Application, Engineering/Scientific, Embedded, product-line, web&mobile apps, and AI software

### Wear VS Deterioration

- As time goes, changes are made, so that it increases failure rate because of side effects
- Curve is dynamic as a developer makes changes and fixs such errors

- Why must software change?
  - must be 'adapted' to meet the needs of new computing environments or techs
  - must be 'enhanced' to implement new business requirements
  - must be 'extended' to make interoperable with other more modern systems or db
  - mush be 're-architected' to make it viable

### What is software engineering?

- Defenition : IEEE defines software engeering is the application of a sysmetic, disciplined, quantifiable
  // (체계적이고, 규율화, 수량화 될 수 있는) approach to the development, operation, and maintainance of software; that is the application of engineering to software

- Layers: 1. A quality focus 2. Process 3. Methods, 4. Tools

- Process Framework Activities : Communication, planning, modeling (analysis of requirements, and design), construction (code generation, and testing), and finally deplyment

- Umbrella Activities(보호활동) : Tracking and control, risk management, quality assurance, review...etc

### Essence of software engineering practice

- Understand the problem(communication and analysis)
  - Who are the stakeholders?
  - What are the unknown?
    (what data, functions, and features are required to solve the problem?)
  - Can the problem be separated into smaller parts, and it results in easier to understand?
  - Can the problem be represented graphically? (analysis model can be created?)
- Plan a solution (modeling and design)
  - Is there existing software that implements the data, functions, and features that are required?(reference)
  - Similar solutions are reusalbe?
  - Can subproblems be defined?
  - Can you represent a solution in a manner that leads to effective implementation?
- Carry out plan (code generation)
  - Does the solution confirm to the plan?
  - Has the design and code been reviewed, or better, have correctness proofs been applied to algorithm?
- Examine result for accuracy (testing & quality assurance)
  - Has a reasonable testing strategy been implemented?
  - Has the software been validated against all stakeholder requirements?

### Hooker's General Priniciples

- The Reason It All Exists
- KISS (Keep It Simple, Stupid!) – design simple as it can be.
- Maintain the Vision
- What you produce, others will consume
- Be open to the future
- Plan ahead for reuse
- Think! - placing thought before action produce results

### How it all starts - safehome begins

Some business need

- to correct a defect
- to adapt a legacy system to a changing business environment
- to extend the functions and features
- to creat a new product, service, or system

## 2. Process Model

### Process Model Flow

- Linear Process Flow : Communication &rarr; planning &rarr; Modeling &rarr; Implementation &rarr; Contruction &rarr; Deployment
- Iterative Process Flow : ((Communication &rarr; planning) &rarr; (Modeling) &rarr; Implementation &rarr; Contruction) &rarr; Deployment
- Evolutionary Process Flow : Communication &rarr; planning &rarr; Modeling &rarr; Implementation &rarr; Contruction &rarr; Deployment (<em> Increment released </em>)
- Parallel Process Flow

4.

## 5. Human Aspects of Software Engineering

### Traits of Successful Software Engineers

- Sense of individual responsibility
- Acutely aware of the needs of team members and stakeholders
- Honest about design flaws and offers constructive criticism
- Resilient under pressure
- Heightened sense of fairness
- Attention to detail
- Pragmatic adapting software engineering practices based on the circumtances at hand

### Effective software team attributes

- Sense of purpose, involvement, trust, improvement, and diversity of team member skill sets

### Project Factors affecting team structure

- Difficulty of the problem to be solved
- Too huge program size in lines of code or function points
- Meeting times (team lifetime)
- Degree to which the problem can be modularized
- Required quality and reliablility(시스템 신뢰성) of the system to be built
- Rigidity of the delivery date
- Degree of communication required for the project

### Agile teams

- Emphasize 'Individual competency' coupled with group collabortion
  (Every members has the ability to make a decision)
- Communication among developers and stakeholders is crucial
- Planning is constrained only by business requirements and organizational standards
- Team is “self-organizing.”
  - Adaptive team structures
  - Significant autonomy

Team members must have trust in one another.
The distribution of skills must be appropriate to the problem.
Mavericks may have to be excluded from the team, if team
cohesiveness is to be maintained.

Team is “self-organizing.”
• An adaptive team structure.
• Planning is kept to a minimum.
• Team select its own approach constrained by business requirements and
organizational standards.

### Impact of social media

- Highly depend on engineer's ability
- Value grows as team size increases or when a team is geographically separated
- Benefits from it must be weighted against the threat of exprosure of crucial information.

### Team decision making complication

- Has unintented consequences on another project object e.g. law
- Different views of the problem can lead to different conclusion about the way forward

### Factors affecting global software dev teams

- Distance complicates communication / accentuates the need for coordination
- Communication enhances collaboration
- Collaboration improves coordination
- Coordination reduces Barrier and complexity
- Barrier and complexity attenuates communication ....

## 6. Project management concepts

- Four P's : People, Product, Process, and Project

- Stakeholders Senior managers, Project managers, <em>Practitioners</em> : who deliver the technical skills that can upgrade a product or apps

### Team Leaders practices

- Good Model the way
- Inspire and shared vision - Motivate team members involving stakeholders early
- Challenge the process - encourage team members while learning from their failures
- Enable others to act - by sharing decision making and goal setting
- Encourage the heart - build team spirit
