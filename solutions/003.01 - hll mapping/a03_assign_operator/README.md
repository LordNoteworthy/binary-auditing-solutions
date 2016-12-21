* We have two local variables in our main function, and we have 3 assignments operators (=):
```
mov     [ebp+var_4], 5      -> var_4 = 5;
mov     [ebp+var_8], 6      -> var_8 = 6;
```
* Afterwards, we can see:
```
mov     eax, [ebp+var_8]        -> because in assembly, we cannot move memory to memory, we need first to move
mov     [ebp+var_4], eax        -> the variable to a register, then move the register to our second variable.
```
* So we can conclude that the last assignment is var_4 = var_8.