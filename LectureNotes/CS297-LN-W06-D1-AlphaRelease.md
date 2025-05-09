---
title: Alpha Release
description: Explain the purpose of an alpha release and how to do alpha testing.
keywords: alpha release, bug reports, functional testing, UX testing
material: Lecture Notes
generator: Typora
author: Brian Bird
---

<h1>Alpha Release</h1>

**CS297 Programming Capstone**



<h2>Schedule</h2>

| Sprint | Week | Focus                                                        |      | Sprint | Week | Focus                        |
| ------ | ---- | ------------------------------------------------------------ | ---- | ------ | ---- | ---------------------------- |
| 1      | 1    | Design review<br />project mgmt.<br />Git workflow           |      | 4      | 7    | DevOps                       |
|        | 2    | First end of sprint meetings                                 |      |        | 8    | <u>Beta release</u>          |
| 2      | 3    |                                                              |      | 5      | 9    | Code freeze                  |
|        | 4    | Functional testing                                           |      |        | 10   | <u>Release to production</u> |
| 3      | 5    | Continuous Integration                                       |      |        | 11   | Final presentation           |
|        | 6    | <mark><u>Alpha release</u></mark><br />Continuous Deployment |      |        |      |                              |



<h2>Contents</h2>

[TOC]

# Alpha Release

This week you will release your project for alpha testing. Today we will discuss all that is involved in an alpha release.

## What is an Alpha Release?

### Purpose of an alpha release

- Get early feedback on usability from potential end-users and other stake holders.
- Get bug reports from potential end users as opposed to just testers.
  In this context, we mean that we won't be using just software dev type people for testing. We'll be showing the product to people who are typical of those who we expect to use the product.
- Motivation to get your project to a usable state.

### Characteristics of an alpha release

- A minimal set of features implemented.
   Not all the features will be done, but a minimal set of the most important features will be at least partially working. These features  should be working well enough that users can actually use the application in some basic way.
- Still has bugs.
  There will be both known and unknown bugs. Give the testers a list of the known bugs.
- You should start using some form of bug tracking at this point.
  You can enter bugs in your agile project management system and identify them as *bugs* to distinguish them from *user stories*.
- You should do a code freeze one or more days before the end of the sprint so you have time to fix critical bugs (not all bugs) before functional testing. There should be no code changes or bug fixes during testing.

### Requirements for the Capstone alpha release

- The web site/app will be running on a staging or test server.
- Your team will have a functional test plan ready.
- Tetsters who are not part of the development team will do the testing.
- You will also get feedback on user experience from the testers and your client.
- Your team will give a presentation on your alpha release next week.

## Testing the Alpha Release

- The web app should be tested running online, not on a development machine.
- You identified three testers when you submitted your test plan. Hopefully at least one of them is not a developer.
- Your testers will use your test plan to test the functionality of the web app.
- Your testers will also give you feedback on UX and usefulness of the web app.
  You can either use the survey you used in the system design class to get UX feedback or an interview.



## Real Life Story

At Intel Architecture Labs:

- Contrast the testing done by the QA department to alpha testing done by "real world" users.
- E-mail auto-sorting feature that passed QA but failed alpha testing.

​      

## References

Luke Frieler, [Alpha vs. Beta Testing](https://www.centercode.com/blog/2011/01/alpha-vs-beta-testing), Centercode blog, 2019.



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/) Capstone Class Lecture Notes written by [Brian Bird](https://profbird.dev), 2018, revised <time>2022</time>, are licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). 