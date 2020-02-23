### Manual Decompilation – Exercise 7

#### Assembly:

```
proc near
    000 push ebx
    004 push esi
    008 xor ebx, ebx
    008 mov [eax], ebx
    008 mov ebx, ecx
    008 dec ebx
    008 test ebx, ebx
    008 jl short loc_408135
    008 inc ebx
loc_40810E:
    008 mov ecx, [eax]
    008 shl ecx, 4
    008 movzx esi, byte ptr [edx]
    008 add ecx, esi
    008 mov [eax], ecx
    008 mov ecx, [eax]
    008 and ecx, 0F0000000h
    008 test ecx, ecx
    008 jz short loc_40812D
    008 mov esi, ecx
    008 shr esi, 18h
    008 xor [eax], esi
loc_40812D:
    008 not ecx
    008 and [eax], ecx
    008 inc edx
    008 dec ebx
    008 jnz short loc_40810E
loc_408135:
    008 pop esi
    004 pop ebx
    000 retn
sub_408100 endp
```

#### C code:

* Looks like a hash routine.
```

void Ex7 (char* arg1, int* arg2, int arg3) {

    *arg2 = 0;

    while (arg3 > 0) {
        *arg2 = (arg2 << 4) + *arg1;

        int tmp = *arg2 & 0xF0000000;
        if (tmp) {
            *arg2 ^= tmp >> 0x18;
        }

        *arg2 &= !tmp;
        arg1++;
        arg3--;
    }
}
```