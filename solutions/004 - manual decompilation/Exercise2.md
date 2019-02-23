### Manual Decompilation – Exercise 1

#### Assembly:
```...
mov dword ptr [esi], 1
xor edx, edx
mov [ebx], edx
jmp short loc_4012F1
loc_4012E8:
mov ecx, [esi]
imul ecx, [esi]
mov [esi], ecx
inc dword ptr [ebx]
loc_4012F1:
cmp dword ptr [ebx], 8
jl short loc_4012E8
...
```

#### C code:
```
*p = 1;

for (*it = 0; *it < 8; *it++) {
    *p *=  *p;
}
```