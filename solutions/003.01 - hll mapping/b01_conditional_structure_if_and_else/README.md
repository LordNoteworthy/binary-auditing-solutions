* We have two local variables __var_4__ and __var_8__. var_4 is assigned the value 0.
```
.text:00401000                 push    ebp
.text:00401001                 mov     ebp, esp
.text:00401003                 sub     esp, 8
.text:00401006                 mov     [ebp+var_4], 0  ; var_4 = 0
.text:0040100D                 cmp     [ebp+var_4], 0
.text:00401011                 jle     short loc_40101C ; jump if (var_4 <= 0)
.text:00401013                 mov     [ebp+var_8], 1  ; var_8 = 1
.text:0040101A                 jmp     short exit
.text:0040101C ; ---------------------------------------------------------------------------
.text:0040101C
.text:0040101C loc_40101C:                             ; CODE XREF: _main+11↑j
.text:0040101C                 cmp     [ebp+var_4], 0
.text:00401020                 jge     short loc_40102B ; jump if (var_4 >= 0)
.text:00401022                 mov     [ebp+var_8], 2  ; var_8 = 2
.text:00401029                 jmp     short exit
.text:0040102B ; ---------------------------------------------------------------------------
.text:0040102B
.text:0040102B loc_40102B:                             ; CODE XREF: _main+20↑j
.text:0040102B                 mov     [ebp+var_8], 0  ; var_8 = 0
.text:00401032
.text:00401032 exit:                                   ; CODE XREF: _main+1A↑j
.text:00401032                                         ; _main+29↑j
.text:00401032                 xor     eax, eax
.text:00401034                 mov     esp, ebp
.text:00401036                 pop     ebp
.text:00401037                 retn
.text:00401037 _main           endp
```
* C pseaudo-code:
```
int var_4, var_8;
var_4 = 0;

if (var_4 > 0) {
    var_8 = 1
} else {
    if (var_4 < 0) {
        var_8 = 2;
    }
    else {
        var_8 = 0;
    }
}
return 0;
```