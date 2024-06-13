# Changes to Make for 2025

## Week 1

Git: Give a tutorial on the Git Branch workflow and how to do PRs, mreges and resolve merge conflicts.

Team work sessions: Make a clear difinition of what "team work sessions are". 
Sprint planning: emphasize that one person should do a whole "vertical slice" view + controller (+ model changes, but only after consulting the team).

New project: Remind them they can use the project template that includes identity.

Put everyone on the same Discord server, so I can moderate.

Reports: get a team report on sprint planning and work sessions (work sessions will include daily standups).

## Week 2

Identity scaffolding: give the tutorial.

Servers: Set up staging and production servers.



## Practices

- Require a staging/testing server in addition to the production server
- Teach them to use Selenium
- 

## Things Related to the Final Grade

### Participation

- Instead of having students report PRs and User story points, have then send a link to those pages on GitHub and Jira.
- For meeting attendance:
  - Combine daily standup with team work sessions
  - Require two real-time work sessions and two that are optionally async
  - Document sprint meetings in Jira?
- Give participation grades more often  (after each sprint?)
- Add the participation grade weighting to the syllabus with some room in it for me to make subjective adjustments.
- Grade Jira use at the end of each sprint.

### Final Submission

- Each student should summarize what they did for the project in one paragraph
- Update the rubric!
  - Put back in: validation, security testing, performance testing.
  - Best practices to look for:
    - Repository pattern
    - Model implementation:  Models with users should have a type of user class, not string for username.
    - Passwords and user names should not be in the source code.
    - There should be separate dev and prod appsettings.json files.  
      But, they shouldn't necessarily be in Git! The base appsettings.json should though.
- Grade git management: no non-source in repo, PRs and merging
- Grade Jira management

