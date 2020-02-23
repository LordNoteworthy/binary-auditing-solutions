- Increase and decrease operations are instructions like `++i` or `i++`.
- We see the _var_4_ is assigned the value 5 and _var_8_ is assigned the value 6.

1. Increase operation of _var_4_ (var_4++):

```
.text:00401014                 mov     eax, [ebp+var_4]     ; eax = var_4
.text:00401017                 add     eax, 1               ; eax = eax + 1
.text:0040101A                 mov     [ebp+var_4], eax     ; var_4 = eax
```

2. Decrease operation of _var_4_ (var_4--):

```
.text:0040101D                 mov     ecx, [ebp+var_4]     ; ecx = var_4
.text:00401020                 sub     ecx, 1               ; ecx = ecx - 1
.text:00401023                 mov     [ebp+var_4], ecx     ; var_4 = ecx
```

3. Decrease operation of _var_8_ (var_8--):

```
.text:00401026                 mov     edx, [ebp+var_8]     ; edx = var_8
.text:00401029                 sub     edx, 1               ; edx = edx - 1
.text:0040102C                 mov     [ebp+var_8]          ; var_8 = edx
```

4. Increase operation of _var_8_ (var_8++):

```
.text:0040102F                 mov     eax, [ebp+var_8]     ; eax = var_8
.text:00401032                 add     eax, 1               ; eax = eax + 1
.text:00401035                 mov     [ebp+var_8], eax     ; var_8 = eax
```
