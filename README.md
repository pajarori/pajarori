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
    languages resb 7 * 20  ; Reserve space for 7 language strings of up to 20 characters each

section .text
global _start

_start:
    ; Initialize registers
    mov eax, 4           ; Syscall number for sys_write
    mov ebx, 1           ; File descriptor 1 (stdout)
    
    ; Print "Hi, I'm nopebee7. Contact me at satyriha"
    mov edx, username
    mov ecx, edx
    mov edx, discord
    call print_string

    ; Exit the program
    mov eax, 1           ; Syscall number for sys_exit
    xor ebx, ebx         ; Return code 0
    int 0x80

print_string:
    ; Input: ECX = pointer to the null-terminated string to print
    ; Output: None
    ; Clobbers: EAX, EBX, EDX

    next_char:
        ; Load the next character into AL and check if it's null (end of string)
        lodsb
        cmp al, 0
        je done

        ; Print the character to stdout
        int 0x80

        ; Repeat for the next character
        jmp next_char

    done:
        ret
```
