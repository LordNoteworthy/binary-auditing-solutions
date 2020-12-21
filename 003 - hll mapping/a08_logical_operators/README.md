- Following table shows the logical operators:

  <p align="center"><img src="https://i.imgur.com/YMPb8v8.png" width="400px" height="auto" alt="Logical Operators"></p>

- Here is our disassembly of the exercice with some comments:

  ```assembly
  .text:00401000                 push    ebp
  .text:00401001                 mov     ebp, esp
  .text:00401003                 sub     esp, 8             ; reserve space for 2 local vars
  .text:00401006                 xor     eax, eax           ; xoring a value with itself make it 0, ZF = 1
  .text:00401008                 jz      short loc_401011   ; the jump will be taken because of the previous op
  .text:0040100A                 mov     [ebp+var_4], 5
  .text:00401011
  .text:00401011 loc_401011:                             ; CODE XREF: _main+8j
  .text:00401011                 mov     ecx, 1             ; ecx = 1
  .text:00401016                 test    ecx, ecx           ; ECX tested against itself + ECX != 0 -> ZF = 0
  .text:00401018                 jz      short loc_401021   ; the jump will not be taken
  .text:0040101A                 mov     [ebp+var_8], 6     ; var_8 = 6
  .text:00401021
  .text:00401021 loc_401021:                             ; CODE XREF: _main+18j
  .text:00401021                 xor     eax, eax
  .text:00401023                 mov     esp, ebp
  .text:00401025                 pop     ebp
  .text:00401026                 retn
  .text:00401026 _main           endp
  .text:00401026
  ```

- If we translate that to C code:

  ```
  int main ()
  {
      int a, b;

      if (!1)         // Here we can see the logical operator `!`
          a = 5;

      if (!0)         // Again here, we can see the logical operator `!`
          b = 6;

      return 0;
  }
  ```

- The author of of the exercice could give a better example here :) to demonstrate the `&&` and the `||`.
