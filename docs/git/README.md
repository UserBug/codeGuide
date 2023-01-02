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

### Other rules

* [Feature branch name should start with ticket id](https://github.com/UserBug/codeGuide/tree/v2/docs/git/featureBranchNameShouldStartWithTicketId.md) 
* [Commit message should start with ticket ID](https://github.com/UserBug/codeGuide/tree/v2/docs/git/commitMessageShouldStartWithTicketId.md)  
* [Recommended workflow for Feature](https://github.com/UserBug/codeGuide/tree/v2/docs/git/recommendedWorkflowForFeature.md)  
* [Recommended workflow for Integration](https://github.com/UserBug/codeGuide/tree/v2/docs/git/recommendedWorkflowForIntegration.md)  

---

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)  

---
Copyright © 2017 Stanislav Kochenkov 
