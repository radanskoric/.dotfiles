---
name: resolve-rebase-conflict
description: Resolve a git rebase conflict.
disable-model-invocation: true
---

I am performing a git rebase and I ran into conflicts.

Analyse the change, check the surrounding code, the history of the current branch, and the target branch and resolve the conflict.

Assume that the target branch is the more authoritative answer. If a conflict doesn't have a clear resolution, stop and ask for my feedback. 

Do not stage the changes, just resolve the conflicts and give me a summary of the changes.
