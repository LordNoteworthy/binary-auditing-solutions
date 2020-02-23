### Manual Decompilation – Exercise 2

#### Assembly:

```...
mov edx, Var1
mov ecx, Var2
mov eax, edx
imul ecx        // edx, eax = Var1 * Var2
mov edx, eax    // edx = eax = LOW(Var1 * Var2)
imul edx, eax   // edx = edx * eax = LOW(Var1 * Var2) * LOW(Var1 * Var2)
mov Var3, ecx   // Var3 = Var2
...
```


#### C code:

```
...
res = (Var1 * Var2) * (Var1 * Var2);
Var3 = Var2;
...
```