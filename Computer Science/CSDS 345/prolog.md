# Prolog 
## Author: Rohan Singh

Prolog is a logical programming language that is basically like a database.

These are som eof the basic rules of prolog:  
  - "%" is used for comments.
  - Variables start with an uppercase letter, everything else is lowercase.  
  - Database facts end in a period.
  - Queries start with "?-"  
  - A rule is of the form "A:- B,C,D". This means B && C && D implies A

## Simple Logical Database
Here is a smaple logical database for a family

```
parentof(dhruva, rohan).
parentof(nimisha, rohan).
parentof(claire, emile).
parentof(vikram, emile).
parentof(dhruva, nishita).
parentof(nimisha, nishita)
parentof(claire, yanik).
parentof(vikram, yanik).
```

Queries
```
?- parentof(dhruva, rohan).                 [returns yes]
?- parentof(dada, dhruva).                  [returns no, because it is not defined]
?- parentof(X, rohan)                       [returns, X = dhruva, you can continue searching by adding a ";"]
```

## Simple Logical Rules
To define a rule we use "A:- B,C,D". This means B && C && D implies A. So to define grandparents from the previous example we can define it as:
```
grandparentof(X,Y) :- parentof(X,A), parentof(A, Y).
```

A more complex one is siblings which can be defined as:
```
siblingof(A,B) :- parentof(X,A),parentof(X,B), A/=B.
```

## Lists
My append in Prolog. This is similar to pattern matching from haskell and uses a recursive deinition. unlike haskell, in prolog we have to define how the ouut looks like too.
```
% myappend(input1, input2, output)
myappend([], L2, L2).
myappend([H|T], L2, [H|S]) :- myappend(T, L2, S).
```
