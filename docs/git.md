## Git

### Basic Foundation

Any branching strategies or approaches adopted in the repository should extend from the Basic Foundation:

#### Commit often and push frequently

* Help roll back to a specific good point in time
* Helps share work to: test, get feedback, identify dependencies.
* Provides context  
  [GitLab - Commit often and push frequently](https://docs.gitlab.com/ee/topics/gitlab_flow.html#commit-often-and-push-frequently)

#### Feature branch serves the developer.

* It can contain any raw and not ready-made code
* It is not stable and can be changed or deleted by the developer at any time
* Internal commits should primarily help the developer.

#### Pull request is a confirmation from the developer that everything is ready.

* Acceptance criteria met
* Definition of Done met
* Tests completed successfully
* The developer is ready to receive feedback from the reviewers

#### The main branch of the project should always be tested and stable

---

### Recommended branching strategies:

* [GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html)
* [Git Flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
* [GitHub flow](https://docs.github.com/en/get-started/quickstart/github-flow)

---

### Feature branch recommendations

* Should have a short life.
* Should contain only one Feature.
* Should represent changes from one and only one developer.
* Should frequently pull changes from main branch.
* Should squash all commits before merged into main branch.
* Should be removed after they are merged into main branch.

---

### Any name of feature branch should start with ticket id

Availability of ticket id in name of the feature branch,  
allows people and issue tracking systems (JIRA) find and show valid links to the branch in Git repo.  
The best way to do this - is to create a branch for development directly from issue tracking systems.  
Examples of branch names: ```OOPP-76-some-feature```, ```EX-2391-some-feature```...

---

### Any git commit message should start with ticket id

If there is a ticket id in the comment name, it will be displayed on the page of ticket in issue tracking system.  
Most modern editors allow you to do this automatically, or you can add git pre commit hook:  
[Automatically Prepend a Jira Issue ID to Git Commit](https://gist.github.com/robatron/01b9a1061e1e8b35d270)

Pay attention, since all individual commits will be merged with squash,  
the commit text is not important. The developer himself decides which text is convenient for him.    
Example of commit: ```[OOR-76] add some component```

---

### Recommended workflow for Task

1. The task is taken for development in the current iteration.
2. __Developer__ creates a feature branch through issue tracking systems (JIRA) from develop branch.
3. __Developer__ writes the code and unit tests only in the feature branch.
4. __Developer__ merges all new changes from develop branch into his feature branch and resolve all conflicts.
5. __Developer__ do smoke testing.
6. __Developer__ create in Pull Request to develop branch, and add at least one __Reviewer__.
7. __Developer__ informs the __Reviewer__ that Pull Request is pending approval for feature branch.
8. __Tester__ checks all acceptance criteria for the task,  
   and performs integration testing of the features.  
   Launches automated tests.
9. __Reviewer__ looks through the code and with the help of comments in the Pull Request can leave comments on improving
   the code.  
   The __Reviewer__ informs the __Developer__ that the review is complete.
   If necessary, __Developer__ makes edits and returns to step #3
10. __Developer__ merges feature branch into the development branch and squash commits.
11. __Tester__ creates a task to complete automated end-to-end testing and performs it in an independent workflow.  
    (Steps #7 and #8 can be executed in parallel or reversed.)

### Recommended workflow for Integration

It is recommended to use the integration branch  
if the work involves the development of changes by several developers in parallel  
and its release together.

1. Tasks are accepted for development in the current iteration and distributed among the developers.
2. __Lead__ creates an integration branch from the development branch.
3. __Developer__ creates a feature branch through issue tracking systems (JIRA) from __integration__ branch.
4. __Developer__ perform regular "workflow for Task" in feature branch.
5. __Lead__ merges all new changes from develop branch into iteration branch and resolve all conflicts.
6. __Developer__ merges all new changes from iteration branch into his feature branch and resolve all conflicts.
7. __Lead__ create in Pull Request to develop branch, and add at least one __Reviewer__.
8. __Lead__ informs the __Reviewer__ that Pull Request is pending approval for integration branch.
9. __Tester__ checks all acceptance criteria for the task,  
   and performs integration testing of the features.  
   Launches automated tests.
10. __Reviewer__ looks through the code and with the help of comments in the Pull Request can leave comments on
    improving the code.  
    The __Reviewer__ informs the __Lead__ that the review is complete.
    If necessary, __Lead__ makes edits and returns to step #3
11. __Lead__ merges iteration branch into the development branch WITHOUT squash commits.

---
Copyright © 2017 Stanislav Kochenkov 
