- The comma operator has left-to-right associativity. Two expressions separated by a comma are evaluated left to right. The left operand is always evaluated, and all side effects are completed before the right operand is evaluated.
- Commas can be used as separators in some contexts, such as function argument lists. Do not confuse the use of the comma as a separator with its use as an operator; the two uses are completely different.
- Example:

  ```
  int main () {
  int i = 10, b = 20, c= 30;
  i = b, c;
  printf("%i\n", i);

  i = (b, c);
  printf("%i\n", i);
  }
  ```

- The output will be:
  ```
  20
  30
  ```
- If we look at the disassembly of this exercice, we see only a `return 0`:
  ```
  .text:00401000 ; int __cdecl main(int argc, const char **argv, const char **envp)
  .text:00401000 _main           proc near               ; CODE XREF: ___tmainCRTStartup+10A↓p
  .text:00401000
  .text:00401000 argc            = dword ptr  4
  .text:00401000 argv            = dword ptr  8
  .text:00401000 envp            = dword ptr  0Ch
  .text:00401000
  .text:00401000                 xor     eax, eax
  .text:00401002                 retn
  .text:00401002 _main           endp
  ```
- I suspect the compiler did some optimization and removed some code, if you have any idea, please let me know.
