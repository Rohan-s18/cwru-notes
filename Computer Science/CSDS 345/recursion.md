# Recursion
## Author: Rohan Singh

Recursion is when a function calls itself.

But what if a function isn't bound by a name, i.e. how can we achieve recrusion if we are not allowed to call the function with the same name.

## Regular Recursion
For the factorial function, we can write the following scheme code
```
(define facotrial
    (lambda (n)
        (if (zero? n)
            1
            (* n (factorial (- n 1)))))) 
```

## Unrolling Recursion
In "Unrolling" the recrusion we replace each recursive call with the code that is the function being called. So it isn't actually doing recursion here.

One way to do it is to pass in a function that we want, in this lamdba function function that we will pass we can pass the function body that we want.

instead of doing the unroll manually, we can define it ion the following way where the number of times we have mkf is the number fo times we can call it before being "Crashed". mkf gets passed in the mkf function as many times.
```
(define fact
    ((lambda (mkf) (mkf (mkf (mkf (mkf crash))))) 
    (lambda (f)
        (lambda (n)
            (if zero? n)
                1
                (* n (f (- n 1)))))))
```

Instead of making the calls to mkf manually, we can just embed the body of the function into the next call by making a slight modification, where we now add the body alognside the function itself.

```
(define fact 
    (lambda (mkf) (mkf mkf))
    (lambda (f)
        (lambda n)
            (if (zero? n)
                1
                (* n ((f f) (- n 1)))))) 
```

Therefore, **Recursion** is when a function that can have access to its own code so it can call itself. Recursion is a fixed point of a function that generates a function where the functionn that generates it is itself.

## Generic Function Generator

The function generation doesn't have to bound by a name, this can instead be done by making a function generator of the followign format: 
```
(
(lambda (m) (m m))
    (lambda f)
        (lambda l)              ; this is the actual function body code
            ; function code 
            ; instead of the recursive call you can do this
            ( "some operations" ((f f) "the input")))

```