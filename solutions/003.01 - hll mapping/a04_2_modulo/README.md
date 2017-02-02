* The DIV instruction (and it's counterpart IDIV for signed numbers) gives both the quotient and remainder (modulo).
* lways divides the 64 bits value across EDX:EAX by a value.
* The result of the division is stored in EAX (quotient) and the remainder in EDX (modulo).
* An alternative approach would be using the AND operator because logical operations and bit-shifting is always faster and better than using DIV/IDIV.
* For example, lets take the random value in Reg. EAX , modulo 64.
* The simplest way would be : AND EAX, 63 (=111111 in binary).
* Important to note that this only works for powers of 2.
* In the file, I was not able to find any of the following instructions. I am not sure if the author takes into consideration the code of the C-Runtime, if you have any comments, please make a comment.





