* Local variables are referenced using __ss:[ebp-X]__.
```
.text:00401000 ; int __cdecl main(int argc, const char **argv, const char **envp)
.text:00401000 _main           proc near               ; CODE XREF: ___tmainCRTStartup+10A↓p
.text:00401000
.text:00401000 var_C           = dword ptr -0Ch
.text:00401000 var_8           = dword ptr -8
.text:00401000 var_4           = dword ptr -4
.text:00401000 argc            = dword ptr  8
.text:00401000 argv            = dword ptr  0Ch
.text:00401000 envp            = dword ptr  10h
.text:00401000
.text:00401000                 push    ebp
.text:00401001                 mov     ebp, esp
.text:00401003                 sub     esp, 0Ch        ; We allocate space for 3 local vars
.text:00401006                 mov     [ebp+var_4], 5  ; mov dword ptr ss:[ebp-0x4], 0x5
.text:0040100D                 mov     [ebp+var_8], 6  ; mov dword ptr ss:[ebp-0x8], 0x6
.text:00401014                 mov     eax, [ebp+var_4]
.text:00401017                 add     eax, [ebp+var_8]
.text:0040101A                 mov     [ebp+var_C], eax ; mov dword ptr ss:[ebp-0xC], eax
.text:0040101D                 xor     eax, eax
.text:0040101F                 mov     esp, ebp
.text:00401021                 pop     ebp
.text:00401022                 retn
.text:00401022 _main           endp
```
* The C code will look like:
```
int a = 5;
int b = 6;
int c = a + b;
```