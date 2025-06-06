1.1
------
![image](https://github.com/user-attachments/assets/557e572c-036c-4fc1-a6b9-d170e5302670)
Mở ảnh grayscale 'world_cup.jpg'

Đảo ngược màu (inversion: trắng thành đen, đen thành trắng)

Hiển thị cả ảnh gốc (img.show()) và ảnh đã xử lý (plt.imshow())


1.2
------
![image](https://github.com/user-attachments/assets/3b71b060-3900-4276-ac6a-4ef2c49add1c)

Đây là gamma correction với gamma = 0.5:
Chuyển ảnh grayscale sang array
Chuẩn hoá ảnh (giá trị pixel từ 0–255 → 0–1)
Chuyển về kiểu int và tạo ảnh mới
Hiển thị ảnh gốc và ảnh sau khi xử lý

sau khi chuyển gamma = 5 
![image](https://github.com/user-attachments/assets/b903e9e9-c965-4933-90a5-6df3f4fa1e14)
Ảnh đầu ra sẽ rất tối, gần như đen, chỉ các vùng rất sáng mới hiện một chút.


1.3
------
![image](https://github.com/user-attachments/assets/99eae6ef-7855-4535-a96f-017dcbef6135)
np.log(1 + b1): áp dụng phép biến đổi logarit cho từng điểm ảnh (tránh log(0))

Chuẩn hóa kết quả bằng cách chia cho log(1 + b2) (với b2 là giá trị pixel lớn nhất)

Nhân 128.0 để giữ ảnh ở độ tương phản trung bình (có thể thay đổi thành 255.0 nếu muốn full scale)

Kết quả: ảnh sẽ có độ tương phản cao hơn ở vùng tối → giúp làm sáng những vùng tối.
1.4
np.histogram tạo histogram ảnh
cdf = hist.cumsum() tính hàm phân phối tích lũy
cdf_m chuẩn hóa CDF về [0–255]
Gán lại giá trị pixel theo CDF để cân bằng độ tương phản
Dùng reshape để trả về ảnh 2D
Ảnh đầu ra (im4) sẽ có độ tương phản cao hơn và trải đều hơn các mức sáng từ đen → trắng
Hiệu quả đặc biệt rõ nếu ảnh gốc có vùng tối hoặc vùng sáng bị lấn át
![image](https://github.com/user-attachments/assets/04baacb3-4753-4a45-a7c6-b87224079415)

1.5
| Bước                             | Mục tiêu                                             |
| -------------------------------- | ---------------------------------------------------- |
| `a = im1.min()`, `b = im1.max()` | Lấy giá trị pixel nhỏ nhất và lớn nhất               |
| `c = im1.astype(float)`          | Chuyển sang `float` để tính toán tránh lỗi           |
| `im2 = 255 * (c - a) / (b - a)`  | Công thức kéo dãn độ tương phản vào khoảng \[0, 255] |
| `im2.astype(np.uint8)`           | Chuyển lại về `uint8` để hiển thị ảnh                |

![image](https://github.com/user-attachments/assets/c0ee8e18-36c1-4ee3-97e6-22940614da99)
Ảnh sẽ có độ tương phản cao hơn, vùng tối và sáng rõ ràng hơn — đặc biệt hiệu quả khi ảnh ban đầu bị "mờ xám" hoặc có dải sáng hẹp.
1.6.1
![image](https://github.com/user-attachments/assets/e0b4f3fb-42ee-4af8-9747-affcd752c27d)
| Phần                | Vai trò                                 |
| ------------------- | --------------------------------------- |
| `fft2(im1)`         | Biến đổi Fourier 2D                     |
| `abs()`             | Lấy biên độ tần số                      |
| `fftshift()`        | Dịch tần số thấp về giữa                |
| `log(1 + x)`        | Giảm độ chênh lệch biên độ              |
| `normalize → 0–255` | Đảm bảo hiển thị ảnh được               |
| `astype(np.uint8)`  | Chuyển về kiểu ảnh grayscale tiêu chuẩn |

1.6.2
--- Butterworth lowpass filter
| Phần                  | Vai trò                                |
| --------------------- | -------------------------------------- |
| `fft2`                | Biến đổi Fourier 2D                    |
| `fftshift`            | Di chuyển tần số thấp về giữa          |
| `H[i, j]`             | Hàm lọc Butterworth (dạng low-pass)    |
| `ifft2`               | Biến đổi ngược về không gian ảnh       |
| `abs`                 | Lấy biên độ phổ sau khi biến đổi ngược |
| `normalize` + `uint8` | Đưa về đúng định dạng ảnh grayscale    |
Ảnh đầu ra (im3) sẽ được làm mịn (blur) vì tần số cao bị loại bỏ

Tăng d_0 → làm mịn ít hơn

Giảm d_0 → làm mịn mạnh hơn

Tăng tl (order) → làm lọc gắt hơn (steeper cutoff)
![image](https://github.com/user-attachments/assets/e3318494-8381-4017-8dca-c307b2f42658)


--- butterworth highpass filter
fft2() & ifft2()	Biến đổi và đảo ngược Fourier
H[i, j] = ...	Công thức Butterworth lọc thấp
d_0	Cắt tần số cao hơn bán kính này
tl	Bậc lọc: càng cao thì biên lọc càng sắc
H * F(u,v)	Nhân trong miền tần số tương đương tích chập trong không gian ảnh
Giảm nhiễu tần số cao
Ảnh được làm mịn nhẹ
Các chi tiết nhỏ bị mờ dần đi
![image](https://github.com/user-attachments/assets/2292fa38-4353-4a7b-8cc7-4a228e779c44)
