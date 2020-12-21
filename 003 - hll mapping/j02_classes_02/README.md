- Very similar to `j01_classes_01` except that it calculates the area of 2 objects.
```assembly
.text:00401040 ; int __cdecl main(int argc, const char **argv, const char **envp)
.text:00401040 _main           proc near               ; CODE XREF: ___tmainCRTStartup+10A↓p
.text:00401040
.text:00401040 var_10          = byte ptr -10h
.text:00401040 var_8           = byte ptr -8
.text:00401040 argc            = dword ptr  8
.text:00401040 argv            = dword ptr  0Ch
.text:00401040 envp            = dword ptr  10h
.text:00401040
.text:00401040                 push    ebp
.text:00401041                 mov     ebp, esp         
.text:00401043                 sub     esp, 10h         ; space for 2 objects = 8*2    
.text:00401046                 push    4
.text:00401048                 push    3
.text:0040104A                 lea     ecx, [ebp+var_8] ; points to obj1
.text:0040104D                 call    ?        InitializeTicket@ClaimTicket@VirtualProcessor@details@Concurrency@@AAEXW4AvailabilityType@234@PAV234@@Z ; Concurrency::details::VirtualProcessor::ClaimTicket::InitializeTicket(Concurrency::details::VirtualProcessor::AvailabilityType,Concurrency::details::VirtualProcessor *)
.text:00401052                 push    6
.text:00401054                 push    5
.text:00401056                 lea     ecx, [ebp+var_10] ; points to obj2
.text:00401059                 call    ?InitializeTicket@ClaimTicket@VirtualProcessor@details@Concurrency@@AAEXW4AvailabilityType@234@PAV234@@Z ; Concurrency::details::VirtualProcessor::ClaimTicket::InitializeTicket(Concurrency::details::VirtualProcessor::AvailabilityType,Concurrency::details::VirtualProcessor *)
.text:0040105E                 mov     eax, ds:?endl@std@@YAAAV?$basic_ostream@DU?$char_traits@D@std@@@1@AAV21@@Z ; std::endl(std::ostream &)
.text:00401063                 push    eax
.text:00401064                 lea     ecx, [ebp+var_8]
.text:00401067                 call    sub_401000
.text:0040106C                 push    eax
.text:0040106D                 push    offset aRectArea ; "rect area: "
.text:00401072                 mov     ecx, ds:?cout@std@@3V?$basic_ostream@DU?$char_traits@D@std@@@1@A ; std::ostream std::cout
.text:00401078                 push    ecx
.text:00401079                 call    sub_4012C0
.text:0040107E                 add     esp, 8
.text:00401081                 mov     ecx, eax
.text:00401083                 call    ds:??6?$basic_ostream@DU?$char_traits@D@std@@@std@@QAEAAV01@H@Z ; std::ostream::operator<<(int)
.text:00401089                 mov     ecx, eax
.text:0040108B                 call    ds:??6?$basic_ostream@DU?$char_traits@D@std@@@std@@QAEAAV01@P6AAAV01@AAV01@@Z@Z ; std::ostream::operator<<(std::ostream & (*)(std::ostream &))
.text:00401091                 mov     edx, ds:?endl@std@@YAAAV?$basic_ostream@DU?$char_traits@D@std@@@1@AAV21@@Z ; std::endl(std::ostream &)
.text:00401097                 push    edx
.text:00401098                 lea     ecx, [ebp+var_10]
.text:0040109B                 call    sub_401000
.text:004010A0                 push    eax
.text:004010A1                 push    offset aRectbArea ; "rectb area: "
.text:004010A6                 mov     eax, ds:?cout@std@@3V?$basic_ostream@DU?$char_traits@D@std@@@1@A ; std::ostream std::cout
.text:004010AB                 push    eax
.text:004010AC                 call    sub_4012C0
.text:004010B1                 add     esp, 8
.text:004010B4                 mov     ecx, eax
.text:004010B6                 call    ds:??6?$basic_ostream@DU?$char_traits@D@std@@@std@@QAEAAV01@H@Z ; std::ostream::operator<<(int)
.text:004010BC                 mov     ecx, eax
.text:004010BE                 call    ds:??6?$basic_ostream@DU?$char_traits@D@std@@@std@@QAEAAV01@P6AAAV01@AAV01@@Z@Z ; std::ostream::operator<<(std::ostream & (*)(std::ostream &))
.text:004010C4                 xor     eax, eax
.text:004010C6                 mov     esp, ebp
.text:004010C8                 pop     ebp
.text:004010C9                 retn
.text:004010C9 _main           endp
```

- C equivalent code:

```cpp
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
    MyObject a = MyObject(3, 4);
    MyObject b = MyObject(5, 6);
    std::cout << "rect area: " << a.Area() << std::endl;
    std::cout << "rectb area: " << b.Area() << std::endl;
}
```