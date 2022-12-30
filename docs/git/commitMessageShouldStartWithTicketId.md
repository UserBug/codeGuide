## Commit message should start with ticket ID

If there is a ticket id in the comment name, it will be displayed on the page of ticket in issue tracking system.  
Most modern editors allow you to do this automatically, or you can add git pre commit hook:  
[Automatically Prepend a Jira Issue ID to Git Commit](https://gist.github.com/robatron/01b9a1061e1e8b35d270)

Pay attention, since all individual commits will be merged with squash,  
the commit text is not important. The developer himself decides which text is convenient for him.    
Example of commit: ```[OOR-76] add some component```

[Automating a Ticket ID to Every Git Commit with Git Hooks](http://coderdiaries.com/automating-a-ticket-id-to-every-git-commit-with-git-hooks/)  

[bigbrassband.atlassian.net - Link git commits to Jira issue](https://bigbrassband.atlassian.net/wiki/spaces/GITCLOUD/pages/923238543)

Related: [Code Guide - Git - Feature branch name should start with ticket id](https://github.com/UserBug/codeGuide/tree/v2/docs/git/featureBranchNameShouldStartWithTicketId.md)

---

[Back to Code Guide - Git](https://github.com/UserBug/codeGuide/tree/v2/docs/git)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 