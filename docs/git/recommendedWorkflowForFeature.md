## Recommended workflow for Feature

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

---

[Back to Code Guide - Git](https://github.com/UserBug/codeGuide/tree/v2/docs/git)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 