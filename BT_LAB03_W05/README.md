CÂU 1
---
shift=(0, 30, 0) = không dịch theo trục y, dịch sang phải 30 pixel, không đổi kênh màu

![image](https://github.com/user-attachments/assets/ad5dda47-e31b-487a-b472-27f353ed4049)

CÂU 2
---
Kết quả: Đu đủ và dưa hấu đã đổi màu (trông giống filter màu lạ) trên ảnh gốc. Đây là cách đơn giản và nhanh để tạo hiệu ứng đặc biệt bằng hoán đổi kênh màu.
![image](https://github.com/user-attachments/assets/f372d383-5a2f-4af2-908f-c5a3485dd5b0)


CÂU 3
---
  rotated_mountain = nd.rotate(mountain, angle=45, reshape=True)
  rotated_boat = nd.rotate(boat, angle=45, reshape=True)
Hàm rotate của ndimage để xoay ảnh.
reshape=True cho phép mở rộng ảnh nếu cần để không bị cắt góc.
![image](https://github.com/user-attachments/assets/9c769a7c-2fcb-41a7-a261-7d29e9bb2f8f)

CÂU 4
---
Dùng slicing img[y1:y2, x1:x2, :] để chọn vùng có ngôi chùa từ ảnh lớn.

: cuối là để giữ tất cả các kênh màu RGB.
![image](https://github.com/user-attachments/assets/c95218ba-4737-40c5-8b48-c7d5d1e9f193)


CÂU 5
---
![image](https://github.com/user-attachments/assets/b5d6a58f-68aa-4d22-b3ba-b83fea0777b8)
# Tịnh tiến
dx = int(input("Nhập số pixel tịnh tiến theo trục x: "))
dy = int(input("Nhập số pixel tịnh tiến theo trục y: "))
transformed = nd.shift(image, shift=(dy, dx, 0))
→ Di chuyển ảnh theo vector (dx, dy).
# Xoay
angle = float(input("Nhập góc xoay (độ): "))
reshape = input("Reshape (True/False): ") == "True"
transformed = nd.rotate(image, angle=angle, reshape=reshape)
→ Xoay ảnh theo góc người dùng nhập.
# Phóng to
zoom_factor = float(input("Nhập hệ số phóng to: "))
transformed = nd.zoom(image, zoom=(zoom_factor, zoom_factor, 1))
→ Phóng to ảnh theo hệ số zoom.
![image](https://github.com/user-attachments/assets/a88d2627-dcba-4a70-bdcf-faef9c37a9a5)
# Thu nhỏ
shrink_factor = float(input("Nhập hệ số thu nhỏ: "))
transformed = nd.zoom(image, zoom=(shrink_factor, shrink_factor, 1))
→ Giống phóng to, chỉ khác hệ số < 1.

# Coordinate Map (Wave Effect)
A = float(input("Nhập biên độ sóng: "))
def wave(coord):
    x, y = coord
    return (x, y + A * np.sin(x / 10.0))
transformed = nd.geometric_transform(image, wave)
→ Áp dụng hàm sin để làm biến dạng ảnh kiểu sóng.
![image](https://github.com/user-attachments/assets/55e5ed4c-77db-4e14-8a03-d5290de392e6)


→ Hiển thị ảnh sau khi biến đổi theo lựa chọn của người dùng.

