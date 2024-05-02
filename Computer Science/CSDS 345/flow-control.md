# Flow Control
## Author: Rohan Singh
Flow control refers to how code moves from line to line.

## Unstructures Flow Control
Unstructed flow Control refers to the unconditional changes in the flow of the code by jumping over other code such as **goto, break, try/catch** etc.

In unstructured flow control, we use continuation passing style to add the arguments for break, next, continue, throw etc.

In general, to add unstructured flow control into our grammar we will update the M-state mapping to make it tail recursive by adding a **next** continuation which refers to what we want to happen after we do the loop. 

```
M_state <-  stmt, state, next
```

### Try/Catch
Whenever a try/catch is trhown we add continuation passing style form of states to go to the finally statement as the next block. That is the **next** continuation is the finally continuation for the try and catch blocks.