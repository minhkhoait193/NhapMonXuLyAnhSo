câu 1
---
xác định tọa độ của canh chua[82:369, 283:578]
![image](https://github.com/user-attachments/assets/5152f622-cfe8-4f6a-a95b-a70e2900be80)

câu 2
---
| Vector tịnh tiến | Ý nghĩa                          | Hiệu ứng quan sát được                                        |
| ---------------- | -------------------------------- | ------------------------------------------------------------- |
| `(100, 25)`      | Dịch xuống 100px và phải 25px    | Ảnh bị đẩy ra góc dưới-phải, xuất hiện khoảng trống trên/trái |
| `(50, -30)`      | Dịch xuống 50px và **trái 30px** | Ảnh bị đẩy ra dưới-trái, xuất hiện khoảng trống trên/phải     |
Khi thay đổi giá trị âm ở trục x, ảnh dịch về bên trái, dẫn đến một phần ảnh bị mất và xuất hiện vùng đen bên phải.
Tương tự, khi tăng giá trị ở trục y (ví dụ 50), ảnh dịch xuống dưới, và vùng đen xuất hiện ở phía trên.
![image](https://github.com/user-attachments/assets/025dcc42-ed28-4756-8955-284d39885ec4)

câu 3
---
| Phép biến đổi       | Hiệu ứng quan sát được                                        |
| ------------------- | ------------------------------------------------------------- |
| **Phóng to 3 lần**  | Ảnh lớn hơn, chi tiết bị mờ nếu dùng nội suy mặc định         |
| **Thu nhỏ 0.3 lần** | Ảnh nhỏ lại, mất nhiều chi tiết, có thể bị nhòe hoặc răng cưa |
![image](https://github.com/user-attachments/assets/6e93250b-b5e2-41e4-abbc-05d3e9c226d6)

câu 4
---
| Thuộc tính           | `reshape=True`                                  | `reshape=False`                                                                   |
| -------------------- | ----------------------------------------------- | --------------------------------------------------------------------------------- |
|  Kích thước đầu ra  | Tự động **tăng kích thước ảnh** để không bị cắt | **Giữ nguyên** kích thước ban đầu                                                 |
|  Hình dạng ảnh     | Có thể bị rỗng nền (màu đen xung quanh)         | **Bị cắt góc** do không đủ chỗ chứa ảnh đã xoay                                   |
|  Khi nào nên dùng? | Khi bạn muốn **giữ toàn bộ nội dung ảnh**       | Khi muốn ảnh xoay mà vẫn **giữ nguyên kích thước** (dùng cho overlay, mask, v.v.) |
reshape=True → không mất dữ liệu nhưng ảnh to ra, có phần nền đen.
reshape=False → giữ kích thước, nhưng mất một phần ảnh do bị cắt.
![image](https://github.com/user-attachments/assets/3068004b-da33-41b7-b2be-407526dd4174)

câu 5.1 Dilation và Erosion
---
| Phép biến đổi    | Mô tả hiệu ứng                                                                   |
| ---------------- | -------------------------------------------------------------------------------- |
| **Dilation**     | Làm **dày** thêm vùng sáng, lấp lỗ đen nhỏ                                       |
| **Erosion**      | Làm **mỏng** vùng sáng, xóa chi tiết nhỏ hoặc nhiễu trắng                        |
| **Kernel (5x5)** | Ảnh hưởng **mạnh hơn** so với (3x3): làm mờ, mài mòn hoặc lan rộng vùng mạnh hơn |

![image](https://github.com/user-attachments/assets/4e2881d0-b3f9-46a2-bc42-9d72f3d1d94f)

câu 5.2 thay đổi hàm GeoFun cos = sin
---
| Biến thể hàm GeoFun | Hiệu ứng quan sát được                                                    |
| ------------------- | ------------------------------------------------------------------------- |
| `cos` (gốc)         | Hình ảnh bị biến dạng dạng sóng đều, co giãn theo trục x và y             |
| `sin`               | Tương tự `cos` nhưng tạo hiệu ứng uốn lượn mềm hơn                        |
| Radial (sóng tròn)  | Làm ảnh bị bóp méo theo hướng tâm, thường dùng để làm hiệu ứng nghệ thuật |
![image](https://github.com/user-attachments/assets/d3a55f0d-33fb-4698-956e-d3f18993ca9a)

