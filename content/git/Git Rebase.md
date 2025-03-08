This command is really handy when we accident commit to wrong branch and want to change the parent branch by using `git rebase --onto`

Our current branches tree

```mermaid
---
title: Our HEAD is at the commit J
---
gitGraph
    commit id: "A"
    commit id: "B"
    commit id: "C"
    commit id: "D" type: HIGHLIGHT
    branch feature-branch
    commit id: "E"
    commit id: "F"
    commit id: "G" type: HIGHLIGHT
    branch current-feature-branch
    commit id: "H"
    commit id: "I"
    commit id: "J" type: HIGHLIGHT
```

and what we would like to achieve:

```mermaid
---
title: Our HEAD is at commit J'
---
gitGraph
    commit id: "A"
    commit id: "B"
    commit id: "C"
    commit id: "D" type: HIGHLIGHT
    branch feature-branch
    commit id: "E"
    commit id: "F"
    commit id: "G" type: HIGHLIGHT
    checkout main
    branch current-feature-branch
    commit id: "H'"
    commit id: "I'"
    commit id: "J'" type: HIGHLIGHT
```

To replace parent branch with `main`, we need to be on `current-feature-branch` branch and do
```
git rebase --onto main feature-branch
```

For general
```
git rebase --onto new-parent old-parent
```