Câu 6: Sử dụng các filter khử nhiễu đã học để xử lý ảnh trong thư mục Exercise. Cho biết filter nào khử nhiễu tốt nhất.

for fname in os.listdir('Exercise'):	Duyệt qua từng ảnh trong thư mục Exercise
| Filter | Tác dụng chính               | Ưu điểm         | Nhược điểm             |
| ------ | ---------------------------- | --------------- | ---------------------- |
| Mean   | Làm mịn ảnh đều              | Dễ tính, nhanh  | Làm mờ cạnh            |
| Median | Loại nhiễu muối tiêu rất tốt | Bảo toàn biên   | Tính chậm hơn          |
| Max    | Làm sáng vùng tối nhỏ        | Xử lý bóng đổ   | Có thể mất chi tiết    |
| Min    | Làm tối vùng sáng nhỏ        | Xử lý đốm trắng | Có thể làm ảnh tối quá |


Median Filter thường là lựa chọn tốt nhất để khử nhiễu muối tiêu (salt & pepper noise)

![image](https://github.com/user-attachments/assets/776bd502-ef57-42f4-88b0-f31456207522)
![image](https://github.com/user-attachments/assets/71a7dda7-2fa6-4150-b2c0-d956f8d42451)
![image](https://github.com/user-attachments/assets/202129ff-4717-44b8-b809-56ad4bbb5cdd)
![image](https://github.com/user-attachments/assets/357006fa-ff22-46a1-acda-651d4f03db75)



Câu 7: Viết chương trình sử dụng các filter xác định biên của các hình trong thư mục Exercise. Lưu các hình vào máy. (Khử nhiễu trước khi xác định biên)
Sau khi áp dụng các bộ lọc phát hiện biên cho ảnh đã khử nhiễu, kết quả cho thấy:
Canny filter cho biên rõ nét nhất, dễ dàng quan sát đường viền vật thể, đặc biệt hiệu quả với ảnh nhiễu như balloons_noisy.png.
Sobel và Prewitt có hiệu quả tương đối tốt với ảnh ít nhiễu (flower.jpeg), nhưng dễ bị nhiễu giả khi ảnh quá rối (baby.jpeg).
Việc khử nhiễu trước khi phát hiện biên là cần thiết, giúp giảm sai lệch và làm nổi bật biên rõ hơn.
→ Canny là bộ lọc phù hợp nhất cho bài toán phát hiện biên sau khi xử lý nhiễu.
![image](https://github.com/user-attachments/assets/d25c93eb-b0ea-4030-b4e4-4e1b6c1ddca2)


Câu 8 – Đổi màu RGB ngẫu nhiên sau khi khử nhiễu
![image](https://github.com/user-attachments/assets/c4c12eb6-d1fd-494c-8e46-deb9e2f351fb)


# Tạo thư mục lưu ảnh nếu chưa có
os.makedirs('picture', exist_ok=True)

# Duyệt từng ảnh trong thư mục 'exercise' và lấy file có đuôi png và jpeg
for fname in os.listdir('exercise'):
    if fname.endswith('.png') or fname.endswith('.jpeg') :
        path = os.path.join('exercise', fname)
        print('Xử lý ảnh:', fname)

        
 # Bước 1: Đọc ảnh
 a = iio.imread(path)       

Nếu ảnh là RGB (3 kênh):

Tạo mảng rỗng có kích thước giống ảnh gốc.

Dùng median_filter cho từng kênh màu (R, G, B) riêng biệt để khử nhiễu.
Nếu ảnh là ảnh xám (grayscale) thì lọc trực tiếp luôn.
  if len(a.shape) == 3:
    a_filtered = np.zeros_like(a)
    for c in range(3):
    a_filtered[:,:,c] = sn.median_filter(a[:,:,c], size=3)
    else:
            a_filtered = sn.median_filter(a, size=3)

idx = np.random.permutation(3)
b = a_filtered[:,:,idx]
Sinh ra một thứ tự ngẫu nhiên của [0, 1, 2] — ví dụ [2, 0, 1].

iio.imwrite(f'picture/rgb_random_{fname}', b)
Lưu ảnh đã đổi màu vào thư mục picture/ với tên mới.



Câu 9 – Đổi màu HSV ngẫu nhiên nhưng không trùng thứ tự kênh cũ

![image](https://github.com/user-attachments/assets/9201d3c2-9704-4285-939b-d0371d8e5ff6)


colorsys.rgb_to_hsv -colorsys.hsv_to_rgb	 	Chuyển từ RGB sang HSV và ngược lại
np.mod(h + random, 1)	 Xoay vòng giá trị Hue để đổi màu
np.clip(s * factor, 0, 1)	 Điều chỉnh độ bão hòa (đậm nhạt) và độ sáng
np.stack([r,g,b], axis=2)	Ghép lại thành ảnh màu hoàn chỉnh

hệ màu HSV rất thuận tiện cho việc điều chỉnh màu sắc bằng cách thay đổi H, S, V một cách ngẫu nhiên, ta có thể tạo ra nhiều phiên bản màu khác nhau từ cùng một ảnh gốc, trong khi vẫn giữ được hình dạng và nội dung ảnh
 
