### Manual Decompilation – Exercise 8

#### Assembly:

```
sub_408138 proc near
000     push ebx
004     push esi
008     mov esi, edx
008     dec esi
008     test esi, esi
008     jl short loc_40816F
008     inc esi

loc_408142:
008     xor edx, edx
008     mov dl, [eax]
008     xor ebx, ebx
008     mov bl, cl
008     add edx, ebx
008     test edx, edx
008     jge short loc_40815B
008     mov ebx, 100h
008     sub ebx, edx
008     mov edx, ebx
008     jmp short loc_408169
loc_40815B:
008     cmp edx, 100h
008     jle short loc_408169
008     sub edx, 100h
loc_408169:
008     mov [eax], dl
008     inc eax
008     dec esi
008     jnz short loc_408142
loc_40816F:
008     pop esi
004     pop ebx
000     retn
sub_408138 endp
```

#### C code:

```
void Ex8 (char* buff, int size) {

    for (int i=0; i < size, i++> {

        int tmp = *buff + a;

        if (tmp < 0)  {
            *buff = 0x100 - tmp;

        } else if (tmp > 0x100) {
            *buff -= 0x100;
        }

        buff++;
}
```