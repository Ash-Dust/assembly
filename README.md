# assembly
khong biet j het :D


     bài 1 
                `
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
                `
      bài 2

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

     bài 3
          
