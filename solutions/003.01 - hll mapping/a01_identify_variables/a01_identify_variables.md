* We have only one function in our program which is the main() which was identified automatically by IDA.
* Notice how IDA tells us that this is an EBP-based stack frame used in the main function, which means the local variables and parameters will be referenced via the EBP register throughout the function.
* In general, local varible are referenced using [EBP-X] and parameters are referenced via [EBP+X].
* IDA has successfully discovered all local variables and parameters in this function. It has labeled the local variables with the prefix var_.
* All local variable are here:
```
var_38= qword ptr -38h
var_2C= dword ptr -2Ch
var_25= byte ptr -25h
var_24= dword ptr -24h
var_20= word ptr -20h
var_1C= dword ptr -1Ch
var_18= word ptr -18h
var_14= word ptr -14h
var_F= byte ptr -0Fh
var_E= byte ptr -0Eh
var_D= byte ptr -0Dh
var_C= dword ptr -0Ch
var_8= qword ptr -8
```
* BYTE: 1 byte, WORD: 2 bytes, DWORD: 4 bytes and QWORD: 8 bytes.
* For example, here is a mapping from Assembly -> C for var_D :
```
.text:00401006                 mov     [ebp+var_D], 0       -> unsigned char var_D = 0;
.text:0040100A                 mov     [ebp+var_D], 0FFh    -> var_D = 0xFF
```
* Same can be applied to the other variables.