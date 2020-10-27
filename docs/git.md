## Git

### Branching strategy
Recommended strategies:

* [GitHub flow](https://guides.github.com/introduction/flow/index.html) 
* [GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html) 
* [Git Flow](https://nvie.com/posts/a-successful-git-branching-model/) 

The main points to which you need to pay attention:

* Each task is developed only in feature branch.
* It is strictly forbidden to make any commits in development branch or master.
* Merge feature branch to develop branch, should be done with squash and deleting feature branch.

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

### Often comment on changes
There is no limit on number of commits in git.  
Try to commit each complete piece of code, like function or object with data.  
Often comment give advantages:

* Easy to debug code and find properly working version.
* Easy to reorder commits or "cherry pick" some of them to another branch.
* Shows progress of work.

---

### Recommended workflow
1. The task is taken for development in the current iteration.
2. __Developer__ creates a feature branch through issue tracking systems (JIRA) from develop branch.
3. __Developer__ writes the code and unit tests only in the feature branch.
4. __Developer__ merges all new changes from develop branch into his feature branch and resolve all conflicts.
5. __Developer__ do smoke testing.
6. __Developer__ create in Pull Request to develop branch, and add at least one __Reviewer__.
7. __Tester__ checks all acceptance criteria for the task,  
and performs integration testing of the features.  
Launches automated tests.
8. __Reviewer__ looks through the code and with the help of comments in the Pull Request can leave comments on improving the code.  
The __Reviewer__ informs the __Developer__ that the review is complete.
If necessary, __Developer__ makes edits and returns to step #3 
9. __Developer__ merges feature branch into the development branch.
10. __Tester__ creates a task to complete automated end-to-end testing and performs it in an independent workflow.  
(Steps #7 and #8 can be executed in parallel or reversed.)

---
Copyright © 2017 Stanislav Kochenkov 
