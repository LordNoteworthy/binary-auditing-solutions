
### Manual Decompilation – Exercise 2

#### Assembly:

```
push sPassword ; line of code
call _strlen
pop ecx
mov esi, eax
mov ebx, offset sMyPassword; ; line of code
push ebx
call _strlen
pop ecx
cmp esi, eax ; small block of code
jz short loc_4012B2
xor eax, eax
jmp short end_proc
loc_4012B2:
    push esi
    push ebx ; line of code
    push sPassword
    call _strcmp
    add esp, 8
    test eax, eax ; small block of code
    jnz short loc_4012CC
    mov eax, 1
    jmp short end_proc
loc_4012CC:
    xor eax, eax
end_proc: ; end of function
    pop esi
    pop ebx
    pop ebp
    retn
```

#### C code:

```
if (strlen(sMyPassword) != strlen(sPassword)) {
    return 0;
}

if (strcmp (sMyPassword, sPassword) == 0) {
    res = 1;
} else {
    res = 0;
}

return res;
```


* You need to explain which instruction(s) should be changed (patched) to make the function return a positive result in most common cases: change xor eax, eax, to mov eax, 1.