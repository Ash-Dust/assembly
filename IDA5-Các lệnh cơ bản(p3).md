# Các lệnh cơ bản (p3)

## LEA (LOAD EFFECTIVE ADDRESS)
LEA A, B
Lệnh LEA (nạp địa chỉ hiệu dung vào thanh ghi) thực hiện chuyển một địa chỉ được chỉ định trong B (nguồn) vào A (đích). 
Nội dung của B không bao giờ được truy cập, nó sẽ luôn là một địa chỉ hoặc 
là kết quả của phép tính toán nằm trong dấu ngoặc vuông [] của toán hạng thứ hai. 
Lệnh LEA được sử dụng rất nhiều để lấy địa chỉ bộ nhớ của các biến hoặc các tham số.
VD:

![image](https://github.com/Ash-Dust/assembly/assets/120457430/db642c91-45b6-4e40-b207-6395de1b2e90)
chương trình sử dụng một lệnh LEA tại địa chỉ 0x401191 
lea     eax, [ebp+var_C], câu lệnh này sẽ thực hiện lấy địa chỉ của biến trên Stack và gán vào thanh ghi EAX. 
Nếu ngược lại, đây là một câu lệnh MOV thì sẽ chuyển nội dung hoặc giá trị đang được lưu giữ trong biến vào EAX.
=> MOV offset giống LEA??

lệnh LEA cũng được sử dụng để thực hiện `các tính toán nằm trong []`, 
sau đó chuyển kết quả tính toán vào thanh ghi đích, mà `không cần truy cập nội dung`.
Xem xét các ví dụ:

LEA EAX, [4+5]

Lệnh trên sẽ tính toán và gán 9 vào thanh ghi EAX, 
nó sẽ không chuyển nội dung của địa chỉ 0x9 như lệnh MOV sẽ thực hiện: MOV EAX, [4+5]

Lệnh LEA thực hiện lấy địa chỉ biến. Tương ứng mã giả là a = &b
Lệnh MOV thực hiện lấy giá trị được lưu tại địa chỉ biến. Tương ứng với mã giả là a = *b

Một ứng dụng khác của lệnh LEA là các phép toán kết hợp giữa các thanh ghi và các hằng số, 
kết quả tính được gán cho toán hạng đầu tiên có thể một số hoặc một địa chỉ phụ thuộc vào giá trị của các thanh ghi:
![image](https://github.com/Ash-Dust/assembly/assets/120457430/a9e01f7d-730a-407d-9303-dd9c7b018687)

Trong hình trên, tại thời điểm thực hiện tính toán, giả sử nếu ESI có giá trị 400000 và EAX bằng 2, 
thì giá trị của thanh ghi EDX sẽ là kết quả tính toán của biểu thức 0x400000 + 2*4+0x14:

![image](https://github.com/Ash-Dust/assembly/assets/120457430/02e13089-56c0-4c24-baf7-34c836a07c84)

nó sẽ gán giá trị 0x40001c vào thanh ghi EDX.




