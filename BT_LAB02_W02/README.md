
cau 1
=
![image](https://github.com/user-attachments/assets/d46cba19-6ed6-46ca-be9f-889e45621220)
-
![image](https://github.com/user-attachments/assets/915565e2-2be2-459a-8c0b-a2400f6ca50d)
-

Nhập phím I, G, L, H, hoặc C → áp dụng thuật toán tương ứng cho ảnh trong thư mục exercise
Tự động lưu ảnh kết quả và hiển thị bằng matplotlib

def inverse_transform(img):
    return 255 - img
Lật ngược độ sáng: pixel càng sáng → càng tối và ngược lại.

Gamma Correction
----
def gamma_correction(img, gamma=0.5):
    img_float = img.astype(float)
    img_norm = img_float / 255.0
    corrected = np.power(img_norm, gamma)
    return np.uint8(corrected * 255)
Điều chỉnh độ sáng ảnh bằng công thức:output=255×(input/255)^γ

Logarithmic Transformation
----
def log_transform(img):
    img_float = img.astype(float)
    c = 255 / np.log(1 + np.max(img_float))
    log_img = c * np.log(1 + img_float)
    return np.uint8(log_img)

công thức: output=c⋅log(1+input)
Histogram Equalization
----
def histogram_equalization(img):
    return cv2.equalizeHist(img)
Tăng độ tương phản tổng thể bằng cách phân phối lại histogram.

Contrast Stretching
----
def contrast_stretching(img):
    a = np.min(img)
    b = np.max(img)
    stretched = 255 * (img - a) / (b - a)
    return np.uint8(stretched)
Kéo giãn độ tương phản từ khoảng [a, b] về [0, 255]

Hàm main() chính
Nhận input từ người dùng (I, G, L, H, C)
Duyệt tất cả ảnh trong thư mục exercise
Chuyển ảnh sang grayscale, xử lý theo lựa chọn
Lưu ảnh và hiển thị bằng matplotlib

Ảnh được xử lý theo lựa chọn và lưu trong thư mục exercise/ dưới dạng filename_suffix.png
Ví dụ: input.jpg + lựa chọn G → input_gamma.png

cau 2
=


