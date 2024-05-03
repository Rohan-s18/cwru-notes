# Denotational Semantics
## Author: Rohan Singh

Denotational Semantics is an approach of formalizing the meanings of programming languages by constructing mathematical objects that describe the meanings of expressions from the languages.

## Simple Mathematical Constructs
For fairly simple mappings such as integers and booleans we will need a mapping from strings to int/boolean. For this purpose we can define:

```
M_int := mapping from string to int or error
M_bool := mapping from string to {true, false} or error
M_name := mapping from a string to a valid variable name
```


## Program State

The program state refers the denotational semantics rules for variables, i.e. a Mathematical object that represents the program memory.

The state of a program is a set that stores the pairs:
$$(\text{variable name}, \text{variable value})$$

Now in addition to just strings, we need to add the programm state as an input for all of the mappings (such as M_int, M_bool etc.)

We can now get a more generalized mapping:
```
M_int(<val1> + <val2>, s) := 
    if M_int(<val1>, s) = error or M_int(<val2>, s) = error:
        error
    else 
        M_int(<val1>, s) + M_int(<val2>, s)
```


**M_state** maps how a construct of a language changes the state.


### Assignment Semantics
Let us see how an assignment \<variable> = \<val> will affect the current program state $s$:

```
M_state(<var> = <val>, s) :=
    if M_int(<val>, s) = error or M_name(<var>) = error:
        error
    else:
        s1 = RemoveBinding(M_name(<var>), s)
        s2 = AddBinding(M_name(<var>), M_int(<val>, s1), s)
```
Here AddBinding and RemoveBinding are helper functions that add/remove bindings between variable names and variable values in the state.

### Conditional Semantics
Let us now see how we can map conditional if/else statements using mathematical objects:

```
M_state(if (<condition>) <stmt1> else <stmt2>, s) := 
    if M_bool (<condition>, s) = true:
        M_state(<stmt1>, s)
    else:
        M_state(<stmt2>, s)
```

### Structured Flow Control
Let us now see how we can map conditional flow control (while) statements using mathematical objects:

```
M_state(while (<condition>) <stmt>, s) :=
    if M_bool (<condition>, s) = true:
        M_state(while (<condition>) <stmt>, M_state(<stmt1>, s))
    else:
        s
```

## Unstructured Flow Control
This refers to the flow control for stuff such as goto, break, continue and throw. This can be achieved by using continuation functions that makes the M_state mapping "tail-recursive". This is obtained by adding passing a continuation for that unstructured flow control at the end of the M_state and write the CPS code for the function such as break, catch, finally by passing the mapping ot the executable body to it in the M_state function.

### Break Semantics
We can achieve the break statement by passing a continuation function **next** to the M_state mapping and adding a function **repeat** which executes the body of the statement and passs it as the next for the while loop to make it tail recursive. This changes the while-loop denotational semantics to:
```
M_state(while (<condition>) <stmt>, s, next) :=
    if M_bool (<condition>, s) = true:
        repeat := f(s1) -> M_state(while (<condition>) <stmt>, s1, next)
        M_state(<stmt>, s, repeat)
    else:
        next(s)
```
In order to incorporate break, we need to use a helper function for the M_state mapping function:
```
M_state(while <condition> <body>, s, next, oldbreak) :=
    break := f(s1) -> next(s_1)
    loop(<condition>, <body>, s, next, break)

loop(condition, body, s, next, break) :=
    if M_bool (condition, s) = true:
        repeat := f(s1) -> loop(condition, body, s1, next, break)
        M_state(body, s, repeat, break)
    else:
        next(s)

```


### Exception Handling