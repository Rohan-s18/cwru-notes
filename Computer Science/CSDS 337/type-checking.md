# Type Checking and Systems
## Author: Rohan Singh

**Static checking:** the compiler enforces programming language’s static semantics. Program properties that can be checked at compile time.


**Dynamic semantics:** checked at run time. Compiler generates verification code to enforce programming language’s dynamic semantics.


## Static Checking
Typical examples of static checking are:
  - Type checks
  - Flow-of-control checks
  - Uniqueness checks
  - Name-related checks

**One-pass compiler:** static checking in C, Pascal, Fortran, and many other languages is performed in one pass while intermediate code is generated.

**Multi-pass compiler:** static checking in Ada, Java, and C# is performed
in a separate phase, sometimes by traversing a syntax tree multiple
times.
