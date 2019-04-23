- We have two local variables in our main function, and we have 3 assignments operators (=):

```
.text:00401006                 mov     [ebp+var_4], 5   -> var_4 = 5;
.text:0040100D                 mov     [ebp+var_8], 6   -> var_8 = 6;
```

- Note: because in assembly, we cannot move memory to memory, we need first to move the variable to a register, then move the register to our second variable.

```
.text:00401014                 mov     eax, [ebp+var_8]
.text:00401017                 mov     [ebp+var_4], eax
```

- So we can conclude that the last assignment is var_4 = var_8.
