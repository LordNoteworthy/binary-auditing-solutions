- The following table lists the Bitwise operators:
  <p align="center"> <img src="https://i.imgur.com/dURb9zE.png" width="auto" height="200px" alt="bitwise Operators"></p>

* We have a shift left operation:

  ```
  .text:00401028                 shl     ecx, 1 ;    SHL X, Y = X * 2 ^ Y
  ```

* And a shift right operation:

  ```
  .text:0040104A                 shr     eax, 1 ;    SHR X, Y =  X / 2 ^ Y
  ```

* And an exclusive OR:
  ```
  .text:00401051                 xor     eax, eax ;  This is equivalent to make mov eax, 0
  ```
