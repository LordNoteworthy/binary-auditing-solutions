* A while loop in C repeatedly executes a target statement as long as a given condition is true:
```
The syntax of a while loop in C programming language is:

while(condition) {
   statement(s);
}
```
* In our scenario, our condition is located at _0x0040100B_, it exits the loop once local __var_4__ is less or equal to 0.
* __var_4__ was initialized to 9 at _0x00401004_.
* The code inside the loop is responsible for printing: ```9, 8, 7, 6, 5, 4, 3, 2, 1``` then after exiting the loop ```FIRE!\n```.
```
.text:00401000                 push    ebp
.text:00401001                 mov     ebp, esp
.text:00401003                 push    ecx
.text:00401004                 mov     [ebp+var_4], 9
.text:0040100B
.text:0040100B loc_40100B:                             ; CODE XREF: _main+38↓j
.text:0040100B                 cmp     [ebp+var_4], 0
.text:0040100F                 jle     short loc_40103A
.text:00401011                 push    offset asc_402154 ; ", "
.text:00401016                 mov     eax, [ebp+var_4]
.text:00401019                 push    eax
.text:0040101A                 mov     ecx, ds:?cout@std@@3V?$basic_ostream@DU?$char_traits@D@std@@@1@A ; std::basic_ostream<char,std::char_traits<char>> std::cout
.text:00401020                 call    ds:??6?$basic_ostream@DU?$char_traits@D@std@@@std@@QAEAAV01@H@Z ; std::basic_ostream<char,std::char_traits<char>>::operator<<(int)
.text:00401026                 push    eax
.text:00401027                 call    sub_401250
.text:0040102C                 add     esp, 8
.text:0040102F                 mov     ecx, [ebp+var_4]
.text:00401032                 sub     ecx, 1
.text:00401035                 mov     [ebp+var_4], ecx
.text:00401038                 jmp     short loc_40100B ; 
.text:0040103A ; ---------------------------------------------------------------------------
.text:0040103A
.text:0040103A loc_40103A:                             ; CODE XREF: _main+F↑j
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
* The C pseaudo-code will look like this:
```
int var_4 = 9;
while (var_4 < 0>) {
    printf ("%d, ", var_4);
    var_4--;
}
printf ("FIRE!\n");
```