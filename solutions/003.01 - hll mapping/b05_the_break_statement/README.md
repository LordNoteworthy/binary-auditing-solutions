- The break statement in C programming has the following two usages:
  - When a break statement is encountered inside a loop, the loop is immediately terminated and the program control resumes at the next statement following the loop.
  - It can be used to terminate a case in the switch statement.

```
.text:00401000                 push    ebp
.text:00401001                 mov     ebp, esp
.text:00401003                 push    ecx
.text:00401004                 mov     [ebp+var_4], 0Ah
.text:0040100B                 jmp     short loc_401016
.text:0040100D ; ---------------------------------------------------------------------------
.text:0040100D
.text:0040100D loc_40100D:                             ; CODE XREF: _main:loc_401056↓j
.text:0040100D                 mov     eax, [ebp+var_4]
.text:00401010                 sub     eax, 1
.text:00401013                 mov     [ebp+var_4], eax
.text:00401016
.text:00401016 loc_401016:                             ; CODE XREF: _main+B↑j
.text:00401016                 cmp     [ebp+var_4], 0
.text:0040101A                 jle     short loc_401058
.text:0040101C                 push    offset asc_402154 ; ", "
.text:00401021                 mov     ecx, [ebp+var_4]
.text:00401024                 push    ecx
.text:00401025                 mov     ecx, ds:?cout@std@@3V?$basic_ostream@DU?$char_traits@D@std@@@1@A ; std::basic_ostream<char,std::char_traits<char>> std::cout
.text:0040102B                 call    ds:??6?$basic_ostream@DU?$char_traits@D@std@@@std@@QAEAAV01@H@Z ; std::basic_ostream<char,std::char_traits<char>>::operator<<(int)
.text:00401031                 push    eax
.text:00401032                 call    sub_401250
.text:00401037                 add     esp, 8
.text:0040103A                 cmp     [ebp+var_4], 3
.text:0040103E                 jnz     short loc_401056
.text:00401040                 push    offset aCountdownAbort ; "countdown aborted!"
.text:00401045                 mov     edx, ds:?cout@std@@3V?$basic_ostream@DU?$char_traits@D@std@@@1@A ; std::basic_ostream<char,std::char_traits<char>> std::cout
.text:0040104B                 push    edx
.text:0040104C                 call    sub_401250
.text:00401051                 add     esp, 8
.text:00401054                 jmp     short loc_401058
.text:00401056 ; ---------------------------------------------------------------------------
.text:00401056
.text:00401056 loc_401056:                             ; CODE XREF: _main+3E↑j
.text:00401056                 jmp     short loc_40100D
.text:00401058 ; ---------------------------------------------------------------------------
.text:00401058
.text:00401058 loc_401058:                             ; CODE XREF: _main+1A↑j
.text:00401058                                         ; _main+54↑j
.text:00401058                 xor     eax, eax
.text:0040105A                 mov     esp, ebp
.text:0040105C                 pop     ebp
.text:0040105D                 retn
.text:0040105D _main           endp
```

- The C pseaudo code:

```
 for ( var_4 = 10; var_4 > 0; --var_4 )
  {
    std::cout << var_4 << ", ";
    if ( var_4 == 3 ){
      std::cout << "countdown aborted!" << std::endl;
      break;
    }
  }
  return 0;
}
```
