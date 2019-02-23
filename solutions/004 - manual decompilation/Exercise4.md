### Manual Decompilation – Exercise 4

#### Assembly:

```
push ebp --> Stack frame creation, no code
mov ebp, esp
add esp, -80h --> this tell us our stack frame is 128 bytes
push ebx --> save ebx contents
mov eax, V2 --> take V2 value
mov ebx, eax --> duplicate V2 value
mov ecx, V3 --> take V3 value
imul ebx, ecx --> calculate V2 * V3 in ebx
mov V4, ebx --> “V4 = V2 * V3”, ebx holds V4 then
mov edx, V1 --> take V1 value
add edx, eax --> calculate (V1+V2) in edx
sub edx, ecx --> calculate (V1+V2) - V3
mov V1, edx --> “V1 = (V1+V2) - V3”
add ebx, edx --> calculate (V2*V3) + V1
mov V3, ebx --> “V3= V4+V1
```

#### C code:

```
{
    unsigned char buffer[128];
    V4 = V2*V3;
    V1 = V1+V2-V3;
    V3 = V4+V1;
    ...
}
```