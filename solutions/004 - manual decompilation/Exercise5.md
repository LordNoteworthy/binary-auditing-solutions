### Manual Decompilation – Exercise 5

#### Assembly:

```
proc near

arg_0 = dword ptr 8
arg_4 = dword ptr 0Ch
arg_8 = dword ptr 10h

    push ebp
    mov ebp, esp
    push ebx
    push esi
    mov ecx, [ebp+arg_8]
    mov esi, [ebp+arg_0]
    mov eax, [ebp+arg_4]
    mov edx, esi
    test ecx, ecx
    jnz short loc_40125A
    xor eax, eax
    jmp short loc_401265
loc_401254:
    mov bl, [eax]
    inc eax
    mov [edx], bl
    inc edx
loc_40125A:
    mov ebx, ecx
    add ecx, -1
    test ebx, ebx
    jnz short loc_401254
    mov eax, esi
loc_401265:
    pop esi
    pop ebx
    pop ebp
    retn
endp
```

#### C code:

```
char* memcpy (char* arg_0, char* arg_4, int arg_8) {
    if (arg_8 == 0) {
        return 0;
    }

    do {
        arg_8--;
        *(arg_4++) = *(arg_0++);
        while (arg_8 != 0) ;
    }

    return arg_4;
}
```