- A goto statement in C programming provides an unconditional jump from the 'goto' to a labeled statement in the same function.
- In our example:

```
.text:00401000                 push    ebp
.text:00401001                 mov     ebp, esp
.text:00401003                 push    ecx
.text:00401004                 mov     [ebp+var_4], 0Ah         ; var_4 = 0xA
.text:0040100B
.text:0040100B loc_40100B:                             ; CODE XREF: _main+38↓j
.text:0040100B                 push    offset asc_402154 ; ", "
.text:00401010                 mov     eax, [ebp+var_4]
.text:00401013                 push    eax
.text:00401014                 mov     ecx, ds:?cout@std@@3V?$basic_ostream@DU?$char_traits@D@std@@@1@A ; std::basic_ostream<char,std::char_traits<char>> std::cout
.text:0040101A                 call    ds:??6?$basic_ostream@DU?$char_traits@D@std@@@std@@QAEAAV01@H@Z ; std::basic_ostream<char,std::char_traits<char>>::operator<<(int)
.text:00401020                 push    eax
.text:00401021                 call    sub_401250               ; print `var_4, `
.text:00401026                 add     esp, 8
.text:00401029                 mov     ecx, [ebp+var_4]
.text:0040102C                 sub     ecx, 1
.text:0040102F                 mov     [ebp+var_4], ecx         ; var_4--
.text:00401032                 cmp     [ebp+var_4], 0           ; check if var_4 <= 0 ?
.text:00401036                 jle     short loc_40103A         ; if true, jump to loc_40103A
.text:00401038                 jmp     short loc_40100B         ; goto loc_40100B
.text:0040103A ; ---------------------------------------------------------------------------
.text:0040103A
.text:0040103A loc_40103A:                             ; CODE XREF: _main+36↑j
.text:0040103A                 push    offset aFire    ; "FIRE!\n"
.text:0040103F                 mov     edx, ds:?cout@std@@3V?$basic_ostream@DU?$char_traits@D@std@@@1@A ; std::basic_ostream<char,std::char_traits<char>> std::cout
.text:00401045                 push    edx
.text:00401046                 call    sub_401250
.text:0040104B                 add     esp, 8
.text:0040104E                 xor     eax, eax
.text:00401050                 mov     esp, ebp
.text:00401052                 pop     ebp
.text:00401053                 retn
.text:00401053 _main           endp
```

- The C pseaudo code:

```
int var_4 = 10;
start:
    std::cout << var_4 << ", ";
    --var_4;
    if ( var_4 > 0 )
        goto start;

std::cout << ""FIRE!\n";
return 0;

```
