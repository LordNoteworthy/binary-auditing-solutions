- From msdn documentation regarding the `new` operator:
- _The new operator invokes the function operator new. For arrays of any type, and for objects that are not of class, struct, or union types, a global function, ::operator new, is called to allocate storage. Class-type objects can define their own operator new static member function on a per-class basis. When the compiler encounters the new operator to allocate an object of type type, it issues a call to type::operator new( sizeof( type ) ) or, if no user-defined operator new is defined, ::operator new( sizeof( type ) ). Therefore, the new operator can allocate the correct amount of memory for the object._
- Basically, it would be just a caller that have as argument the number of bytes to allocate.
- In this example: we allocate 0x14 bytes = 20d = 5 dwords.

```
; int __cdecl main(int argc, const char **argv, const char **envp)
_main proc near

var_8= dword ptr -8
var_4= dword ptr -4
argc= dword ptr  8
argv= dword ptr  0Ch
envp= dword ptr  10h

push    ebp
mov     ebp, esp
sub     esp, 8
push    14h             ; unsigned int
call    ??2@YAPAXI@Z    ; operator new(uint)
add     esp, 4
mov     [ebp+var_8], eax
mov     eax, [ebp+var_8]
mov     [ebp+var_4], eax
mov     ecx, [ebp+var_4]
mov     dword ptr [ecx], 1
mov     edx, [ebp+var_4]
mov     dword ptr [edx+4], 2
mov     eax, [ebp+var_4]
mov     dword ptr [eax+8], 3
mov     ecx, [ebp+var_4]
mov     dword ptr [ecx+0Ch], 4
mov     edx, [ebp+var_4]
mov     dword ptr [edx+10h], 5
xor     eax, eax
mov     esp, ebp
pop     ebp
retn
_main endp
```

- C pseaudo code:

```
main(int argc, const char **argv, const char **envp) {

	int *var_4, *var_8;
	int *arr = new int[5];

	var_8 = arr;
	var_4 = arr;
	*var_4 = 1;
	*(var_4 + 1) = 2;
	*(var_4 + 2) = 3;
	*(var_4 + 3) = 4;
	*(var_4 + 4) = 5;
    
    /*
    an alternative solution 
    arr[0] = 1;
    arr[1] = 2;
    arr[2] = 3;
    arr[3] = 4;
    arr[4] = 5;
    */

    return 0;
}
```