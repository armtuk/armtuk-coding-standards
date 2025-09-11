
# Testing and Test Alongside Development.

## Test implementation
All Code function units must be implementing using the following cycle: Red, Green, Refactor.

### Red
- Step 1: for a given coding task, write a set of tests based on appropriate acceptance criteria. 
  - Include tests which cover each scenario that validate successful operation of the coding task.
  - Include tests which cover scenarios where the code is expected to fail including:
    - invalid inputs.
    - invalid underlying system states.
- Step 2: Run these test and validate that it fails.
### Green
- Step 2: Implement the functionality using the simplest and most direct solution. Execte the test and continue to fix the code implementation until the test passes. Once the test passes, move to step 3.
### Refactor
- Step 3: Refactor the implementation to follow all best practice rules. Execute the test and ensure the test passes. Continue to fix the code until the test passes. 

### Test Guidelines
- Name each test clearly and descriptively with what it's testing and the expected outcome.
- Tests must validate behavior.
- Test Removal Protocol
  - No test may be deleted or skipped unless:
    - A rationale is included in NOW.md with @test-removed
    - A code comment explains the reason (e.g., spec changed, test invalidated)