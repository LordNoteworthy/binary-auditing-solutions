### Manual Decompilation – Exercise 9

#### Assembly:

```
procedure0 proc near
000     push 0
004     push procedure1
008     call EnumWindows
000     retn
procedure0 endp
------

procedure1 proc near
    ClassName = byte ptr -204h
    String = byte ptr -104h
    hwnd = dword ptr -4
    V1 = dword ptr 8

000     push ebp
004     mov ebp, esp
004     add esp, -204h
208     push ebx
20C     push esi
210     push edi
214     mov edi, [ebp+V1]
214     push 100h
218     lea eax, [ebp+String]
218     push eax
21C     push edi
220     call GetWindowTextA
214     mov [ebp+eax+String], 0
214     push 100h
218     lea eax, [ebp+ClassName]
218     push eax
21C     push edi
220     call GetClassNameA
214     mov [ebp+eax+ClassName], 0
214     mov esi, 3
214     mov ebx, offset Address1
Label1:
214     lea eax, [ebp+ClassName]
214     call tolower
214     mov edx, [ebx]
214     call Sysutils::StrPos(char *,char *)
214     test eax, eax
214     jnz short Label2
214     lea eax, [ebp+String]
214     call tolower
214     mov edx, [ebx]
214     call Sysutils::StrPos(char *,char *)
214     test eax, eax
214     jz short Label3
Label2:
214     push 0
218     push offset aSyslistview32
21C     push 0
220     push edi
224     call FindWindowExA
214     mov [ebp+hwnd], eax
214     push 0
218     push 0
21C     push 1009h
220     mov eax, [ebp+hwnd]
220     push eax
224     call SendMessageA
214     push 0
218     push 0
21C     push 0Fh
220     mov eax, [ebp+hwnd]
220     push eax
224     call SendMessageA
214     push 0
218     push 0
21C     push 02h
220     push edi
224     call SendMessageA
214     push 0
218     push 0
21C     push 10h
220     push edi
224     call SendMessageA
Label3:
214     add ebx, 4
214     dec esi
214     jnz short Label1
214     mov al, 1
214     pop edi
210     pop esi
20C     pop ebx
208     mov esp, ebp
004     pop ebp
000     retn 8
procedure1 endp

aSyslistview32 db 'SysListView32'
Address1:
    dd offset aRegmon ; "REGMON"
    dd offset aFilemon ; "FILEMON"
    dd offset aRegmonex ; "REGMONEX"
```

#### C code:

```
#define MaxCount 0x100

char *Address1[] = {"REGMON", "FILEMON", "REGMONEX"};
char aSyslistview32[] =  "SysListView32";

BOOL procedure0 () {
    // Enumerates all top-level windows on the screen by passing the handle to each window,
    // in turn, to an application-defined callback function.
    return EnumWindows(procedure1, NULL);
}

BOOL CALLBACK procedure1(HWND V1, LPARAM lparam) {
    char String[256];
    char ClassName[256];
    HWND hwnd;

    // Copies the text of the specified window's title bar (if it has one) into a buffer.
    GetWindowTextA(V1, String, MaxCount);
    
    // Retrieves the name of the class to which the specified window belongs.
    int Len = GetClassNameA(V1, ClassName, MaxCount);

    ClassName[Len] = '\0';

    int i = 3;
    do {
        // Returns a pointer to the first occurrence of STR2 in STR1.
        if ((Sysutils::StrPos(tolower(ClassName), Address1[i]) == 0)  ||
            (Sysutils::StrPos(tolower(String),  Address1[i]) == 0)) {
                i--;
        }
        
        else {

            // Retrieves a handle to a window whose class name and window name match the specified strings.
            hwnd = FindWindowExA(V1, NULL, aSyslistview32, NULL)

            SendMessageA(hwnd, LVM_DELETEALLITEMS, NULL, NULL);
            SendMessageA(hwnd, WM_PAINT, NULL, NULL);
            SendMessageA(V1, WM_DESTROY, NULL, NULL);
            SendMessageA(V1, WM_CLOSE, NULL, NULL);

            i--;
        }
 
    } while (i > 0) ;

    return 1;
}
```