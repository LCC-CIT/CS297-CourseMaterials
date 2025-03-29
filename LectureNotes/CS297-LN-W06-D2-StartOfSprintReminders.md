---
title: Start of Sprint
description: Reminders regarding PRs, Sprint meetings, Testing, and Bug Reporting
keywords: bug reports, sprint meeting, PR, test
material: Lecture Notes
generator: Typora
author: Brian Bird
---

<h1>Start of Sprint Reminders</h1>

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

## Sprint Meetings

Keep them short and to the point.

- Sprint plannnig should just be about prioritizing, and moving backlog into the current sprint.
  - Have your agile management software (like Jira) open with everyone looking at the backlog for the current sprint.
  - Bugs and non-user-story tasks may also need to be added.
  - You may also need to:
    - Add any missing user stories.
    - Add a task to do some new design on a user story.
- Daily standups should just be for each team member to answer the three stock questions.
  - Not of problem solving.
  - Not for giving advice or opinions.
- Sprint Product Review
  - Focus on getting feedback from the client.
- Sprint retrospective
  - Ask the three questions
  - Keep everything positive, constructive, and relevant.

## Pull Requests

- Creating a PR
  - Should be for one user story, unless:
    - There are two stories that are interdependnt and can't be implmented separately.
    - One or more child issues (tasks) are complete and testable, evan thought the story isn't complete.
  - Include the user story or issue ID.
  - Should reference a functional and/or integration or unit test.
  - Can be for a bug fix or non-user-story task.
- Reviewing a PR
  - Actually reveiw the code and check for best practices.
  - Test the feature and evaluate the test (either written or automated) to ensure that it fully tests the feature.
  - If there are issues, give feedback in the PR comments and be specific about what you think needs to be revised.
- Closing a PR
  - It must either pass review, or be determined to be unneeded.
  - The team can establish a team practice as to whether it is the reviewer or the author of the PR who merges the PR into main.



## Related Lecture Notes

[Agile Scrum Review: Starting a Sprint](lectureNotes/CS297-LN-W01-D2-AgileProjectMgmt1.html)

[Agile Scrum Review: Finishing a Sprint](lectureNotes/CS297-LN-W01-D2-AgileProjectMgmt2.html)

[Scrum Meeting Report Guide](CS297_MeetingReportGuide.html)



## References

[Pull Request Help Docs](https://docs.github.com/en/pull-requests)&mdash;GitHub

[Scrum Sprints: Everything you need to know](https://www.atlassian.com/agile/scrum/sprints)&mdash;Atlassian



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/) Capstone Class Lecture Notes written by [Brian Bird](https://profbird.dev), <time>2023</time>, are licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). 