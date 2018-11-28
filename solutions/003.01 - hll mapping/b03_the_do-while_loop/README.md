* The syntax of a do...while loop in C programming language is:
```
do {
   statement(s);
} while( condition );
```
* Notice that the conditional expression appears at the end of the loop, so the statement(s) in the loop executes once before the condition is tested.
* In our scenario, our condition is located at _0x002E1042_, it exits the loop once local __var_4__ is equal to 0.
* __var_4__ was initialized to 9 at _0x002E1004_. 
* The code inside the loop is responsible for printing: ```"You entered: X \n"``` and X is between 9 and 1.
* Compared to the while loop example seen before, you can notice that the condition falls at the end of the loop.

```
.text:002E1000                 push    ebp
.text:002E1001                 mov     ebp, esp
.text:002E1003                 push    ecx
.text:002E1004                 mov     [ebp+var_4], 9
.text:002E100B
.text:002E100B loc_2E100B:                             ; CODE XREF: _main+42↓j
.text:002E100B                 push    offset asc_2E2154 ; "\n"
.text:002E1010                 mov     eax, [ebp+var_4]
.text:002E1013                 push    eax
.text:002E1014                 push    offset aYouEntered ; "You entered: "
.text:002E1019                 mov     ecx, ds:?cout@std@@3V?$basic_ostream@DU?$char_traits@D@std@@@1@A ; std::basic_ostream<char,std::char_traits<char>> std::cout
.text:002E101F                 push    ecx
.text:002E1020                 call    sub_2E1240
.text:002E1025                 add     esp, 8
.text:002E1028                 mov     ecx, eax
.text:002E102A                 call    ds:??6?$basic_ostream@DU?$char_traits@D@std@@@std@@QAEAAV01@K@Z ; std::basic_ostream<char,std::char_traits<char>>::operator<<(ulong)
.text:002E1030                 push    eax
.text:002E1031                 call    sub_2E1240
.text:002E1036                 add     esp, 8
.text:002E1039                 mov     edx, [ebp+var_4]
.text:002E103C                 sub     edx, 1
.text:002E103F                 mov     [ebp+var_4], edx
.text:002E1042                 jnz     short loc_2E100B
.text:002E1044                 xor     eax, eax
.text:002E1046                 mov     esp, ebp
.text:002E1048                 pop     ebp
.text:002E1049                 retn
.text:002E1049 _main           endp
```
* The C pseaudo-code will look like this:
```
int var_4 = 9;
do {
    printf ("You entered: %d\n", var_4);
    var_4--;
} while (var_4) ;
```