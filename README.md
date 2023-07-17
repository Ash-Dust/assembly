# assembly


bài 1 
```                
org 100h

.data
    message db 10,13, "nhap chuoi: $"   
    message2 db 10,13, "chuoi da nhap la $"
    chuoi db 100 dup("$");



.code
    ; co data thi ghi
    mov ax, @data
    mov ds, ax
    
    ; in tin nhan
    
    mov ah, 09h
    lea dx, [message]
    int 21h

    ; Read chuoi
    mov ah, 0Ah
    lea dx, [chuoi]
    int 21h

    ; in ra chuoi
    mov ah, 09h
    lea dx, [message2]
    int 21h
    lea dx, [chuoi+2] ; skip 2 bytes dau (length and '$')
    int 21h

    ; exit
    mov ah, 4Ch
    int 21h

ret
```
                
bài 2
      
```
org 100h

.data
    message db 10,13, "nhap chuoi: $"   
    message2 db 10,13, "chuoi in hoa la $"
    chuoi db 100 dup("$");



.code
    ; co data thi ghi
    mov ax, @data
    mov ds, ax

    ; in tin nhan
    mov ah, 09h
    lea dx, [message]
    int 21h

    ; Read chuoi
    mov ah, 0Ah
    lea dx, [chuoi]
    int 21h   

    ; in ra chuoi
    mov ah, 09h
    lea dx, [message2]
    int 21h
  
    ;lam cho chuoi in hoa    
    call inhoa
    
    ; exit
    mov ah, 4Ch
    int 21h

ret      


inhoa proc
    lea si, chuoi+2 ; skip 256 vs $      ;con tro
    lap2:
        mov dl, [si]       
        cmp dl, 'a'     ;nho hon a thi in
        jl in2
        cmp dl, 'z'     ;lon hon z thi in
        jg in2
        sub dl, 32 ; tru di 32 de chuyen thanh in hoa
    in2:
        mov ah, 2 ;     ;in ra
        int 21h
        inc si
        cmp [si], '$'
        jne lap2
   
inhoa endp
```
bài 3
```
.model small
.stack 100h
.data
        tb1 db 'nhap chuoi: $ ' 
        tb2 db 10,13, 'do dai cua chuoi la: $'
        s db 100, dup('$')
        x dw ?    
.code
main proc
        mov ax, @data
        mov ds, ax
        
        ;nhap chuoi
        mov ah,9
        lea dx,tb1
        int 21h
        
        mov ah,10
        lea dx,s
        int 21h
        
        ;do dai chuoi
        mov ah,9
        lea dx,tb2
        int 21h
        
        mov ax,0
        mov al,s+1 ; chuyen chieu dai chuoi vao al
        mov x,ax ; chuyen ax vao x
        
        call print
        
        mov ah,4
        int 21h
        
main endp

;hien thi
print proc
    mov ax, x
    mov bx, 10
    mov cx, 0
    
    chia:
        mov dx, 0
        div bx
        push dx
        inc cx
        cmp al,0
        je hienthi
        jmp chia
    hienthi:
        pop dx
        add dl,30h
        mov ah,2
        int 21h
        dec cx
        cmp cx,0
        jne hienthi
        ret
print endp

end main
```
bài 4
```
.model small
.stack 100h
.data
    array db 100 dup('$')
        
.code
main proc
        mov ax, @data
        mov ds, ax
        
        mov bl,0
        mov si, offset array
        
        loop:
            mov ah,1
            int 21h
            
            cmp al,13
            je s1
            mov [si], al
            inc si        ; tang gia tri index cua array
            inc bl         ; tang count 
            jmp loop
            
        s1:
            mov cl,bl   
            
        p1:
            dec si            ;giam gia tri index cua array
            mov dx,[si]       ;si = 0 se dung ctrinh
            mov ah,2
            int 21h
            loop p1
            
            mov ah,4ch
            int 21h
        
main endp  



end main
```
          
