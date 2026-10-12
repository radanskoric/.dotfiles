---
name: polish-code-change
description: Polish a finished code change. Intended to be invoked when the change is fully working but before it's ready to be committed. 
disable-model-invocation: true
---

Review the changes that you just made and look for opportunities to simplify it:
- Remove duplicate logic.
- Pick a simpler approach if it exists.
- Check surrounding code to see if it can be re-used to simplify the changes.
- Identify complex code and focus on either breaking it down for easier understanding or changing the approach to a simpler one. 

Overall, your goal is to make future changes and maintenance of the code you introduced easier.
