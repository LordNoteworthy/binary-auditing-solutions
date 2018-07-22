* Conditional operators return one value if condition is true and returns another value is condition is false. This operator is also called as __ternary operator__.
* Syntax:
    ```
    (Condition? true_value: false_value);
    ```
* Example :
    ```
    (A > 100  ?  0  :  1);
    ```
* In above example, if A is greater than 100, 0 is returned else 1 is returned. This is equal to if else conditional statements.
* Now, let's go back to our exercice:
    ```
    .text:00A71006                 mov     [ebp+var_4], 2
    .text:00A7100D                 mov     [ebp+var_8], 7
    .text:00A71014                 mov     eax, [ebp+var_4]
    .text:00A71017                 cmp     eax, [ebp+var_8]
    .text:00A7101A                 jle     short loc_A71024
    .text:00A7101C                 mov     ecx, [ebp+var_4]
    .text:00A7101F                 mov     [ebp+var_10], ecx
    .text:00A71022                 jmp     short loc_A7102A
    .text:00A71024 ; ---------------------------------------------------------------------------
    .text:00A71024
    .text:00A71024 loc_A71024:                             ; CODE XREF: _main+1A↑j
    .text:00A71024                 mov     edx, [ebp+var_8]
    .text:00A71027                 mov     [ebp+var_10], edx
    .text:00A7102A
    .text:00A7102A loc_A7102A:                             ; CODE XREF: _main+22↑j
    .text:00A7102A                 mov     eax, [ebp+var_10]
    .text:00A7102D                 mov     [ebp+var_C], eax
    .text:00A71030                 mov     eax, [ebp+var_C]
    ```
* If we tranlate it to C code:
```
var_10 = (var_4 <= var_8) ? var_8 : var_4;
```
* `var_4` is equal to __2__, and `var_8` is equal to __8__, as 2 is less than 8, `var_10` will be equal to `var_8`.