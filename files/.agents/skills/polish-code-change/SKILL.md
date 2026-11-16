---
name: polish-code-change
description: Polish a finished code change. Intended to be invoked when the change is fully working but before it's ready to be committed. 
disable-model-invocation: true
---

Review the code changes that were made and look for opportunities to simplify it by evaluating each part as follows:
1. Ask yourself if this piece of code should even exist in the first place? Why was introduced and is the reason still valid given what we learned? If you can't come up with a clear reson, consider removing it.
2. Could a completely different approach lead to simpler code? If unsure or if a change would be large, ask me for feedback.  
3. Check the supporting libraries that the project already depends on and look for existing code that could be used instead of introducing new logic.
4. Check surrounding code to see if it can be re-used to simplify the changes.
5. If the code is still complex and the previous steps didn't simplify it, focus on breaking it down for easier understanding and apply the previous steps to each new smaller piece of code. 

Overall, your goal is to make future changes and maintenance of the code you introduced easier.

End the run with a high level summary of the changes made.
