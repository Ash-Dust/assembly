##Các lệnh chuyển dữ liệu
MOV dest, src: Sao chép nội dung của toán hạng nguồn (src) tới đích (dest)
Giữa các thanh ghi, giữa một thanh ghi và một ô nhớ hoặc chuyển trực tiếp một số vào một thanh ghi hay ô nhớ.
vd: 
  ```
    MOV EAX, EDI; EAX nhận giá trị của EDI; còn EDI giữ nguyên giá trị, không bị thay đổi
    chỉ có thể chuyển trực tiếp dữ liệu từ hoặc đến thanh ghi
    ngoại trừ thanh ghi EIP không thể là Destination hoặc Source của bất kỳ hoạt động nào
        
    MOV EAX, 1; chuyển số 1 vào thanh ghi EAX, giá trị trước đó của thanh ghi EAX bị ghi đè lên (thay bằng giá trị mới)
  ```
![image](https://github.com/Ash-Dust/assembly/assets/120457430/81940a17-33c7-425b-9126-7fc1ecf508c1)
   
mov     eax, offset dword_46F908
Chuyển địa chỉ 0x46F908 vào thanh ghi EAX, tức là EAX = 0x46F908
*offset là tiền t1o6 chỉ địa chỉ của thanh ghi

mov     eax, dword_46F908
Chuyển nội dung hoặc giá trị tại địa chỉ đó vào thanh ghi EAX, tức là EAX = 0x0

Khi hoạt động vs thanh ghi:
![image](https://github.com/Ash-Dust/assembly/assets/120457430/46a76680-bf2e-42a2-9bbb-230f1ea35483)
 dấu ngoặc [] vì rõ ràng bạn không biết giá trị tĩnh mà thanh ghi có thể có được tại thời điểm đó
 và bạn không thể biết hướng nào bạn sẽ trỏ đến để lấy thêm thông tin từ đó (~~là không rõ giá trị, hay là biến j đấy???sẽ tìm hiểu sau~~)
 *tiền tố unk_ : ko biết kiểu dữ liệu là gì

![image](https://github.com/Ash-Dust/assembly/assets/120457430/1da969ce-2f67-4884-b994-dc2af0f65bb8)

cái này set up cái j đó để làm cái j đó =)):
![image](https://github.com/Ash-Dust/assembly/assets/120457430/4ce4e7b7-8aa5-460e-bf29-4f375b3dd9a5)

bonus kiến trúc 64 bit:
Các thanh ghi dùng chung 32 bit (4 byte) eax, ebx, ecx, edx, esi, edi, ebp và esp được mở rộng thành 64 bit (8 byte); 
các thanh ghi này được đặt tên là rax, rbx, rcx, rdx, rsi, rdi, rbp và rsp.
8 thanh ghi mới được bổ sung thêm là r8, r9, r10, r11, r12, r13, r14, và r15.
![image](https://github.com/Ash-Dust/assembly/assets/120457430/ab8d2bff-1400-4190-b724-e768b1d590b5)
Truy cập các thanh ghi r8 – r15 dưới dạng byte, word, dword hoặc qword bằng cách bổ sung thêm b, w, d hoặc q vào sau tên thanh ghi
Trong kiến trúc x86, các tham số của hàm sẽ được đẩy vào ngăn xếp trước khi gọi hàm,
trong khi ở kiến trúc x64, bốn tham số đầu tiên được truyền vào các thanh ghi rcx, rdx, r8 và r9
và nếu chương trình còn các tham số khác nữa, chúng sẽ được lưu vào stack. 

=> Điều này sẽ khiến cho `khó xác định được xem địa chỉ bộ nhớ nào là biến cục bộ hay tham số của hàm`







    
    
    
    
  
