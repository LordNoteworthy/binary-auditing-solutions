- **Compound assignment** is the name given to certain assignment operators in certain programming languages (especially those derived from C).
- An compound assignment is generally used to replace a statement where an operator takes a variable as one of its arguments and then assigns the result back to the same variable.
- A simple example is `x += 1` which is expanded to `x = x + 1`. Similar constructions are often available for various binary operators.
- Remember that memory to memory operation is not permitted in assembly, it should be always first copied to a register, do the math and copy back from the register to memory.

1. The first compound assignment (var_4 += 6):

```
.text:0040101B                 mov     eax, [ebp+var_4] ; eax = var_4
.text:0040101E                 add     eax, 6           ; eax = eax + 6
.text:00401021                 mov     [ebp+var_4], eax ; var_4 = eax
```

2. The second compound assignment (var_8 -= 5):

```
.text:00401024                 mov     ecx, [ebp+var_8] ; ecx = var_8
.text:00401027                 sub     ecx, 5           ; ecx = ecx - 5
.text:0040102A                 mov     [ebp+var_8], ecx ; var_8 = ecx
```

3. The third compound assignment (var_C \*= 3):

```
.text:0040102D                 mov     edx, [ebp+var_C] ; edx = var_C
.text:00401030                 imul    edx, 3           ; edx = edx * 3
.text:00401033                 mov     [ebp+var_C]      ; var_C = edx
```
