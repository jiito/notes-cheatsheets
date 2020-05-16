# Node.js testing and code quality

### improve communication between computers and engineers

## What is code quality?

- Meet the needs of customers
- Freedom from deficiencies
- Does what it is _supposed to do_
- _useful_
- _maintainable_
  - Can you do it?
  - Can others read it?]

**Goal:** continual improvement

## Coding conventions and standards

- Set of guidelines
- Programming style
- Practices
- Methods

Coding standard:

- collection of conventions

## Creating and enforcing a coding standard

- What's available?
- What the most positive?
- Briefly document each justification
  - One sentence
- Revisit the rules

Use a linter to enforce the standard

## Unit, integration, and functional testing

**Unit Testing**

- Tests an isolated unit via it's API
- Preformed in memory
  - no permanent changes
- Safe to run repeatedly
- Fast execution
- Assertions
  - Validate correctness
  - Throws error if false
  - _Examples_
    - ok
    - equal
    - deepEqual
    - ...
  - Can use Assert module
- Simulate dependencies
- Only your custom code

**Integration Testing**

- Builds on unit tests
- Combines and tests resulting combinations
- Complex
- Harder to maintain

**Functional Test**

- Focus on result not code
- Features
- **UI**
- Slower

## Testing Frameworks

Testing software is separate from the application

- Defines assertions
- Executes tests
- Reports results
- structural consistency

Tools

- Environment setup
- Application control
- Test data
- Execution control
  - subset of test

Setup

- Prepare application
- replace dependencies
- test data

Execution

- target behavior
- Capture output

Validation

- ensure results
- Assertions

Cleanup

- Application state is restored
- Allow other tests to run
