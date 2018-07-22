* Equality operators are operators like **==** and **!=**.
* Relational operators are operators lile **>**, **<**, **>=** and **<=** ...
* In this exercise, we have to identify those operators which means we have to look for instructions which transfer control flow after a condition is met.
* Some infos:
    - __CMP__ subtracts the operands and sets the flags. Namely, it sets the zero flag (ZF) if the difference is zero (operands are equal).
    - __TEST__ sets the zero flag, when the result of the AND operation is zero. If two operands are equal, their bitwise AND is zero when both are zero. TEST also sets the sign flag (SF), when the most significant bit is set in the result, and the parity flag (PF), when the number of set bits is even.
    - Just remember that __TEST__ is behaving like an AND and __CMP__ like a SUB.
    - __JE__ tests the zero flag and jumps if the flag is set. __JE__ is an alias of JZ [Jump if Zero] so the disassembler cannot select one based on the opcode. JE is named such because the zero flag is set if the arguments to CMP are equal.
* So if you have something like:
    ```
    TEST EAX,EAX 
    JE some_address 
    ```
* The CPU will jump to *some_address* if and only if ZF = 1, in other words if and only if AND(EAX,EAX) = 0 which in turn it can occur if and only if EAX == 0 
* The equivalent C code is: 
    ```
    if(eax == 0) {
        goto some_address
    }
    ```
* If you look now at the snippet below, you can immediately sport the equality operator being used to check if ECX is equal to 0, which is not the case here beucase it is equal to 1.
    ```
    .text:013C100B                 mov     ecx, 1
    .text:013C1010                 test    ecx, ecx
    .text:013C1012                 jz      short loc_13C1016
    .text:013C1014                 xor     eax, eax
    .text:013C1016
    .text:013C1016 loc_13C1016:                            ; CODE XREF: _main+9j
    .text:013C1016                                         ; _main+12j
    .text:013C1016                 pop     ebp
    ```
* The condition will not be satisfied and he program will not jump to *loc_13C1016* but instead he will zero eax and continue its execution flow.
