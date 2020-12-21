- There are two constants defined as double:

```assembly
.text:00401006                 fld     ds:dbl_4020F0   ; double dbl_4020F0 = 5.0
.text:0040100C                 fstp    [ebp+var_10]
.text:0040100F                 fld     ds:dbl_4020E8   ; double dbl_4020E8 = 6.28318
```
- **fld**: Load Floating Point Value. It Pushes the source operand onto the FPU register stack.
- **fstp**:  Store Floating Point Value. It copies the value in the ST(0) register to the destination operand.
- As an addition note, in a PE file format, the **.rdata** section represents read-only data, such as literal strings, **constants**, and debug directory information. When we double click on the constant name, we can see:
```assembly
.rdata:004020E8 dbl_4020E8      dq 6.28318              ; DATA XREF: _main+Fr
.rdata:004020F0 dbl_4020F0      dq 5.0                  ; DATA XREF: _main+6r
```
- Above we can see that our constants are defined in the RDATA section.
