# Suggestions for Next Year's Class (2024)

[TOC]



## Week 1 

### Revise the "Intro to course" lecture notes

***(I think I've already done this in 2023)***

- Break into two files:
  -  Intro to course--about how the class is like the real world and what we hope they will learn and how this is important to employers.
  - Overview of syllabus, grading and individual time reporting

Revise the sprint meetings lecture notes

- Break into two files
  - One for daily stand-ups and sprint planning and reporting on those.
  - One for the rest of the meetings (sprint review and team retrospective) and reporting on those.
    - Give this lecture in **week 2** since that's when they will do these meetings.

### Review PRs and code reviews

All the usual stuff, plus:

- Just one user story per PR, unless the implementation of one user story can’t be tested without implementing another.
- User stories should not be marked done until the PR has been reviewed, accepted, and the code merged into main.
- PR should include tests: always a functional test, sometimes also a unit test or integration test.

## Week 2

### Review unit testing. Talk about:

-  Why we use the repository pattern. 

- Why some people use the Unit of Work pattern.  

  > The goal of the unit of work pattern is to simplify DML (Data Manipulation Language) in your code and only commit changes to the database/objects when it's truly time to commit. &mdash;https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki/05)-The-Unit-of-Work-Pattern

- What should be tested and why query code should usually be in controllers and not in repositories.

- Test Driven Development and "test first".

Require a graded submission of the unit testing project.

### Introduce functional testing now instead of week 4

- A test should be written for every PR.
- Use cucumber?
  - [SpecFlow for .NET](https://docs.specflow.org/projects/getting-started/en/latest/index.html)
  - [Cucumber Open by SmartBear](https://cucumber.io/tools/cucumber-open/)
