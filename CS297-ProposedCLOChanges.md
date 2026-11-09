# CS297 Proposed Course Learning Outcome (CLO) Changes

**CS297 Software Development Capstone** · Prepared November 9, 2026

## Summary

I recommend replacing the 8 catalog CLOs with the 8 below. They keep the project and teamwork outcomes, drop the career-prep ones, and add the outcomes the course now teaches: Agile team meetings and reporting, team workflow tools, quality testing, server environments and CI/CD, and staged releases. A [CLO to PLO Alignment](#clo-to-plo-alignment) table shows which Program Learning Outcomes (PLOs) of the AAS in Software Development each one supports. The CLOs are written at about the same level of abstraction as the PLOs. The specific tools and activities that put each one into practice are listed separately in [Course Content Behind Each CLO](#course-content-behind-each-clo).

## What This Is Based On

Weekly overviews exist only for weeks 1, 4–8 and 10; there are none for weeks 2, 3 or 9. They're mostly schedules and due dates, so I also used:

- The week 1–6 lecture notes
- The syllabus (`CS297_Syllabus.md`)
- `CapstoneProjectRequirements.md`
- The alpha and final presentation guides
- The grading rubrics: project implementation, team participation, alpha presentation and functional test plan
- The Spring 2026 Moodle course page (weeks 1–11), including its supplemental readings, examples and assignment descriptions

The syllabus already lists only 3 CLOs, and it says "medium scale" where the catalog says "small scale." The syllabus should be updated once new CLOs are approved.

## What to Do with Each Catalog CLO

| # | Catalog CLO | Recommendation |
|---|---|---|
| 1 | Analyze, design and implement a small scale, but significant programming project | **Revise** to medium scale, as an implementation outcome (new CLO 4) |
| 2 | Demonstrate an ability to integrate knowledge and skills acquired in previous coursework | **Merge** into new CLO 4 |
| 3 | Demonstrate the ability to work as an effective member of a project team | **Revise** as Agile team meetings and reporting (new CLO 2) and team workflow tools (new CLO 3) |
| 4 | Research, analyze and describe the current state of the state and regional job markets | **Drop**: not taught |
| 5 | Participate in self-evaluation of work skill strengths | **Revise** as individual progress reporting (new CLO 2) |
| 6 | Prepare an effective cover letter and resume for an employment application | **Drop**: not taught |
| 7 | Through mock interviews, demonstrate an ability to respond to typical general and scenario questions | **Drop**: not taught |
| 8 | Develop a plan for professional growth | **Drop**: not taught |

If the program still wants career-prep outcomes (catalog CLOs 4, 6, 7 and 8), they need a home in another course. The only career-related item in the current materials is the LCC Job Fair announcement.

## Recommended CLOs

Upon successful completion of this course, the student will be able to:

1. Work with clients and stakeholders to continually refine and prioritize the requirements of a software product throughout its development in an Agile workflow.
2. Plan, conduct, and document effective Agile team meetings, including sprint planning, daily stand-ups, sprint reviews with clients, and team retrospectives, and report on team and individual progress.
3. Coordinate and integrate a team's work using project-management, issue-tracking, version-control, and team communication tools.
4. Implement a medium-scale, secure, data-driven software application that integrates the concepts, design and coding principles learned in prior coursework for the AAS in Software Development.
5. Evaluate software quality, functionality, usability, accessibility, and security through User eXperience (UX) testing, automated and manual testing and use the results to correct issues.
6. Configure and manage test, staging, and production servers, including the secure management of credentials across development and production platforms, and automate building, testing, and deployment using continuous integration and continuous delivery (CI/CD).
7. Plan, carry out, and document alpha, beta, and production releases of a software product, using feedback from each release to guide the next stage of development, and finally to hand off the finished product and its documentation to the client.
8. Present and evaluate a team's product and development process for technical and non-technical audiences.

### CLO to PLO Alignment

| CLO | Supports PLOs |
|---|---|
| 1. Requirements | 1, 2 |
| 2. Team meetings and reporting | 2 |
| 3. Team workflow tools | 2, 7 |
| 4. Implementation | 3, 4, 5, 6, 7, 8 (security) |
| 5. Quality testing | 7, 8 |
| 6. Environments, credentials, and CI/CD | 2, 3, 8 (security) |
| 7. Releases | 2, 3 |
| 8. Presentation and evaluation | none directly (professional communication) |

### Technology-Neutral Wording

The course is moving from .NET to JavaScript and React, so the CLO text names concepts, not products: for example, "version control" rather than Git, "relational database" rather than MySQL, and "ORM (object-relational mapping)" rather than Entity Framework. The [Course Content Behind Each CLO](#course-content-behind-each-clo) table still names the specific tools used in Spring 2026, as evidence of what was taught; update it as the course content changes.

### Changes in This Revision

- **Made the wording technology-neutral.** Removed "such as Jira and Git" from CLO 3.
- **Added team communication tools to CLO 3**, covering the Discord server and the mix of real-time and asynchronous work that online teams do.
- **Added "secure" to CLO 4**, since authentication and authorization are project requirements and are taught in week 1.
- **Added release documentation and client handoff to CLO 7.** The beta release report (changes, bugs fixed, known bugs, testers), the Final Project Documents forum (Jira and repository links, live site, UML diagrams, functional test plans) and the week 10 handoff to the client weren't covered by any CLO.

### Changes in the Previous Revision

- **Removed duplication between CLOs 1 and 2.** "Agile" and planning were in both. CLO 1 is now only about requirements, CLO 2 is about team meetings and reporting, and CLO 3 is about the tools that coordinate the work.
- **Added team meetings and reporting** (CLO 2): sprint planning, daily stand-ups, sprint reviews with clients and retrospectives, plus team meeting reports and individual status reports.
- **Moved self-evaluation** from the presentation CLO into CLO 2's reporting, since the weekly individual status reports are where it happens.
- **Split delivery into two CLOs.** CLO 6 covers server environments, secure credential management and CI/CD automation; CLO 7 covers the alpha, beta and production releases.
- **Moved the PLO tags** out of the CLO text into the alignment table above.

### Course Content Behind Each CLO

| CLO | Where it shows up in the course |
|---|---|
| 1. Requirements | Week 1 design review: requirements document, UI wireframes, domain model; Jira epics and user stories; backlog refinement each sprint; client feedback from sprint reviews and releases |
| 2. Team meetings and reporting | Weeks 1–3 Agile Scrum lecture notes: Scrum roles, sprint planning, daily stand-ups, sprint review and retrospective; each student serves as Scrum Master for at least one sprint; meeting plans for the first three sprints; sprint meeting reports (`CS297_MeetingReportGuide.md`); weekly individual progress reports; sprint meeting attendance and stand-ups graded in the team participation rubric |
| 3. Team workflow tools | Jira backlog, sprints, sub-tasks and story-point estimates; Git feature-branch workflow and practice repository; pull requests (graded, 1 per week); merges and merge-conflict resolution; class Discord server; online teams working both in real time and asynchronously |
| 4. Implementation | Capstone project requirements: ASP.NET, Node.js, React or React Native; a database; authentication and authorization; admin pages; input forms; custom code. Week 1 Identity Scaffolding notes, video and demo site (seeded admin user, MySQL database); weeks 3–4 Bird Sighting demos (dynamic forms with JavaScript, Ajax data from a controller); implementation rubric (code quality, best practices, simplicity, internal documentation) |
| 5. Quality testing | Week 4 functional testing and test procedures with 3 recruited testers; UX testing; unit tests; bug tracking; alpha and beta testing |
| 6. Environments, credentials, and CI/CD | Week 2 publishing to SmarterASP.NET and supplemental reading on environment-specific configuration (`appsettings.Staging.json`); staging server for testing (week 4); week 5 continuous integration with GitHub Actions; week 6 continuous delivery to Azure or SmarterASP with GitHub environments and secrets; "published to a server" in the implementation rubric |
| 7. Releases | Alpha release and alpha testing report (week 6), beta release report with changes, bugs fixed, known bugs and beta testers (week 8), code freeze (week 9), production release and client handoff (week 10); Final Project Documents forum: Jira and GitHub links, live site URL, UML diagrams, functional test plans |
| 8. Presentation and evaluation | Alpha presentation (week 7), final presentation (finals week), optional presentation to the CIT Community Advisory Committee |

## Where the PLOs Aren't Covered

There are two kinds of gap: a PLO that no CLO covers, and a PLO a CLO names but the course doesn't actually teach or grade. Both are noted below.

| PLO | Covered by | Status |
|---|---|---|
| 1. Requirements and specifications | CLO 1 | **Partial.** Requirements come from the System Design course; the capstone only reviews and refines them. |
| 2. Agile team practices | CLOs 1, 2, 3, 6, 7 | **Strong**, with two weak spots. Peer code review is barely taught and not graded: the participation rubric counts PRs created, not reviews done. Acceptance testing is informal, done through beta testers and the client. |
| 3. Console, desktop, web, mobile, cloud | CLOs 4, 6, 7 | **Partial.** Covers web and cloud (Azure), and mobile only if a team chooses React Native. Console and desktop are absent, which is reasonable for a capstone. |
| 4. Paradigms, data structures, algorithms, patterns | CLO 4 | **Partial.** Design docs and the domain model are revised, and code quality is graded, but design patterns and algorithms aren't addressed explicitly. |
| 5. Relational and non-relational databases | CLO 4 | **Required, lightly taught, not graded.** "Use a database" is a project requirement, and the week 1 demo site shows a relational database with seed data. No rubric line covers databases, and non-relational databases don't appear. |
| 6. Distributed systems and APIs | CLO 4 | **Partial.** The weeks 3–4 Bird Sighting demos show a browser calling the server asynchronously (Ajax) for data, and a web service is one of the allowed technology choices. Communication between separate processes or services isn't otherwise addressed. |
| 7. Develop, test, debug maintainable code | CLOs 3, 4, 5 | **Strong.** Code quality and unit tests are rubric items. |
| 8. Testing for functionality, usability, accessibility, performance, security | CLOs 5, 6 | **Partial; course changes needed.** Functional, usability and unit testing are strong. CLO 5 names accessibility and basic security, but neither is currently taught or graded: accessibility appears once in the materials, and security appears only as code-review comments (e.g., "passwords in source code"). CLO 6's secure credential management is taught only for CI/CD (GitHub Secrets in the week 6 lecture). Environment-specific configuration appears only as optional week 2 reading; keeping development and production credentials separate on developer machines and servers isn't taught. Performance is graded, but load testing is struck out of the final presentation guide and isn't named in CLO 5. |
| 9. AI tools to generate, verify, debug, refactor code | none | **Not covered.** No course content. The only "AI" in the materials is a registration announcement. |
| 10. Integrating AI and ML into applications | none | **Not covered.** No course content. |

## Suggestions for Closing the Gaps

- **CLO 6 (credential management).** Add a lesson on keeping secrets out of source control across environments: a local secret store or an untracked environment file in development, environment-specific configuration, and host-provided environment variables or a key vault in production, alongside the CI/CD secrets already covered. The current week 2 reading on environment-specific configuration could become required material for that lesson. This also addresses the "passwords in source code" issue seen in project grading.
- **CLO 5 (accessibility and basic security).** Now that these are in the CLO, the course needs content and assessment to support them. For example, add accessibility checks (an automated checker such as Lighthouse or axe, plus keyboard-only and screen-reader passes) and basic security checks (no secrets in source, input validation, authorization on restricted pages) to the functional test procedure and the functional test plan rubric.
- **PLO 9 (AI development tools).** No CLO is proposed because the course doesn't teach this. If AI-assisted development is added to the course, a CLO like this would close the gap and fits the existing workflow:
  *"Use AI development tools to generate, review, debug, and refactor code, and verify the output for accuracy, maintainability, and security."*
- **PLO 10 (AI and ML integration).** This would need a project requirement, such as having each project integrate at least one AI or ML service.
- **PLO 2 (peer code review).** Grade PR reviews, not just PRs created, in the team participation rubric.
- **Syllabus.** Replace the syllabus's 3 CLOs with the approved set so the syllabus and catalog agree.
