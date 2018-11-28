* __sizeof__ is an operator in C which  simply returns the amount of memory is allocated to data types.
* Our disassembly looks like:
```
.text:00401000                 push    ebp
.text:00401001                 mov     ebp, esp
.text:00401003                 push    ecx
.text:00401004                 mov     [ebp+var_4], 1 ; var_4 = sizeof(char)
.text:0040100B                 xor     eax, eax
.text:0040100D                 mov     esp, ebp
.text:0040100F                 pop     ebp
.text:00401010                 retn
.text:00401010 _main           endp
```
* As far as I know, sizeof is a __compile time__ operator, is it not obvious to guess the C code but I guess it looks like __var_4__ was set to the __sizeof(char)__ which is equal to 1.


