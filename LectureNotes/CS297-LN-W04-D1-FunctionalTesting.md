---
title: Functional Testing
description: Overview of Functional Testing
keywords: testing, functional test, black box test, bug report, bug tracking, test cases
material: Lecture Notes
generator: Typora
author: Brian Bird
---

<h1>Functional Testing</h1>

**CS297 Programming Capstone**



<h2>Schedule</h2>

| Sprint | Week | Focus                                              |      | Sprint | Week | Focus                        |
| ------ | ---- | -------------------------------------------------- | ---- | ------ | ---- | ---------------------------- |
| 1      | 1    | Design review<br />project mgmt.<br />Git workflow |      | 4      | 7    | DevOps                       |
|        | 2    | End of sprint meetings                             |      |        | 8    | <u>Beta release</u>          |
| 2      | 3    |                                                    |      | 5      | 9    | Code freeze                  |
|        | 4    | <mark>Functional testing</mark>                    |      |        | 10   | <u>Release to production</u> |
| 3      | 5    | Continuous Integration                             |      |        | 11   | Final presentation           |
|        | 6    | Continuous Deployment<br /><u>Alpha release</u>    |      |        |      |                              |



<h2>Contents</h2>

[TOC]

## Overview of Functional Testing

Functional tests confirm that a software application or system operates correctly. Functional testing focuses on <u>testing the user interface</u> of the application to ensure that all user stories for an application  have been correctly implemented.

Functional testing is "Black box" (vs "White box" testing)

- Black box tests use the application's user interfaces and public APIs.
- White box tests use internal interfaces&mdash;unit tests are an example.

### Staging for Testing Web Apps

Dev teams often use three web sites (they can all be on the same web server, or not)

- Development site
- Staging (testing) site
- Production site

At this point, you will only need a development and staging site since you won't release your web app to production until the end of the term.

## Writing a Test Procedure

Here is an example taken from Hamilton (2022)  
Note that the *Actual Results* and *Pass/Fail* columns will be filled in by a tester.

![](FormatForStandardTestCases.png)

## Keep Updating the Test Procedure

You will use this test procedure to veryify your site is working correctly before each release:

- Alpha
- Beta
- Production

Keep your test plan up to date.

- For every user story you implement, add a test case to the test plan before craeting a PR. Reference the test case on the PR.
- Review the test plan before each release to be sure it is up to date.

## Bug Tracking

#### Bug / issue tracking systems

- Specialized for bug tracking
  - [BugZilla](https://www.bugzilla.org)
  - [Mantis](http://www.mantisbt.org)
  - GitHub Issues
- Agile project management systems which include issue tracking:
  - [Jira](https://www.atlassian.com/software/jira/features/bug-tracking)
  - ZenHub
  - Azure DevOps Boards


#### Make bug reports useful
Ask your testers to enter the following information:

- A descriptive title

- Steps to reproduce the bug

- Description of the failure
  - Include any error messages
  - Include a screen-shot if needed

**Example from Jira**  
Note that Jira has a "Bug" option for the issue "work type".  

<img src="/Volumes/DataCard/Repos/CS297-CourseMaterials/LectureNotes/Images/JiraBugIssue.png" alt="JiraBugIssue" style="zoom:40%;" />




##  References

Ashley Dotterweich, [What is Functional Testing?](https://dzone.com/articles/what-is-functional-testing), DZone article, 2016.
Functional testing focuses on  testing an application through the user interface to ensure that all  user stories have been correctly implemented.

Thomas Hamilton, [How to Write Test Cases: Sample Template with Examples](https://www.guru99.com/test-case.html), Guru99, 2019, revised 2022.
How to write a set of test cases for manually testing a software application.

Lawrence Howlett, [ How To Create Your Own Front-End Website Testing Plan](https://www.smashingmagazine.com/2014/11/how-to-create-your-own-front-end-website-testing-plan/), SmashingMag, 2014.
This article shows you what to consider when creating a front-end  testing plan and how to test efficiently across browsers, devices and  web pages.

------

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/) Capstone Class Lecture Notes written by [Brian Bird](https://profbird.dev), 2019, revised <time>2025</time>, are licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). 