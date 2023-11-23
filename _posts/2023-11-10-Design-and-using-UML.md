---
layout: post
title: Unified Modeling Language (UML)
date: 2023-11-10 00:00:00
categories: [automotive]
tags: [design, uml]
last_modified_at: 2023-11-10
---


# Design phase

* **design**: specifying the structure of how a software system will be written and function, without actually writing the complete implementation
* a transition from "what" the system must do, to "how" the system will do it 
  * What classes will we need to implement a system that
  * meets our requirements?
  * What fields and methods will each class have?
  * How will the classes interact with each other?

# How do we design classes?

* class identification from project spec / requirements
  * nouns are potential classes, objects, fields
  * verbs are potential methods or responsibilities of a class

* CRC card exercises
  * write down classes' names on index cards
  * next to each class, list the following:
  * responsibilities: problems to be solved; short verb phrases
  * collaborators: other classes that are sent messages by this class (asymmetric)
* UML diagrams
  * class diagrams (today)
  * sequence diagrams
  * ....

# What is UML?

* UML: pictures of an OO system
  * programming languages are not abstract enough for OO design
  * UML is an open standard; lots of companies use it

* What is legal UML?
  * a descriptive language: rigid formal syntax (like programming)
  * a prescriptive language: shaped by usage and convention
  * it's okay to omit things from UML diagrams if they aren'tneeded by team/supervisor/instructor


<figure>
  <img src="/assets/img/blogs/automotive/UML_logo.svg.png" alt="UML Logo">
  <figcaption>UML Logo</figcaption>
</figure>

# Uses for UML

* as a sketch: to communicate aspects of system
  * forward design: doing UML before coding
  * backward design: doing UML after coding as documentation
  * often done on whiteboard or paper
  * used to get rough selective ideas

* as a blueprint: a complete design to be implemented
  * sometimes done with CASE (Computer-Aided Software Engineering) tools

* as a programming language: with the right tools, code can be auto-generated and executed from UML
  * only good if this is faster than coding in a "real" language

# Example

1. State machine diagram
<figure>
  <img src="/assets/img/blogs/automotive/state-machine-of-fota-target.png" alt="State machine of the FOTA Target">
  <figcaption>State machine of the FOTA Target</figcaption>
</figure>

2. Sequence Diagram
<figure>
  <img src="/assets/img/blogs/automotive/installation-sequences.png" alt="Installation sequence">
  <figcaption>Installation sequence</figcaption>
</figure>

# Learning resources

* **#1** [lecture08-uml1](https://courses.cs.washington.edu/courses/cse403/11sp/lectures/lecture08-uml1.pdf)
* **#2** [OOP_Bai13(vi)](https://users.soict.hust.edu.vn/trungtt/uploads/slides/OOP_Bai13(vi).pdf)