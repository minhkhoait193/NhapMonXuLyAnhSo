1.1
![image](https://github.com/user-attachments/assets/557e572c-036c-4fc1-a6b9-d170e5302670)
Mở ảnh grayscale 'world_cup.jpg'

Đảo ngược màu (inversion: trắng thành đen, đen thành trắng)

Hiển thị cả ảnh gốc (img.show()) và ảnh đã xử lý (plt.imshow())
1.2
![image](https://github.com/user-attachments/assets/c4fd692e-5495-48dc-bdbe-8d4f4541c3b7)

Đây là gamma correction với gamma = 0.5:

Chuyển ảnh grayscale sang array

Chuẩn hoá ảnh (giá trị pixel từ 0–255 → 0–1)
Chuyển về kiểu int và tạo ảnh mới

Hiển thị ảnh gốc và ảnh sau khi xử lý
1.3
1.4
1.5
1.6.1
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
