# Unit Testing 

## Overview
Without tests, software entropy (the amount of disorder in a system) steeply increases and, thus, the hours you spent to develop is becomming meaningless since the code base becomes unreliable. Tests help make sure the existing functionality works, even after you introduce new features or refactor the code to better fit new requirements.

## What makes a good test or a bad test?
There are four attributes:
- Protection against regressions
- Resistance to refactoring
- Fast feedback
- Maintainability

Note that it is impossible to create a test satistying all the four attributes. *Maintainability* and *Resistance to refactoring* is non-negotiable. You can only set degrees between *Protection against regressions* and *Fast feedback*. Both of them are incompatible: End-to-end-testing is more likely to be bound for *Protectoin against regressions* while Unit-testint is more likely to be bound for *Fast feedback*.   

## Things you need to know before Testing
- System Under Test (SUT) and Collaborator
- Out-of-process dependency and shared dependency

## How do I write a test?
- One test per behavior 
- AAA patterns (Arrange, Act, and Assert)
- Naming conventions

## Mock vs Stub

