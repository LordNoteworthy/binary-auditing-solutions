1. **SUB** arithmetic operation, basically this is used to reserve space for local variables. We have 5 variables: 1 QWORD and 4 DWORD which results on 24d = 18h bytes.

```
.text:013C1003 sub     esp, 18h             ; esp = esp - 0x18
.text:013C1020 sub     ecx, [ebp+var_4]     ; ecx = ecx - var_4
```

2. ADD arithmetic operation is an addition (ADD):

```
.text:013C1017 add     eax, [ebp+var_8]     ; eax = eax +  var_8
```

3. IMUL arithmetic operation is a signed multiply:

```
.text:013C1029 imul    edx, [ebp+var_8]     ; edx = edx * var_8
```

4. IDIV arithmetic operation is a signed division, after IDIV: EAX = Quotient, EDX = Remainder.

```
.text:013C1033 cdq                                     ; EAX -> EDX:EAX (with sign)
.text:013C1034 idiv    [ebp+var_8]                     ; EDX:EAX = EAX / var_8
```
