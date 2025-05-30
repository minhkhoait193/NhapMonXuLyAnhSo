Bài 1: Viết chương trình nạp một ảnh và lưu thành 3 ảnh với 3 màu khác nhau (RGB)

a là một mảng 3 chiều chứa dữ liệu ảnh RGB (height x width x 3).
a[:,:,0] là kênh R, a[:,:,1] là kênh G, a[:,:,2] là kênh B

![image](https://github.com/user-attachments/assets/992d7000-5691-406b-93f2-ed15f4a97430)
plt.imshow(r) truyền giá trị g hoặc b để đổi màu cho hình

Bài 2: Viết chương trình nạp một ảnh và hoán đổi giá trị các màu

numpy: để xử lý mảng dữ liệu ảnh.
imageio: để đọc và ghi ảnh.
matplotlib.pyplot: để hiển thị ảnh.
b1 = a.copy() để không làm thay đổi ảnh gốc.
b1[:,:,0] = a[:,:,1]: đưa kênh G sang vị trí kênh R.
b1[:,:,1] = a[:,:,0]: đưa kênh R sang vị trí kênh G.
Kết quả: ảnh có màu thay đổi giữa đỏ và xanh lá.

![image](https://github.com/user-attachments/assets/50da023a-7e5b-4438-9c03-d28a40dba7c7)

Bài 3: Nạp ảnh, chuyển sang hệ HSV và lưu 3 ảnh với 3 kênh H, S, V
                           
`a = iio.imread(...) / 255.0`  Đọc ảnh và chuẩn hóa về giá trị 0–1   
`rgb2hsv = np.vectorize(...)`  Hàm chuyển từng pixel từ RGB → HSV    
`h, s, v = rgb2hsv(...)`       Tách từng kênh Hue, Saturation, Value 
`iio.imwrite(...)`             Lưu mỗi kênh thành ảnh xám            
`plt.imshow(h, cmap='gray')`   Hiển thị kênh H dưới dạng ảnh xám     

![image](https://github.com/user-attachments/assets/83aad370-000c-4a32-bd56-d643497bec1c)

Bài 4: Nạp ảnh, đổi sang HSV rồi sửa H = 1/3 và V = ¾, sau đó lưu ảnh mới
h / 3	Làm lệch tông màu ( từ đỏ → xanh)
v * 0.75	Làm ảnh tối hơn
np.stack(...)	Gộp 3 kênh lại thành ảnh màu
![image](https://github.com/user-attachments/assets/a6509c66-758d-4c8d-bdcf-1f3e3d0b4ca0)

Bài 5: Sử dụng mean filter cho các hình trong thư mục "Exercise"  

Tạo ma trận 5x5 toàn số 1 → np.ones((5,5))
Chia cho 25 để lấy trung bình cộng → k là kernel 5x5.
Mỗi ô có giá trị 1/25 = 0.04
Lấy tên từng file ảnh trong thư mục Exercise.
sn.convolve(a ,k) là hàm thực hiện convolution (tích chập) giữa ảnh và kernel k.
Kết quả là ảnh đã làm mịn.
astype(np.uint8): ép kiểu dữ liệu về 8-bit (giá trị từ 0–255).
![image](https://github.com/user-attachments/assets/6fb11172-48d3-497b-acbe-f566c96c1c8c)
![image](https://github.com/user-attachments/assets/91ba399b-39a2-491a-a7e1-488a9d73b81a)

