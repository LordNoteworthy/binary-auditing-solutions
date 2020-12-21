- C++ uses heaviy the __ecx__ register as a pointer to the __this__ object.

```assembly
.text:00F61040 ; int __cdecl main(int argc, const char **argv, const char **envp)
.text:00F61040 _main           proc near               ; CODE XREF: ___tmainCRTStartup+10A↓p
.text:00F61040
.text:00F61040 var_8           = dword ptr -8
.text:00F61040 argc            = dword ptr  8
.text:00F61040 argv            = dword ptr  0Ch
.text:00F61040 envp            = dword ptr  10h
.text:00F61040
.text:00F61040                 push    ebp
.text:00F61041                 mov     ebp, esp
.text:00F61043                 sub     esp, 8           ; Allocate space for our MyObj{x, y}
.text:00F61046                 push    4                ; Push MyObj.y
.text:00F61048                 push    3                ; Push MyObj.x
.text:00F6104A                 lea     ecx, [ebp+var_8] ; ecx point to MyObj
.text:00F6104D                 call    ?                InitializeTicket@ClaimTicket@VirtualProcessor@details@Concurrency@@AAEXW4AvailabilityType@234@PAV234@@Z ; Concurrency::details::VirtualProcessor::ClaimTicket::InitializeTicket(Concurrency::details::VirtualProcessor::AvailabilityType,Concurrency::details::VirtualProcessor *)
.text:00F61052                 lea     ecx, [ebp+var_8]
.text:00F61055                 call    sub_F61000       ; Calculate the area, x*y
.text:00F6105A                 push    eax
.text:00F6105B                 push    offset aArea    ; "area: "
.text:00F61060                 mov     eax, ds:?cout@std@@3V?$basic_ostream@DU?$char_traits@D@std@@@1@A ; std::ostream std::cout
.text:00F61065                 push    eax
.text:00F61066                 call    sub_F61270
.text:00F6106B                 add     esp, 8
.text:00F6106E                 mov     ecx, eax
.text:00F61070                 call    ds:??6?$basic_ostream@DU?$char_traits@D@std@@@std@@QAEAAV01@H@Z ; std::ostream::operator<<(int)
.text:00F61076                 xor     eax, eax
.text:00F61078                 mov     esp, ebp
.text:00F6107A                 pop     ebp
.text:00F6107B                 retn
.text:00F6107B _main           endp
```

- At 0x00F6104D is the object creation, we call the constructor to initialize the object we want to calculate the area for.
- It takes 
```assembly
.text:00F61020 ; private: void __thiscall Concurrency::details::VirtualProcessor::ClaimTicket::InitializeTicket(enum Concurrency::details::VirtualProcessor::AvailabilityType, class Concurrency::details::VirtualProcessor *)
.text:00F61020 ?InitializeTicket@ClaimTicket@VirtualProcessor@details@Concurrency@@AAEXW4AvailabilityType@234@PAV234@@Z proc near
.text:00F61020                                         ; CODE XREF: _main+D↓p
.text:00F61020
.text:00F61020 var_4           = dword ptr -4               ; this
.text:00F61020 arg_0           = dword ptr  8
.text:00F61020 arg_4           = dword ptr  0Ch
.text:00F61020
.text:00F61020                 push    ebp
.text:00F61021                 mov     ebp, esp
.text:00F61023                 push    ecx
.text:00F61024                 mov     [ebp+var_4], ecx
.text:00F61027                 mov     eax, [ebp+var_4]
.text:00F6102A                 mov     ecx, [ebp+arg_0]
.text:00F6102D                 mov     [eax], ecx           ; this.x = arg0
.text:00F6102F                 mov     edx, [ebp+var_4]
.text:00F61032                 mov     eax, [ebp+arg_4] 
.text:00F61035                 mov     [edx+4], eax         ; this.y = arg4
.text:00F61038                 mov     esp, ebp
.text:00F6103A                 pop     ebp
.text:00F6103B                 retn    8
.text:00F6103B ?InitializeTicket@ClaimTicket@VirtualProcessor@details@Concurrency@@AAEXW4AvailabilityType@234@PAV234@@Z endp
```

- The area function calculate simply the area of the object:
```assembly
.text:00F61000 Area            proc near               ; CODE XREF: _main+15↓p
.text:00F61000
.text:00F61000 var_4           = dword ptr -4               ; this
.text:00F61000
.text:00F61000                 push    ebp
.text:00F61001                 mov     ebp, esp
.text:00F61003                 push    ecx
.text:00F61004                 mov     [ebp+var_4], ecx
.text:00F61007                 mov     eax, [ebp+var_4]
.text:00F6100A                 mov     ecx, [ebp+var_4]
.text:00F6100D                 mov     eax, [eax]           ; eax = this.x
.text:00F6100F                 imul    eax, [ecx+4]         ; eax = eax * this.y
.text:00F61013                 mov     esp, ebp
.text:00F61015                 pop     ebp
.text:00F61016                 retn
.text:00F61016 Area            endp
```

- C equivalent code:

```cpp;
class MyObject
{
public:
    MyObject(int _x, int _y) { x = _x; y = _y; };
    int Area() { return x * y; }
private:
    int x;
    int y;
};

int main()
{
    MyObject o = MyObject(3, 4);
    std::cout << "area: " << o.Area() << std::endl;
}
```