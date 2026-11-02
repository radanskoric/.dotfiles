---
name: better-tests
description: Use when implementing automated tests or when reviewing and improving existing automated tests.
---

Apply the guidelines in this skill in one of two ways:
1. **For new features**: Use the red/green TDD approach. Examine the planned changes and plan the failing test according to the guidelines in this skill.
2. **For existing tests**: Review and refactor the test code to follow the guidelines in this skill.

## Core Testing Philosophy  

Write **thorough, stable, fast, and few** tests. Focus on testing the **interface, not the implementation**. Every test should have a clear purpose and add value without redundancy.  

## The Message Grid: What to Test and How  

All code interactions can be categorized by **message origin** (incoming, outgoing, sent to self) and **message type** (query or command):  
1. Incoming Query Messages  
**Rule**: Test by making assertions about what they return  

- **What**: Public methods that return values without side effects
- **How**: Create object instance, send message, assert on return value
- **Example**: Testing a `diameter` method that calculates and returns a value
- **Key Point**: Test the interface, ignore internal implementation

2. Incoming Command Messages  
**Rule**: Test by making assertions about direct public side effects  

- **What**: Public methods that change object state
- **How**: Send message, assert on the resulting state change
- **Example**: Testing a `set_cog(value)` method by asserting the new cog value
- **Key Point**: Only test direct, public side effects owned by this class

3. Messages Sent to Self (Private Methods)  
**Rule**: Don't test them directly  

- **What**: Private methods called internally
- **How**: Don't create explicit tests; they're covered by public interface tests
- **Why**: Private methods are implementation details, not part of the public contract
- **Exception**: May temporarily test complex private algorithms during development, but delete these tests once stable

4. Outgoing Query Messages  
**Rule**: Don't test them  

- **What**: Messages sent to collaborators that return values without side effects
- **How**: Ignore completely in unit tests
- **Why**: The collaborator is responsible for testing its own return values
- **Anti-pattern**: Don't mock or assert on query message calls

5. Outgoing Command Messages  
**Rule**: Test that the message gets sent (use mocks)  

- **What**: Messages sent to collaborators that have side effects
- **How**: Mock the collaborator, set expectation that message is sent
- **Why**: This object is responsible for sending the message, not for the distant side effect
- **Key Point**: Test at the nearest edge, not the distant side effect

6. Messages Sent to Self (Commands)  
**Rule**: Don't test them directly  

- **Same as private methods - covered by public interface tests**

## Key Testing Principles  

### Test Location Responsibility  

- **Incoming messages**: Test in the receiver (this class)
- **Outgoing messages**: Test in the sender only if they're commands
- **Value assertions**: Only make them for incoming messages to this object

### Mock Usage Guidelines  

- Use mocks **only** for outgoing command messages
- Keep mocks in sync with real APIs (use tools that verify mock contracts)
- Mock the **nearest edge**, not distant side effects
- Prefer real objects when side effects are cheap and close

### What NOT to Test  

- Private methods directly
- Outgoing query messages
- Implementation details
- Distant side effects (that's integration testing)
- Values returned by collaborators (they test themselves)

### Common Anti-Patterns to Avoid  

1. **Over-specification**: Testing implementation details that can change
2. **Redundant assertions**: Testing the same thing in multiple places
3. **Integration tests disguised as unit tests**: Reaching across multiple objects
4. **Testing private methods**: Creates brittleness without value
5. **Mocking queries**: Unnecessary and creates coupling

## Benefits of Following These Rules  

- **Thorough**: Every behavior tested exactly once in the right place
- **Stable**: Tests don't break when implementation changes
- **Fast**: No waiting for distant side effects or complex setups
- **Few**: Minimal test code to maintain
- **Refactor-safe**: Can change implementation without breaking tests

## Testing Mindset  

- Think of objects as **black boxes** with clear boundaries
- Focus on **messages and their contracts**, not internal mechanics
- **Trust collaborators** to do their job correctly
- Write tests that make it **safe and cheap to refactor**
- Delete unnecessary tests - fewer, better tests are more valuable

## Decision Framework  
For any piece of code, ask:  

1. **What type of message is this?** (incoming/outgoing/self, query/command)
2. **What is this object responsible for?** (sending the message vs. handling the result)
3. **Does this test add unique value?** (or is it redundant/over-specified)
4. **Will this test break when I refactor implementation?** (if yes, reconsider)

Remember: **Good tests are not magic, they're magic tricks** - learnable patterns that create stable, valuable test suite
