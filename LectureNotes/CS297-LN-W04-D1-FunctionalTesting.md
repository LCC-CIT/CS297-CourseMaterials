---
​---
title: Functional Testing
description: Overview of Functional Testing
keywords: Test, Functional Test
material: Lecture Notes
generator: Typora
author: Brian Bird
​---
---

<h1>Functional Testing</h1>

**CS297 Programming Capstone**



<h2>Schedule</h2>

| Sprint | Week | Focus                                              |      | Sprint | Week | Focus                        |
| ------ | ---- | -------------------------------------------------- | ---- | ------ | ---- | ---------------------------- |
| 1      | 1    | Design review<br />project mgmt.<br />Git workflow |      | 4      | 7    | DevOps                       |
|        | 2    | First end of sprint meetings                       |      |        | 8    | <u>Beta release</u>          |
| 2      | 3    |                                                    |      | 5      | 9    | Code freeze                  |
|        | 4    | <mark>Functional testing</mark>                    |      |        | 10   | <u>Release to production</u> |
| 3      | 5    | Continuous Integration                             |      |        | 11   | Final presentation           |
|        | 6    | <u>Alpha release</u><br />Continuous Deployment    |      |        |      |                              |



<h2>Contents</h2>

[TOC]

## Overview of Functional Testing

Functional tests confirm that a software application or system  operates correctly. Functional testing focuses on testing the interface  of the application to ensure that all user stories for an application  have been correctly implemented.

Functional testing is "Black box" (vs "White box" testing)

- Black box tests use the application's user interfaces and public APIs
- White box tests use internal interfaces - unit tests are an example

### Staging for Testing Web Apps

Multiple sites (can all be on the same server)

- Development testing site
- Acceptance testing site
- Production site

## Writing a Test Procedure

Here is an example taken from Hamilton (2022) :

![](D:\Repos\CS297-CourseMaterials\LectureNotes\FormatForStandardTestCases.png)

## Bug Tracking

#### Bug / issue tracking systems

- Specialized for bug tracking

- - [BugZilla](https://www.bugzilla.org)
  - [Mantis](http://www.mantisbt.org)
  - GitHub Issues

- Agile project management systems which include issue tracking:

- - Jira
  - Pivotal Tracker
  - ZenHub
  - Azure DevOps Boards

#### Make bug reports useful
Ask your testers to enter the following information:

- A descriptive title

- Steps to reproduce the bug

- Description of the failure

- - Include any error messages
  - Include a screen-shot if needed



##  References

[What is Functional Testing?](https://dzone.com/articles/what-is-functional-testing)
 Functional testing focuses on  testing an application through the user interface to ensure that all  user stories have been correctly implemented. - DZone article, 2016.

Thomas Hamilton, [How to Write Test Cases: Sample Template with Examples](https://www.guru99.com/test-case.html), Guru99, 2019, revised 2022.
How to write a set of test cases for manually testing a software application.
[
 How To Create Your Own Front-End Website Testing Plan](https://www.smashingmagazine.com/2014/11/how-to-create-your-own-front-end-website-testing-plan/)
 This article shows you what to consider when creating a front-end  testing plan and how to test efficiently across browsers, devices and  web pages. - SmashingMag, 2014.

[Differences between Software Testing and Game Testing](http://www.gamasutra.com/blogs/JohanHoberg/20140721/221444/Differences_between_Software_Testing_and_Game_Testing.php)
 What is the major difference between testing an application or a software system compared to testing a game? - Gamasutra, 2014.

------

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)
Capstone Class Lecture Notes by [Brian Bird](https://profbird.dev), <time>2022</time>, are licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). 