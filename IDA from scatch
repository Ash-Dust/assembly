# P2
```
## Hệ thống số ###
   

    Bin : ob__, bin(__)
    Dec
    Hex: 0x__,
    Số âm -> bit  đầu tiên 
    0 =>> số dương
    1 =>> số âm
          
    giá trị âm lớn nhất là -1 tương ứng với 0xFFFFFFFF
    giá trị âm bé nhất là 0x80000000
    
    + Trường hợp không quan tâm đến dấu, thì tất cả các giá trị sẽ là số dương nằm trong khoảng từ 0 đến 0xFFFFFFFF
    + Trường hợp xem xét đến sử dụng bit dấu, chúng ta sẽ có các số dương  nằm trong khoảng từ  0x0  đến 0x7FFFFFFF 
    và các số âm nằm trong khoảng từ 0xFFFFFFFF đến 0x80000000.
    
    #Số dương
    00000000 bằng 0
    00000001 bằng 1
    ...
    7FFFFFFF bằng 2147483647 thập phân (sẽ là số dương lớn nhất)
    
    #Số âm
    FFFFFFFF bằng -1
    FFFFFFFE bằng -2
    ...
    80000001 bằng -2147483647 
    80000000 bằng -2147483648 (sẽ là số âm nhỏ nhất)
    
    Nói tóm gọn lại trong IDA khi xét có số âm 
    bit đầu tiên từ 0 - 7 =>> số dương
    bit đầu tiên từ F - 8 =>> số âm
    
    dễ hiểu hơn là từ 00000000 -> 7FFFFFFF sẽ bằng 0           -> 2147483647 
                và từ 80000000 -> FFFFFFFF sẽ bằng 2147483647  -> 4294967295 (tương đương từ -2147483648 -> -1)      =)) 
                                          ### mịa có mỗi cái này t ngồi cả buổi ms nghiệm ra    từ đó ta có -1 = 4294967295 ảo ma thật sự
         
------------------------------------------------------------------------------------------------------------------------------------------

## Bảng mã ASCII
          Từ (HEX) 30 -> 39: số từ 1-9
              DEC  48 -> 57: số từ 1-9
          
          Từ (HEX) 41 -> 5A: từ A - Z
              DEC  65 -> 90: từ A - Z
          
          
          Từ (HEX) 61 -> 7A: từ a - z
              DEC  97 ->122: từ a - z

Có thể sử dụng hàm chr() để chuyển từ hex sang ASCII
![image](https://user-images.githubusercontent.com/120457430/255154915-fdcf38af-bad4-4e51-bb4e-999dd9100a2f.png)

Ngoài ra có thể dùng Hex View-1
![image](https://github.com/Ash-Dust/upload-picture/assets/120457430/b3a8d12b-d305-4795-8a26-ca6c0727c1b7)

------------------------------------------------------------------------------------------------------------------------------------------
## IDA search
Này vào mục search của IDA thoyy
![image](https://github.com/Ash-Dust/upload-picture/assets/120457430/eeb4d2a8-51e3-49e6-8da9-03b8f6665310)

    # Next code: theo mình hiểu là nó sẽ search cái câu lệnh (code) tiếp theo

    # Next data: như trên nhưng thay câu lệnh(code) = data

    # Next Explored và Next Unexplored: các vùng không được phát hiện là lệnh hoặc dữ liệu hợp lệ  
    ~~///[ ko hiểu lắm, sau này sẽ quay lại]~~

    # Immediate Value – Search Next Immediate Value: Tìm kiếm giá trị chỉ định
          **Find all occurences** : tìm tiếm tất cả 
          nếu muốn tìm lần lượt chọn **Search next immediate value**
    
    # Text – Search Next Text: tìm kiếm chuỗi, bao gồm cả biểu thức.
    Nếu chỉ tìm kiếm một lần, muốn tìm tiếp thì sử dụng Search Next Text.

    # Sequences of bytes: tìm kiếm 
    ![image](https://github.com/Ash-Dust/upload-picture/assets/120457430/28fb4955-dfac-446e-bf6e-b5acc6b61165)

    # Not Function
    Chức năng này cho phép tìm kiếm byte đầu tiên không thuộc về bất kỳ hàm nào. Đôi khi có những hàm mà IDA không thể xác định 
đó là hàm nhưng chúng lại có các lệnh hợp lệ.
    
```
