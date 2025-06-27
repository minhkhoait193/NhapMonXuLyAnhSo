câu 1
---

![image](https://github.com/user-attachments/assets/3940cbd9-7e8b-40de-b01c-3f995bb960fa)

câu 2
---
![image](https://github.com/user-attachments/assets/d9ceb1e4-9917-46bb-b7b7-da1301ade83c)

![image](https://github.com/user-attachments/assets/76f229b6-fc0d-4b2f-938c-88a1e5c041df)

câu 3
---
![image](https://github.com/user-attachments/assets/6bb1442e-d0ad-42fd-bb27-bb3da6e9912f)

câu 4
---
![image](https://github.com/user-attachments/assets/c4559535-2549-419a-92c1-38435ce3980d)

câu 5
---
Hàm tạo hiệu ứng sóng (warp)
  def wave_transform(amplitude):
      def transform(outcoord):
          y, x = outcoord
          shift_x = amplitude * np.sin(y / 30.0)
          return y, x + shift_x
      return transform
Đây là hàm sinh (factory):
Trả về một hàm con transform() để dùng với nd.geometric_transform
Nó làm cho tọa độ x lệch đi theo sóng sin → ảnh bị uốn cong như gợn sóng

Làm mờ Gaussian:
  sigma = float(input(...))
  result = nd.gaussian_filter(img, sigma=sigma)

Biến dạng sóng (warp):
Duyệt từng kênh màu để áp dụng geometric_transform với hàm wave_transform
Nếu ảnh là grayscale thì xử lý trực tiếp

Xoay:
  angle = float(input(...))
  reshape_str = input(...)
  reshape = True if reshape_str == 'y' else False
  result = nd.rotate(img, angle=angle, reshape=reshape)

Tịnh tiến:
  dx = int(input(...))
  dy = int(input(...))
  shift = (dy, dx, 0) if img.ndim == 3 else (dy, dx)
  result = nd.shift(img, shift=shift)
Dịch ảnh theo x và y
Nếu ảnh có 3 kênh (RGB), phải thêm 0 cho kênh màu


![image](https://github.com/user-attachments/assets/4ebbec18-0890-41e1-a249-1116191d131f)
