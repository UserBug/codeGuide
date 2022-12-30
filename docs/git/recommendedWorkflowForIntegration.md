## Recommended workflow for Integration

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

[Back to Code Guide - Git](https://github.com/UserBug/codeGuide/tree/v2/docs/git)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 