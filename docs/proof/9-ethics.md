# Analysis: Ethics in Software Development and Engineering

- [Analysis: Ethics in Software Development and Engineering](#analysis-ethics-in-software-development-and-engineering)
  - [Intro](#intro)
  - [What is ethics in Software Development?](#what-is-ethics-in-software-development)
  - [Why is ethics important in Software Engineering?](#why-is-ethics-important-in-software-engineering)
  - [What could be done to address ethical aspects in your work?](#what-could-be-done-to-address-ethical-aspects-in-your-work)
    - [What are the types of harms the public can suffer as a result of this work?](#what-are-the-types-of-harms-the-public-can-suffer-as-a-result-of-this-work)
    - [How can software engineers contribute to the good life of others?](#how-can-software-engineers-contribute-to-the-good-life-of-others)
    - [Who exactly are the public, who is the userbase to whom the engineer is obligated to?](#who-exactly-are-the-public-who-is-the-userbase-to-whom-the-engineer-is-obligated-to)
    - [Why is the engineer obligated to protect the public?](#why-is-the-engineer-obligated-to-protect-the-public)
    - [What are the professional codes of software engineering ethics?](#what-are-the-professional-codes-of-software-engineering-ethics)
  - [How do you know that your ethical considerations match with those of other software engineers?](#how-do-you-know-that-your-ethical-considerations-match-with-those-of-other-software-engineers)
  - [Which ethical aspects play a role in my project?](#which-ethical-aspects-play-a-role-in-my-project)
    - [IPS](#ips)
    - [GPS](#gps)
  - [Do you foresee ethical conflicts caused by your software? What kind of?](#do-you-foresee-ethical-conflicts-caused-by-your-software-what-kind-of)
  - [Can you do something to avoid or minimize these conflicts?](#can-you-do-something-to-avoid-or-minimize-these-conflicts)
  - [References](#references)

## Intro

This analysis will mainly focus on ethics in software development, and the application in the individual project.

It will answer several main questions about ethics in software development, and it will signal, if any, ethical roadblocks that can occur in a software development project. 

## What is ethics in Software Development?

**Ethics** in its broadest sense refers to the basic concept of *how best to live*. Therefore, you can say that ethics in software development encompasses the following:

* How best to code ethically
* How best to work together with your peers
* How best to better the users' experience

## Why is ethics important in Software Engineering?

Software engineers build lines of code, not cars, rockets or bridges full of vulnerable human beings. Where is the comparison between real-life and code here? Cars and rockets depend on *critical software* to operate safely. Bridges are built upon with use of sophisticated computer programs calculating expected load, strain, material strength and resiliency.<sup>[[1]](#ref1)</sup>

Another example could be the cultural sensitivity of people in a certain countries. Those people could, for example, be very sensitive about territorial borders. A real world example could be the error Google made in 2010, where Google incorrectly drew the Nicaraguan border with Costa Rica, resulting in a deployment of Nicaraguan soldiers to said border.<sup>[[2]](#nicref1)</sup>

A third reason, and arguably equally as imporant, is teamwork. If you code ethically, work with defined conventions and have good communication with your peers, the overall quality of your product increases. 

## What could be done to address ethical aspects in your work?

Understanding, commitment and agreement. 

The easiest way to work ethically is to be aware of your userbase. Understand what your users want. At the same time, the development team needs to establish a convention and agreements on how to code. They should agree to adhere to these conventions.

Software engineers should concern themselves primarily with the health, safety and welfare of those who are affected by their work. This includes customers, but also peers.

To know how to "be ethical", you need to understand the following points<sup>[[1]](#ref1)</sup>:

* **What** are the types of harms the public can suffer as a result of this work?
* **How** can software engineers **contribute** to the good life of others?
* **Who** exactly are the public, who is the userbase to whom the engineer is obligated to?
* **Why** is the engineer obligated to protect the public?
* What are the professional **codes** of software engineering ethics?

### What are the types of harms the public can suffer as a result of this work?

Failure in software engineering can result in different types of harm to the userbase. In case of the Nicaraguan border dispute, it can cause catastrophic loss of life or injury. 

Failure can also result in mental harm to the userbase. What if an inadvertant use of a certain feature discriminates against a group of people? You could look at the recent developments of artificial intelligence, where the AI can discriminate. Oftentimes this is the result of a bias during development, be it intentional or unintentional. Associate Professor Jeannie Marie Paterson and Dr Yvette Maker have written about this.<sup>[[3]](#aidiscriminate)</sup>

### How can software engineers contribute to the good life of others?

Ethics is not just about preventing harm on others. Ethics is just as much about doing good. A software engineer should strive to improve the userbase's lives.

### Who exactly are the public, who is the userbase to whom the engineer is obligated to?

Usually, the stakeholders, everyone who is potentially affected by the software, is the public. The software engineer is obligated to this group. This group can be split into multiple smaller groups, each with their own ingagement levels with the software. 

For example, when developing software for a pacemaker, a direct stakeholder could be the person who has the pacemaker in their body. Their lives are directly impacted by the software. A secondary stakeholder could be the doctor who needs to interface with the software.

In most ethical contexts, there are a variety of stakeholders potentially impacted by the software engineers' actions, and their interests may not always align with each other.<sup>[[1]](#ref1)</sup>

### Why is the engineer obligated to protect the public?

The simple answer is, 'because software engineers are human beings, and all human beings have ethical obligations to each other.'<sup>[[1]](#ref1)</sup>

### What are the professional codes of software engineering ethics?

Each professional group of engineers employs their own codes of practise, including codes for ethical practise.

The ACM and IEEE have created a joint code of practises.<sup>[[4]](#ethiccode1)</sup> The NSPE has created a code of ethics as well.<sup>[[5]](#ethiccode2)</sup>

These codes are *not* meant to serve as a formal checklist on how to be an ethical engineer. Ethical codes are just a tool to help us develop an eye for what would be appropriate in certain circumstances.

## How do you know that your ethical considerations match with those of other software engineers?

This is a har question to answer, and it is unsure if you can always answer it wholly. 

One thing to keep in mind is that it is impossible to always be a hundred percent in line with everyone.

What you can do, is regularly discuss your practises with your peers. Keep in contact and communicate if something is unclear, or when you want to update your code of ethics. Communication is key. 

Furthermore, you can define a document in which you define your definitions of done (DOD). Make a contract in which you state that certain parts of code needs to be tested.

## Which ethical aspects play a role in my project? 

### IPS

In my individual project, I am aiming to make students' lives easier by providing them with critical information at the start of the day. Think of the weather, next 5 appointments, 5 newest emails. Currently, many of these services are fragmented across many services like Google, Buienradar...

As far as cooperation with peers, this is a bit less prevalent. I am not directly working together with peers. What I do provide any future developers with, is a concise codebase, using known per-language code conventions. I also provide, where necessary, unit tests and integration tests. Finally, I offer developers the Docker building blocks, in the form of Dockerfiles, to build the services.

My repositories are open source and I aim to provide the APIs with the necessary documentation. (still planned as of 2022-nov-21)

### GPS

The group project goal is to make a visit to a restaurant easier for both the customer and the restaurant itself. It is a web application which provides a portal for the customer to order food without needing a waiter to come by the table each time to take the order.

In a team environment, we work with known definitions of done. We use tooling, such as SonarCloud, to verify our code and check for code smells and known bugs. During each pull requests, we analyze each other's code and comment on its resillience.

## Do you foresee ethical conflicts caused by your software? What kind of?

No.

## Can you do something to avoid or minimize these conflicts? 

No.

## References

> [1]<a name="ref1"></a> An Introduction to Software Engineering Ethics (n.d.). Retrieved November 21, 2022, from https://www.scu.edu/media/ethics-center/technology-ethics/Students.pdf

> [2]<a name="nicref1"></a> Walker, P. (2017, November 26). Nicaragua to keep troops in disputed territory after Google Maps error. The Guardian. https://www.theguardian.com/world/2010/nov/11/nicaragua-troops-calero-island-google-maps

> [3]<a name="aidiscriminate"></a> Associate Professor Jeannie Marie Paterson and Dr Yvette Maker, University of Melbourne. (2022, November 21). Why does artificial intelligence discriminate? Pursuit. https://pursuit.unimelb.edu.au/articles/why-does-artificial-intelligence-discriminate

> [4]<a name="ethiccode1"></a> ACM Ethics. (2022, June 8). Software Engineering Code - ACM Ethics. ACM Ethics - the Official Site of the Association for Computing Machinery’s Committee on Professional Ethics. https://ethics.acm.org/code-of-ethics/software-engineering-code/

> [5]<a name="ethiccode2"></a> Code of Ethics | National Society of Professional Engineers. (n.d.). https://www.nspe.org/resources/ethics/code-ethics