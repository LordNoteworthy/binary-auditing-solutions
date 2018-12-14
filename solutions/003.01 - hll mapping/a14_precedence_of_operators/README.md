* Operator precedence determines the grouping of terms in an expression and decides how an expression is evaluated. Certain operators have higher precedence than others; for example, the multiplication operator has a higher precedence than the addition operator.
* Our exercice:
```
.text:00401000                 push    ebp
.text:00401001                 mov     ebp, esp
.text:00401003                 push    ecx
.text:00401004                 mov     [ebp+var_4], 6
.text:0040100B                 mov     [ebp+var_4], 6
.text:00401012                 mov     [ebp+var_4], 0
.text:00401019                 xor     eax, eax
.text:0040101B                 mov     esp, ebp
.text:0040101D                 pop     ebp
.text:0040101E                 retn
.text:0040101E _main           endp
```
* Well, that is not obvious here to guess the C code. Please, let me know if you can figure this out.