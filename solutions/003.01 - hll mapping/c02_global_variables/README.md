* There are 2 globals variables: __dword_403018__ and __dword_40301C__. They are referenced using ds:[MEM_ADDRESS]:
```
.text:00401000 ; int __cdecl main(int argc, const char **argv, const char **envp)
.text:00401000 _main           proc near               ; CODE XREF: ___tmainCRTStartup+10A↓p
.text:00401000
.text:00401000 argc            = dword ptr  8
.text:00401000 argv            = dword ptr  0Ch
.text:00401000 envp            = dword ptr  10h
.text:00401000
.text:00401000                 push    ebp
.text:00401001                 mov     ebp, esp
.text:00401003                 mov     dword_403018, 8 ; mov dword ptr ds:[0x00403018], 0x8
.text:0040100D                 mov     dword_40301C, 9 ; mov dword ptr ds:[0x0040301C], 0x9
.text:00401017                 xor     eax, eax
.text:00401019                 pop     ebp
.text:0040101A                 retn
.text:0040101A _main           endp
.text:0040101A
```
* They are defined in __.data__ section:
```
.data:00403018 dword_403018    dd 5                    ; DATA XREF: _main+3↑w
.data:0040301C dword_40301C    dd 6                    ; DATA XREF: _main+D↑w
```