- A for loop in C repeatedly executes a target statement as long as a given condition is true:

```
The syntax of a for loop in C programming language is:

for ( init; condition; increment/decrement ) {
   statement(s);
}
```

- In our scenario, the **init** is located at _0x00401004_, our local **var_4** is set to 0xA.
- Our **condition** is located at _0x00401016_, it exits the loop once local **var_4** is less or equal to 0.
- Our **decrement** is located at _0x00401010_, our our local **var_4** is decremented by 1.
- The code inside the loop is responsible for printing: `10, 9, 8, 7, 6, 5, 4, 3, 2, 1` then after exiting the loop `FIRE!\n`.
- Notice how this is different than the while loop seen before.

```
.text:00401000                 push    ebp
.text:00401001                 mov     ebp, esp
.text:00401003                 push    ecx
.text:00401004                 mov     [ebp+var_4], 0Ah
.text:0040100B                 jmp     short loc_401016
.text:0040100D ; ---------------------------------------------------------------------------
.text:0040100D
.text:0040100D loc_40100D:                             ; CODE XREF: _main+3A↓j
.text:0040100D                 mov     eax, [ebp+var_4]
.text:00401010                 sub     eax, 1
.text:00401013                 mov     [ebp+var_4], eax
.text:00401016
.text:00401016 loc_401016:                             ; CODE XREF: _main+B↑j
.text:00401016                 cmp     [ebp+var_4], 0
.text:0040101A                 jle     short loc_40103C
.text:0040101C                 push    offset asc_402154 ; ", "
.text:00401021                 mov     ecx, [ebp+var_4]
.text:00401024                 push    ecx
.text:00401025                 mov     ecx, ds:?cout@std@@3V?$basic_ostream@DU?$char_traits@D@std@@@1@A ; std::basic_ostream<char,std::char_traits<char>> std::cout
.text:0040102B                 call    ds:??6?$basic_ostream@DU?$char_traits@D@std@@@std@@QAEAAV01@H@Z ; std::basic_ostream<char,std::char_traits<char>>::operator<<(int)
.text:00401031                 push    eax
.text:00401032                 call    sub_401250
.text:00401037                 add     esp, 8
.text:0040103A                 jmp     short loc_40100D
.text:0040103C ; ---------------------------------------------------------------------------
.text:0040103C
.text:0040103C loc_40103C:                             ; CODE XREF: _main+1A↑j
.text:0040103C                 push    offset aFire    ; "FIRE!\n"
.text:00401041                 mov     edx, ds:?cout@std@@3V?$basic_ostream@DU?$char_traits@D@std@@@1@A ; std::basic_ostream<char,std::char_traits<char>> std::cout
.text:00401047                 push    edx
.text:00401048                 call    sub_401250
.text:0040104D                 add     esp, 8
.text:00401050                 xor     eax, eax
.text:00401052                 mov     esp, ebp
.text:00401054                 pop     ebp
.text:00401055                 retn
.text:00401055 _main           endp
```

- The C pseaudo-code will look like this:

```
for (var_4 = 10; var_4 > 0; --var_4) {
    printf ("%d, ", var_4);
}
printf ("FIRE!\n");
```
