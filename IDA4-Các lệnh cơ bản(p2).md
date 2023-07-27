# Các lệnh cơ bản(p2)
## XCHG
XCHG A,B; Hoán đổi giá trị của A với giá trị của B. 
A và B có thể là hai thanh ghi, thanh ghi và ô nhớ, nhưng không được phép đồng thời là 2 ô nhớ.

giả sử nếu EAX có giá trị 0x12345678 và ESI có giá trị 0x55, 
khi ta thực hiện lệnh XCHG thì thanh ghi EAX sẽ được gán giá trị 0x55 và thanh ghi ESI là 0x12345678.
Như vậy, sau khi thực hiện lệnh XCHG thì giá trị của hai thanh ghi được hoán đổi cho nhau.

Lệnh XCHG cũng có thể được sử dụng để hoán đổi giữa giá trị thanh ghi với nội dung bộ nhớ được trỏ bởi thanh ghi:
![image](https://github.com/Ash-Dust/assembly/assets/120457430/9a56248e-3897-4bce-9a2a-cd6fe85cd63d)

Trong ví dụ trên, [ESI] có nghĩa là tìm kiếm nội dung tại vị trí trong bộ nhớ được trỏ bởi giá trị của thanh ghi ESI và hoán đổi cho
giá trị của EAX. 
giá trị của thanh ghi EAX sẽ được lưu vào vị trí bộ nhớ mà thanh ghi ESI trỏ tới nếu như vùng nhớ đó có quyền ghi.

Giả sử, nếu EAX có giá trị 0x55 và ESI có giá trị 0x10000. 
Lệnh XCHG lúc này sẽ kiểm tra hiện đang có gì lưu tại vị trí bộ nhớ 0x10000 và vùng nhớ này có thể ghi được không,
nó sẽ lưu giá trị 0x55 ở đó và sẽ đọc giá trị mà nó đã có và lưu vào thanh ghi EAX.

`Điều gì xảy ra nếu chúng ta thực hiện tương tự, 
nhưng thay vì sử dụng thanh ghi, chúng ta sử dụng một địa chỉ bộ nhớ là một giá trị số cụ thể 
như chúng ta đã thực hiện với lệnh MOV ở phần trước?                                 
Kiểu tại sao phải sử dụng XCHG mà k sử dụng MOV í??
`

![image](https://github.com/Ash-Dust/assembly/assets/120457430/ccce4c4a-6cfb-4a93-be4b-5a7209e5e939)

ủa là sao ?? sao hong trả lời mà cài Key patch??? =)))
chỗ này hk hỉu lắm nha, mà hình như KeyPactch dùng để chỉnh sửa lệnh, để sau này dùng

PÁNH ĐỌC GIẢI THÍCH GIÙM TEO =))
#_**Important???**_

## Stack
Là kiểu 1 stack í, vào trước ra sau =)))
Stack cho phép lưu trữ và khôi phục lại dữ liệu. Đối với việc xử lý dữ liệu trên stack


•Có hai thao tác lệnh cơ bản: 

    PUSH, đẩy/lưu một phần tử vào đỉnh ngăn xếp và thao tác ngược lại của nó.
    POP, loại bỏ/khôi phục một phần từ được đẩy vào cuối cùng ra khỏi ngăn xếp.
Tại mỗi thời điểm, ta chỉ có quyền truy cập tới đỉnh của stack(phần tử được đẩy vào cuối cùng).

### PUSH
![image](https://github.com/Ash-Dust/assembly/assets/120457430/e9c52b04-7afc-44f3-96bd-801220a39e79)

Thông thường, trong kiến trúc 32 bit, lệnh PUSH thường được sử dụng để 
`truyền các tham số của một hàm vào ngăn xếp` trước khi thực hiện lời gọi hàm bằng một lệnh CALL.

### POP
![image](https://github.com/Ash-Dust/assembly/assets/120457430/f3051c1e-641f-4e21-91af-e4977f98a7f7)

POP EDI; => đọc giá trị đầu tiên của ngăn xếp và lưu giá trị đó vào EDI;

![image](https://github.com/Ash-Dust/assembly/assets/120457430/45cecf1d-44be-4445-a318-d589ee83969b)

Tóm cái váy lại stack vào pop ra; =)) hết phim
