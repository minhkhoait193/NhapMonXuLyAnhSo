
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
![image](https://github.com/user-attachments/assets/ad3492ac-d3f3-4dc6-acef-39265f7a26ed)
-
![image](https://github.com/user-attachments/assets/69566c3c-4e0a-447a-9c6f-605be5872a83)
-
Chương trình tạo menu cho phép người dùng chọn một trong ba phương pháp xử lý ảnh theo miền tần số:

F – Fast Fourier Transform (FFT):
Biến đổi ảnh từ không gian không gian (spatial domain) sang miền tần số để phân tích phổ tần số.

L – Butterworth Lowpass Filter:
Lọc tần số thấp, giúp làm mượt ảnh và loại bỏ chi tiết tần số cao (nhiễu).

H – Butterworth Highpass Filter:
Lọc tần số cao, giúp làm nổi bật các cạnh và chi tiết nhỏ trong ảnh.

cau 3
=
![image](https://github.com/user-attachments/assets/89a71ca7-c61f-48de-bf0c-f090759dea27)
-
![image](https://github.com/user-attachments/assets/ab6fb31c-83f9-41d1-9434-301dce799671)
-
Đảo thứ tự kênh màu RGB một cách ngẫu nhiên:
Mỗi ảnh màu được tráo đổi thứ tự các kênh R, G, B để tạo hiệu ứng màu khác biệt.
Chọn ngẫu nhiên một phép biến đổi trong Câu 1 để áp dụng cho ảnh đã chuyển sang grayscale, gồm:
Image Inverse
Gamma Correction
Log Transformation
Histogram Equalization
Contrast Stretching

cau 4
=
![image](https://github.com/user-attachments/assets/bd6d787a-00c3-4709-adee-1e0d8757ed19)
-
![image](https://github.com/user-attachments/assets/0f9153ce-4275-4b33-80ac-aa6ecea16b14)
-
Đảo thứ tự kênh màu RGB một cách ngẫu nhiên:
Tương tự Câu 3, tráo đổi thứ tự các kênh R, G, B để thay đổi màu sắc ảnh.

Chọn ngẫu nhiên một phép biến đổi tần số trong Câu 2:

Fast Fourier Transform (FFT)

Butterworth Lowpass Filter

Butterworth Highpass Filter

Áp dụng thêm bộ lọc không gian phù hợp:

Nếu chọn Lowpass, áp dụng thêm Min Filter (lọc lấy giá trị nhỏ nhất trong vùng lân cận) để tăng hiệu ứng làm mượt.

Nếu chọn Highpass, áp dụng thêm Max Filter (lọc lấy giá trị lớn nhất) để làm rõ chi tiết biên





