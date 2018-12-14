* The __continue__ statement in C programming works somewhat like the break statement. Instead of forcing termination, it forces the next iteration of the loop to take place, skipping any code in between.
```
.text:00401000                 push    ebp
.text:00401001                 mov     ebp, esp
.text:00401003                 push    ecx
.text:00401004                 mov     [ebp+var_4], 0Ah
.text:0040100B                 jmp     short loc_401016
.text:0040100D ; ---------------------------------------------------------------------------
.text:0040100D
.text:0040100D continue:                               ; CODE XREF: _main+22↓j
.text:0040100D                                         ; _main+42↓j
.text:0040100D                 mov     eax, [ebp+var_4]
.text:00401010                 sub     eax, 1
.text:00401013                 mov     [ebp+var_4], eax
.text:00401016
.text:00401016 loc_401016:                             ; CODE XREF: _main+B↑j
.text:00401016                 cmp     [ebp+var_4], 0
.text:0040101A                 jle     short end
.text:0040101C                 cmp     [ebp+var_4], 5
.text:00401020                 jnz     short loc_401024
.text:00401022                 jmp     short continue
.text:00401024 ; ---------------------------------------------------------------------------
.text:00401024
.text:00401024 loc_401024:                             ; CODE XREF: _main+20↑j
.text:00401024                 push    offset asc_402154 ; ", "
.text:00401029                 mov     ecx, [ebp+var_4]
.text:0040102C                 push    ecx
.text:0040102D                 mov     ecx, ds:?cout@std@@3V?$basic_ostream@DU?$char_traits@D@std@@@1@A ; std::basic_ostream<char,std::char_traits<char>> std::cout
.text:00401033                 call    ds:??6?$basic_ostream@DU?$char_traits@D@std@@@std@@QAEAAV01@H@Z ; std::basic_ostream<char,std::char_traits<char>>::operator<<(int)
.text:00401039                 push    eax
.text:0040103A                 call    sub_401250
.text:0040103F                 add     esp, 8
.text:00401042                 jmp     short continue
.text:00401044 ; ---------------------------------------------------------------------------
.text:00401044
.text:00401044 end:                                    ; CODE XREF: _main+1A↑j
.text:00401044                 push    offset aFire    ; "FIRE!\n"
.text:00401049                 mov     edx, ds:?cout@std@@3V?$basic_ostream@DU?$char_traits@D@std@@@1@A ; std::basic_ostream<char,std::char_traits<char>> std::cout
.text:0040104F                 push    edx
.text:00401050                 call    sub_401250
.text:00401055                 add     esp, 8
.text:00401058                 xor     eax, eax
.text:0040105A                 mov     esp, ebp
.text:0040105C                 pop     ebp
.text:0040105D                 retn
.text:0040105D _main           endp
```
* The C pseaudo code:
```
for ( var_4 = 10; var_4 > 0; --var_4 ) {

    if ( i == 5 ) 
        continue;

    std::cout << var_4 << ", ";
}

std::cout << "FIRE!\n";
return 0;
```
