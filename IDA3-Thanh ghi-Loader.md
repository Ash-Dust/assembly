## Mở đầu (Loader)
Khi bỏ file vào IDA sẽ có một phân tích tĩnh (Loader) để phân tích file.
Ở chế độ Loader này, chương trình sẽ không được thực thi, nhưng nó được IDA phân tích và sau cùng sẽ tạo ra một file .idb
– là cơ sở dữ liệu lưu các thông tin trong quá trình phân tích, bao gồm đổi tên biến, tên hàm, các chú thích…. 
Trên thực tế, file .idb sẽ là tổng hợp của 5 files(.id0, .id1, .nam, .id2, and .til) được sinh ra trong quá trình phân tích:

![image](https://github.com/Ash-Dust/assembly/assets/120457430/462dead0-f0b7-4949-990e-91d003aec845)

Ở chế độ Loader, chúng ta có thể `phân tích` `bất kỳ hàm nào của chương trình`, tuy nhiên không phải lúc nào chúng ta cũng có thể truy xuất
vào hàm mà ta cần tìm hiểu, lúc đó ta phải học cách để debug. Tất nhiên, để tìm hiểu cách phân tích các hàm, chúng ta cần phải 
`trang bị kiến thức cơ bản về các thanh ghi và các câu lệnh asm cơ bản`. 
`Bởi vì` mặc dù không debug, không có cửa sổ thanh ghi với các giá trị tại từng thời điểm, các câu lệnh sử dụng chúng 
thì `dựa vào các kiến thức cơ bản này`, `ta có thể hiểu mục đích của hàm hoặc chương trình làm gì`.
### Các thanh ghi và mục đích sử dụng của chúng
Thanh ghi giúp bộ xử lý lưu trữ các giá trị
được xem như các vùng lưu trữ nhỏ được tích hợp sẵn trong bộ xử lý (volatile memory – chỉ giữ được dữ liệu khi máy tính còn hoạt động)
`Khi CPU thực thi một lệnh`, `nó phải lấy lệnh từ bộ nhớ`, `giải mã lệnh`, và sau đó `thực hiện hành động` tương ứng với mục đích của lệnh. 
`Các hành động mà CPU thực hiện` `có thể` `thao tác thông tin trong các thanh ghi hoặc trong bộ nhớ`
Chúng ta có 8 thanh ghi dùng chung, gồm:

 _ EAX (thanh ghi chứa – accumulator)_: được sử dụng nhiều nhất trong các lệnh `số học, logic, và chuyển dữ liệu`. 
  Các `thao tác nhân, chia` sử dụng thanh ghi này. Với các `hàm API của Windows`,kết quả trả về của hàm `thường sẽ lưu vào EAX`.
  
  _EBX (thanh ghi cơ sở – base):_ thanh ghi EBX thường được dùng để định` địa chỉ`, `đặc biệt ` là khi làm việc với `mảng`.
  Thanh ghi này `cũng được dùng như một thanh ghi dữ liệu` `khi không được sử dụng để định địa chỉ`.
  
  _ECX (thanh ghi đếm – count):_ ECX là một thanh ghi dùng chung có thể được sử dụng như là một `bộ đếm cho các lệnh khác nhau`.
  Nó cũng `có thể chứa địa chỉ lệch của dữ liệu trong bộ nhớ`. 
  `Các lệnh sử dụng bộ đếm là các lệnh liên quan lặp chuỗi, các lệnh chuyển, xoay và LOOP / LOOPD.`
  
  _EDX (thanh ghi dữ liệu – data):_ là một thanh ghi dùng chung dùng để chứa `một phần kết quả của phép nhân hoặc một phần của phép chia`. 
  Nó cũng `có thể truy cập địa chỉ dữ liệu trong bộ nhớ trực tiếp`.
  
  _EDI (chỉ số đích – destination):_ EDI thường được sử dụng trong các thao tác làm việc với `chuỗi hoặc mảng`. 
  Thanh ghi này sẽ trỏ tới chuỗi đích. Bên cạnh đó nó cũng là một _`thanh ghi dùng chung`_.
  
  _ESI (chỉ số nguồn – source):_ Giống như EDI,
  ESI cũng thường được sử dụng trong các thao tác làm việc với `chuỗi hoặc mảng`. 
  Thanh ghi này sẽ trỏ tới chuỗi nguồn.
  
  _EBP (con trỏ cơ sở – base):_ EBP trỏ tới vị trí bộ nhớ,
  bên cạnh `mục đích dùng chung` thì nó được sử dụng làm frame pointer`
  để truy xuất các tham số và các biến cục bộ` trong `ngăn xếp của một hàm`.
  
  _ESP (con trỏ ngăn xếp – stack):_ thanh ghi này luôn trỏ đến `đỉnh hiện thời của Stack`. 
  Theo nguyên tắc làm việc của Stack thì thanh ghi này `sẽ hướng về phía địa chỉ thấp hơn`.



Như vậy, có tổng cộng 8 thanh ghi 32 bit dùng chung là `EAX`, `EBX`, `ECX`, `EDX`, `ESP`, `EBP`, `ESI` và `EDI`. 
Ngoài ra, các thanh ghi này còn có thể chia nhỏ thành các thanh ghi 16-bit và 8-bit như hình dưới đây:
![image](https://github.com/Ash-Dust/assembly/assets/120457430/7bd4c11c-579c-4b6c-bb2d-6742adfd6c6b)

Ví dụ, nếu thanh ghi EAX có giá trị là 0x12345678 thì AX là thanh ghi 16 bit chứa bốn chữ số cuối cùng:
![image](https://github.com/Ash-Dust/assembly/assets/120457430/721e2994-7862-48ea-9b93-c1732df72cc6)

Thanh ghi AX có thể được tách thành 2 thanh ghi 8 bit, đó là cặp thanh ghi: 
   AH chứa hai số 5 và 6 
và AL chứa hai số cuối cùng là 7 và 8:

![image](https://github.com/Ash-Dust/assembly/assets/120457430/c22d1b84-cbe5-46fb-90f9-dc17a5034e05)

=> các thanh ghi 32 bit được chia nhỏ thành các thanh ghi khác vd EAX (32bit) được chia nhỏ thành AX (16bit),
và AX (16bit) lại được chia nhỏ thành AH (8bit) và AL (8bit)
có 4 thanh ghi được chia như thế này EAX (AX, AH và AL), EBX (BX, BH và BL), ECX (CX, CH và CL) và EDX (DX, DH và DL)
Các thanh ghi còn lại chỉ được tách thành một thanh ghi 16 bit, không chia nhỏ thêm thành các thanh ghi 8 bit:

![image](https://github.com/Ash-Dust/assembly/assets/120457430/c5b6145e-6a2a-407f-a5e8-be00631faf19)
 ### Các thanh ghi đặc biệt
 Bên cạnh các thanh ghi dùng chung ở trên, các bạn sẽ gặp các thanh ghi đặc biệt khác nữa, bao gồm:

EIP (con trỏ lệnh – instruction): đây `là một thanh ghi đặc biệt`, nó `luôn trỏ đến lệnh tiếp theo sẽ được thực hiện`. 
Khác với các thanh ghi khác, `EIP không thể bị tác động trực tiếp bởi các lệnh`.

  Bên lề: Zero Flag (ZF) là cờ phổ biến nhất được sử dụng trong reversing. 
  Chủ yếu được sử dụng trong các lệnh rẽ nhánh có điều kiện, làm thay đổi luồng thực thi dựa trên các kết quả lệnh trước đó.

  Tiếp theo là các thanh ghi đoạn, các thanh ghi này trỏ tới các phần khác nhau của file thực thi như CS = CODE, DS = DATA v..v…
  ![image](https://github.com/Ash-Dust/assembly/assets/120457430/a58299ea-5527-4604-af7d-ba2c26a2dc62)

kích thước của các kiểu dữ liệu thường được sử dụng nhiều nhất:
![image](https://github.com/Ash-Dust/assembly/assets/120457430/f4a38ca2-07d1-4156-919c-4441ad9e788f)






