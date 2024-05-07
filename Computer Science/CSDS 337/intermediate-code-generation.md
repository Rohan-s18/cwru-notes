# Intermediate Code Generation

Intermediate Code Generation enables attaching a back end for the new machine to an existing front end. It also enables machine-independent code optimization. 

These include:  
  - Graphical representations (AST)
  - Postfix notation: operations on values stored on operand stack
  - Three-address code: (e.g. triples and quads)   
        x := y op z
  - Two-address code:  
        x := op y  
        which is the same as x := x op y



## Graphical representations
We can represent syntax using Abstract Syntax Trees or Directed Acyclic Graphs:

<img title="a title" alt="Alt text" src="imgs/DAG.png">

For ASTs 
<br> 

Pros: 
  - easy restructuring of code
  - expressions for intermediate code optimization  
  
Cons:  
  - memory intensive

## Postfix Noatation
<img title="a title" alt="Alt text" src="imgs/postfix.png">


## Three-Address Statements

<img title="a title" alt="Alt text" src="imgs/tac.png">

The following is a list of three-address statements:

<img title="a title" alt="Alt text" src="imgs/three-address-stmts.png">


