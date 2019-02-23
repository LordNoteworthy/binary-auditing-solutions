### Manual Decompilation – Exercise 6

#### Assembly

```
proc near
    V1 = dword ptr 8
    V2 = dword ptr 0Ch
    V3 = dword ptr 10h
    V4 = dword ptr 14h

    push ebp
    mov ebp, esp
    push esi
    push edi
    mov edi, [ebp+V4]
    mov esi, [ebp+V3]
    mov edx, [ebp+V2]
    mov eax, [ebp+V1]
    test edi, edi
    jnz short loc_40122C
    xor eax, eax
    jmp short loc_401237
    loc_401219:
    mov ecx, esi
    cmp cl, [edx]
    jz short loc_401227
    mov cl, [edx]
    mov [eax], cl
    inc edx
    inc eax
    jmp short loc_40122C
loc_401227:
    mov [eax], cl
    inc eax
    jmp short loc_401237
loc_40122C:
    mov ecx, edi
    add edi, -1
    test ecx, ecx
    jnz short loc_401219
    xor eax, eax
loc_401237:
    pop edi
    pop esi
    pop ebp
    retn
endp
```

#### C code:

```
char* Ex6 (char* V1, char* V2, char* V3, int V4) {

    if (V4 == 0) {
        return 0;
    }

    do {
        V4--;

        if (*V2 == *V3) {
            *V1 = *V3;
            V1++;
            return V1
        }

        *V1 = *V2;
        V1++; V2++;
     } while (V4 != 0) ;

    return 0;
}
```