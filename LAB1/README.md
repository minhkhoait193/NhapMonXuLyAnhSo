from PIL import Image
import numpy as np

import imageio.v2 as iio
import matplotlib.pylab as plt

 import các thư viện
 vd 2.1
 đọc ảnh 
 và xuất ảnh ra
![image](https://github.com/user-attachments/assets/3b4cd8d1-b18c-4ec4-9a11-eae43139b2e3)



 vd2.2
 đọc ảnh và chuyển chế độ đọc ảnh là ảnh xám
![image](https://github.com/user-attachments/assets/4dbf22e6-7d4f-49b1-94b4-f79fc0ba8bf1)



 vd2.3
Đọc ảnh 'bird.png' ở dạng số thực (float32) rồi ép kiểu về uint8 để xử lý bit.
(cl = data & 0xF0) Giữ lại 4 bit cao (11110000) của mỗi pixel, các bit thấp bị xóa (set về 0).
 lưu ảnh thành file mới và hiện thị hình ảnh
![image](https://github.com/user-attachments/assets/52046c90-97d1-4a35-b1d8-e23f5cc2a4f3)




 vd 2.4

Lấy kênh G (green): data[:, :, 1] và kênh B (blue): data[:, :, 2]
![image](https://github.com/user-attachments/assets/bb6ff1ed-7b59-4813-8167-c76ab9d79b2b)



 vd 2.5

 Dùng để chuyển đổi hệ màu RGB ↔ HSV và ngược lại
![image](https://github.com/user-attachments/assets/ad2cb8d3-fda0-4071-bce6-b60e15fa9340)

 vd 2.6


h, s, v = rgb2hsv(rgb[:, :, 0], rgb[:, :, 1], rgb[:, :, 2])
Chuyển HSV trở lại RGB.

![image](https://github.com/user-attachments/assets/257dcf1f-030f-46c0-8757-c568391b879f)


 vd 2.7


 Dùng scipy.ndimage để xử lý ảnh bằng hàm convolve.
 Tạo kernel 5×5 với tất cả phần tử = 1/25 → trung bình cộng của vùng 5×5.
 Áp dụng convolution giữa ảnh a và kernel k.
 Kết quả là ảnh đã được làm mờ, sau đó ép kiểu uint8 để hiển thị.
  ![image](https://github.com/user-attachments/assets/e02377db-adb8-4129-a419-268d9c1ada30)




 vd 2.8
a = iio.imread('bird.png', mode='F').astype(np.uint8)
Ép kiểu thành uint8 để dễ xử lý với hàm lọc
b = sn.median_filter(a, size=5, mode='reflect')
Áp dụng bộ lọc trung vị với kích thước 5x5.
mode='reflect': phần biên của ảnh sẽ được phản chiếu ra ngoài để tránh bị lỗi biên khi lọc.
![image](https://github.com/user-attachments/assets/744fa69e-671d-4b69-9193-ef947ba4c8ec)

 vd 2.9



Áp dụng bộ lọc cực đại (maximum filter) với vùng lân cận kích thước 5x5.
![image](https://github.com/user-attachments/assets/a7ef75c4-220a-470d-b182-97e59ca56a2a)




 vd 2.10
Áp dụng minimum filter với vùng 5×5 quanh mỗi điểm ảnh.



![image](https://github.com/user-attachments/assets/4591123f-4052-469f-8d58-9d1ff60d8389)




 vd 2.11
 Áp dụng Sobel filter từ thư viện skimage.filters.

![image](https://github.com/user-attachments/assets/fce184d7-90e0-410c-b62a-d82d150212b8)

vd 2.12
Áp dụng Prewitt filter từ skimage.filters.

Bộ lọc này giúp phát hiện biên bằng cách tính độ chênh lệch cường độ sáng giữa các pixel lân cận.
![image](https://github.com/user-attachments/assets/845f507b-0318-490e-8929-cc75dcad7fb9)


vd 2.13
Áp dụng Canny edge detector:

sigma=3: độ mờ (Gaussian blur) trước khi phát hiện biên.

Giá trị lớn → làm mịn nhiều hơn, giảm nhiễu nhưng mất chi tiết nhỏ.

Kết quả là ảnh nhị phân: viền trắng (1), nền đen (0).

Được ép kiểu uint8 để hiển thị dễ dàng.
![image](https://github.com/user-attachments/assets/3d35bd0f-f934-4898-9f8e-ad88536ea07c)

vd 2.14
Áp dụng Laplace filter từ scipy.ndimage.

Bộ lọc này dựa trên đạo hàm bậc 2 → dùng để phát hiện vùng có thay đổi độ sáng đột ngột.

mode='reflect': phản chiếu biên ảnh để tránh lỗi ở viền.

Kết quả ép kiểu uint8 để hiển thị, nhưng có thể bị mất chi tiết nếu giá trị nhỏ hoặc âm.
![image](https://github.com/user-attachments/assets/802a8129-cc9e-4c2f-83d5-f61f1ea2e528)


vd 2.15


