- There is two ways we can compute the `modulo` operation in assembly:
  1. The DIV instruction (and it's counterpart IDIV for signed numbers) gives both the quotient and remainder (modulo). The result of the division is stored in EAX (quotient) and the remainder in EDX (modulo).
  2. This works only if **b** is a power of **two**, then `a % b == a & (b - 1)`.
- In the exercise, I was not able to find any instructions which gives the modulo, I am wondering if the author takes into consideration the code which calls the `main()` function, if you have any suggestion, please let me know.
- Main function disassembly:

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
