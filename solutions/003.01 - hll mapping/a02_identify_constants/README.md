* There are two constants defined as double:
```
.text:00401006                 fld     ds:dbl_4020F0   ; double dbl_4020F0 = 5.0
.text:0040100C                 fstp    [ebp+var_10]
.text:0040100F                 fld     ds:dbl_4020E8   ; double dbl_4020E8 = 6.28318
```

* As an addition note, in a PE file format, the .rdata section represents read-only data, such as literal strings, **constants**, and debug directory information. When we double click on the constant name, we can see:
```
.rdata:004020E8 dbl_4020E8      dq 6.28318              ; DATA XREF: _main+Fr
.rdata:004020F0 dbl_4020F0      dq 5.0                  ; DATA XREF: _main+6r
```
* Above we can see that our constants are defined in the RDATA section.