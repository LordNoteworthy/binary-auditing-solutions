* Explicit Type Conversion: This process is also called type casting and it is user defined. Here the user can type cast the result to make it of a particular data type. Example:
```
    double x = 1.2; 
  
    // Explicit conversion from double to int 
    int sum = (int)x + 1; 
```
* In our example, we have the following scenario:
```
.text:01071006                 fld     ds:pi           ; Pushes the source operand onto the FPU register stack ST(0)
.text:0107100C                 fstp    [ebp+var_8]     ; Store the value in the ST(0) register to the destination operand
.text:0107100F                 fld     [ebp+var_8]
.text:01071012                 call    __ftol2_sse     ; Convert the float into an int using SSE, the casting is done here as this x = (int)3.14
```
* The user wants to convert the PI number to an int, which can be achieved simply by:
```
    float pi = 3.1400001;
    int a = (int)pi;
```
* The compiler optimized this convertion using SSE version of ftol2(): ```__ftol2_sse()```:.
* If you disassm ```__ftol2_sse```, this function will check if SSE instructions are supported by the CPU ```__get_sse2_info```, if yes, __cvttsd2si__ will take care the of convertion, otherwise we will fall to __ftol2() without SSE.
```
text:01071820                 cmp     dword_1073374, 0 ; Is SSE supported ? __get_sse2_info()
.text:01071827                 jz      short __ftol2
.text:01071829
.text:01071829 __ftol2_pentium4:                       ; CODE XREF: __ftol2_sse+34↓j
.text:01071829                 push    ebp
.text:0107182A                 mov     ebp, esp
.text:0107182C                 sub     esp, 8
.text:0107182F                 and     esp, 0FFFFFFF8h
.text:01071832                 fstp    [esp+0Ch+var_C]
.text:01071835                 cvttsd2si eax, [esp+0Ch+var_C] ; convert with truncation scalar double-precision floating-point values
.text:0107183A                 leave                   ; to scalar doubleword integers
.text:0107183B                 retn
.text:0107183C ; ---------------------------------------------------------------------------
.text:0107183C
.text:0107183C __ftol2_sse_excpt:
.text:0107183C                 cmp     dword_1073374, 0
.text:01071843                 jz      short __ftol2
.text:01071845                 sub     esp, 4
.text:01071848                 fnstcw  [esp+4+var_4]
.text:0107184B                 pop     eax
.text:0107184C                 and     ax, 7Fh
.text:01071850                 cmp     ax, 7Fh
.text:01071854                 jz      short __ftol2_pentium4
.text:01071856
.text:01071856 __ftol2:                                ; CODE XREF: __ftol2_sse+7↑j
.text:01071856                                         ; __ftol2_sse+23↑j
.text:01071856                 push    ebp
.text:01071857                 mov     ebp, esp
.text:01071859                 sub     esp, 20h
.text:0107185C                 and     esp, 0FFFFFFF0h
.text:0107185F                 fld     st
.text:01071861                 fst     dword ptr [esp+24h+var_C]
.text:01071865                 fistp   [esp+24h+var_14]
.text:01071869                 fild    [esp+24h+var_14]
.text:0107186D                 mov     edx, dword ptr [esp+24h+var_C]
.text:01071871                 mov     eax, dword ptr [esp+24h+var_14]
.text:01071875                 test    eax, eax
.text:01071877                 jz      short integer_QnaN_or_zero
.text:01071879
.text:01071879 arg_is_not_integer_QnaN:                ; CODE XREF: __ftol2_sse+9F↓j
.text:01071879                 fsubp   st(1), st
.text:0107187B                 test    edx, edx
.text:0107187D                 jns     short positive
.text:0107187F                 fstp    [esp+24h+var_24]
.text:01071882                 mov     ecx, [esp+24h+var_24]
.text:01071885                 xor     ecx, 80000000h
.text:0107188B                 add     ecx, 7FFFFFFFh
.text:01071891                 adc     eax, 0
.text:01071894                 mov     edx, dword ptr [esp+24h+var_14+4]
.text:01071898                 adc     edx, 0
.text:0107189B                 jmp     short localexit
.text:0107189D ; ---------------------------------------------------------------------------
.text:0107189D
.text:0107189D positive:                               ; CODE XREF: __ftol2_sse+5D↑j
.text:0107189D                 fstp    [esp+24h+var_24]
.text:010718A0                 mov     ecx, [esp+24h+var_24]
.text:010718A3                 add     ecx, 7FFFFFFFh
.text:010718A9                 sbb     eax, 0
.text:010718AC                 mov     edx, dword ptr [esp+24h+var_14+4]
.text:010718B0                 sbb     edx, 0
.text:010718B3                 jmp     short localexit
.text:010718B5 ; ---------------------------------------------------------------------------
.text:010718B5
.text:010718B5 integer_QnaN_or_zero:                   ; CODE XREF: __ftol2_sse+57↑j
.text:010718B5                 mov     edx, dword ptr [esp+24h+var_14+4]
.text:010718B9                 test    edx, 7FFFFFFFh
.text:010718BF                 jnz     short arg_is_not_integer_QnaN
.text:010718C1                 fstp    dword ptr [esp+24h+var_C]
.text:010718C5                 fstp    dword ptr [esp+24h+var_C]
.text:010718C9
.text:010718C9 localexit:                              ; CODE XREF: __ftol2_sse+7B↑j
.text:010718C9                                         ; __ftol2_sse+93↑j
.text:010718C9                 leave
.text:010718CA                 retn
.text:010718CA __ftol2_sse     endp
``` 


