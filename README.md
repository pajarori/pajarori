<pre align="center">
███╗   ██╗ ██████╗ ██████╗ ███████╗██████╗ ███████╗███████╗███████╗
████╗  ██║██╔═══██╗██╔══██╗██╔════╝██╔══██╗██╔════╝██╔════╝╚════██║
██╔██╗ ██║██║   ██║██████╔╝█████╗  ██████╔╝█████╗  █████╗      ██╔╝
██║╚██╗██║██║   ██║██╔═══╝ ██╔══╝  ██╔══██╗██╔══╝  ██╔══╝     ██╔╝ 
██║ ╚████║╚██████╔╝██║     ███████╗██████╔╝███████╗███████╗   ██║  
╚═╝  ╚═══╝ ╚═════╝ ╚═╝     ╚══════╝╚═════╝ ╚══════╝╚══════╝   ╚═╝  
</pre> 

```asm
section .data
    username db "nopebee7",0
    location db "Indonesia",0
    discord db "satyriha",0

section .bss
    languages resb 7 * 20

section .text
global _start

_start:
    mov eax, 4 
    mov ebx, 1      
    
    mov edx, username
    mov ecx, edx
    mov edx, discord
    call print_string

    mov eax, 1
    xor ebx, ebx 
    int 0x80

print_string:
    next_char:
        lodsb
        cmp al, 0
        je done
        int 0x80
        jmp next_char
    done:
        ret
```
