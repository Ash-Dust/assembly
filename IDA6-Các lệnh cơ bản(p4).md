# Các lệnh cơ bản (p4)
## ADD
ADD A, B ; A = A + B
Tất nhiên ta cũng có thể sử dụng các thanh ghi 16-bit và 8-bit. Ví dụ:
ADD AL, 8
ADD AX, 8
ADD BX, AX
ADD byte ptr ds: [EAX], 7 //Lệnh này cộng vào byte nội dung mà EAX trỏ đến với giá trị hằng số là 7 và lưu lại tại cùng một vị trí.

## SUB
SUB A, B ; A = A – B

## INC và DEC
INC A; A++
DEC A; A–
Thường được sử dụng trong lặp

## IMUL
Đây là lệnh thực hiện phép tính nhân số có dấu và có hai dạng như sau:
IMUL A, B    ; A = A * B
IMUL A, B, C ; A = B * C

## DIV/ IDIV
DIV/ IDIV A

A được hiểu là số chia. Số bị chia và thương số không được chỉ định bởi vì chúng luôn giống nhau. có 3 dạng như sau:

Nếu A có kiểu byte, lấy giá trị của thanh ghi AX chia cho A, kết quả thương số lưu vào thanh ghi AL, phần dư lưu vào thanh ghi AH.

Nếu A có kiểu word, lấy giá trị của cặp thanh ghi DX:AX chia cho A, kết quả thương số lưu vào thanh ghi AX, phần dư lưu vào thanh ghi DX.

Nếu A có kiểu dword, lấy giá trị của cặp thanh ghi EDX:EAX chia cho A, kết quả thương số lưu vào thanh ghi EAX, phần dư lưu vào thanh ghi EDX.

VD:

![image](https://github.com/Ash-Dust/assembly/assets/120457430/1a9fabf8-1304-495a-a5c3-aaa9bf421b3f)

nếu EAX = 5, EDX = 0 và ECX = 2, nó sẽ thực hiện phép chia số nguyên. 
Kết quả của phép chia 5 / 2 sẽ được 2 và dư 1. Khi đó kết quả là 2 được lưu vào thanh ghi EAX và số dư 1 sẽ được lưu vào thanh ghi EDX.

EDX sẽ ghi phần dư

EAX ghi kết quả

Khi thực hiện phép chia, do thanh ghi EDX được sử dụng để lưu phần dư nên nó sẽ được thiết lập về 0 trước khi thực hiện phép tính.

Để xóa EDX về 0 có hai cách:
    • Sử dụng câu lệnh XOR (chi tiết bên dưới): XOR EDX, EDX  
    • Sử dụng câu lệnh CDQ (như trên hình minh họa): 
    Câu lệnh này thực hiện mở rộng bit dấu (bit 31) của thanh ghi EAX sang thanh ghi EDX. 
    Nếu bit này có giá trị 0 thì EDX sẽ bằng 0.

## Các lệnh logic

### AND, OR và XOR
AND A, B ; A = A & B

OR A, B  ; A = A | B

XOR A, B ; A = A ^ B

![image](https://github.com/Ash-Dust/assembly/assets/120457430/0b476cf5-a99f-470b-9db5-da3cba1169af)

Lệnh hay được sử dụng nhiều nhất là XOR cùng một thanh ghi để dễ dàng xóa thanh ghi đó về 0.
bằng cách này sẽ thực hiện nhanh hơn lệnh MOV.

![image](https://github.com/Ash-Dust/assembly/assets/120457430/4dd2d600-c92b-435b-8f12-fcae64dbe152)

Để kiểm tra ta có thể viết một lệnh xor hai số giống nhau ở dạng binary trong khung Python. Kết quả trả về luôn là 0:
![image](https://github.com/Ash-Dust/assembly/assets/120457430/4d03485f-05e2-4d40-9b44-af7b5306eb20)
có thể áp dụng với số thập phân và thập lục phân

### NOT 
NOT A; đảo ngược tất cả các bit của A và lưu lại kết quả vào A

### NEG
NEG A ; chuyển đổi A thành –A

### Các lệnh dịch bit SHL, SHR
SHL A, B; Dịch trái A đi B bit
SHR A, B; Dịch phải A đi B bit





      
