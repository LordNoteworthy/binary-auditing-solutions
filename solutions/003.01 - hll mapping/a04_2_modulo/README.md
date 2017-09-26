* The DIV instruction (and it's counterpart IDIV for signed numbers) gives both the quotient and remainder (modulo). The result of the division is stored in EAX (quotient) and the remainder in EDX (modulo).
* A modulo operation in assembly could also be achieved using an AND instruction. If you compute modulo a power of two, using bitwise AND is simpler and generally faster than performing division. If b is a power of two, a % b == a & (b - 1). For example, let's take a value in register EAX, modulo 64.
The simplest way would be AND EAX, 63, because 63 is 111111 in binary.
* In the exercise, I was not able to find any instructions which gives the modulo, I am wondering if the author takes into consideration the code which calls the Main function, if you have any suggestion, please let me know.
* Main function is:
```
.text:00401000 ; int __cdecl main(int argc, const char **argv, const char **envp)
.text:00401000 _main           proc near               ; CODE XREF: ___tmainCRTStartup+10Ap
.text:00401000
.text:00401000 var_4           = dword ptr -4
.text:00401000 argc            = dword ptr  8
.text:00401000 argv            = dword ptr  0Ch
.text:00401000 envp            = dword ptr  10h
.text:00401000
.text:00401000                 push    ebp
.text:00401001                 mov     ebp, esp
.text:00401003                 push    ecx
.text:00401004                 mov     [ebp+var_4], 2
.text:0040100B                 xor     eax, eax
.text:0040100D                 mov     esp, ebp
.text:0040100F                 pop     ebp
.text:00401010                 retn
.text:00401010 _main           endp
```




