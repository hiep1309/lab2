#1.1
Công nghệ:
Thư viện: Pillow (PIL), NumPy, Matplotlib
Hàm chính: np.asarray(), 255 - image_array, Image.fromarray()

Thuật toán:
Nghịch đảo giá trị pixel: output_pixel=255−input_pixel
Mục đích: Tạo hiệu ứng âm bản.

Cách hoạt động:
Chuyển ảnh sang mảng NumPy.
Áp dụng phép trừ từng pixel từ 255.
Chuyển lại thành ảnh và hiển thị.

#1.2
Công nghệ:
Thư viện: NumPy (tính toán mũ), PIL
Hàm chính: np.power(), np.clip()

Thuật toán:
Công thức gamma: output=255×(input/255)^γ
 Mục đích: Điều chỉnh độ sáng/độ tương phản phi tuyến tính.

Cách hoạt động:
Chuẩn hóa giá trị pixel về [0, 1].
Áp dụng hàm mũ với hệ số gamma.
Chuyển về khoảng [0, 255] và hiển thị.

#1.3
Công nghệ:
Thư viện: NumPy (logarithm), PIL
Hàm chính: np.log1p(), np.max()

Thuật toán:
Công thức log: output= (log(1+max_value))/(c×log(1+input))
​(với c=255)
Mục đích: Nén dải động, làm rõ vùng tối.

Cách hoạt động:
Tính logarit của từng pixel sau khi chuẩn hóa.
Co giãn kết quả về [0, 255].

#1.4
Công nghệ:
Thư viện: NumPy (histogram, CDF), PIL
Hàm chính: np.histogram(), cumsum()

Thuật toán:
Cân bằng histogram:
Tính histogram và CDF.
Ánh xạ lại pixel dựa trên CDF chuẩn hóa.
Mục đích: Cải thiện độ tương phản toàn cục.

Cách hoạt động:
Làm phẳng ảnh thành mảng 1D.
Tính CDF và ánh xạ lại giá trị pixel.

#1.5
Công nghệ:
Thư viện: NumPy (min/max), PIL
Hàm chính: np.min(), np.max()

Thuật toán:
Công thức co giãn tuyến tính: output=255× (max−min/input−min)
Mục đích: Kéo dải cường độ về toàn bộ khoảng [0, 255].

Cách hoạt động:
Tìm giá trị min/max của ảnh.
Áp dụng công thức co giãn cho từng pixel.

#1.6.1
Công nghệ:
Thư viện: scipy.fftpack, NumPy
Hàm chính: fft2(), fftshift(), np.log1p()

Thuật toán:
Biến đổi Fourier 2D:
Tính FFT → dịch tần số 0 về trung tâm.
Hiển thị phổ biên độ (log scale).
Mục đích: Phân tích thành phần tần số trong ảnh.

Cách hoạt động:
Áp dụng FFT và dịch chuyển phổ.
Tính log để hiển thị rõ các tần số thấp.

#1.6.2
Công nghệ:
Thư viện: scipy.fftpack, math (tính khoảng cách)
Hàm chính: fft2(), ifft2(), vòng lặp tạo bộ lọc.

Thuật toán:
Bộ lọc Butterworth:
Lowpass: H(u,v)= 1/(1+(D(u,v)/D0)^2n
Highpass: H(u,v)= 1/(1+(D0/D(u,v))^2n
(với D(u,v) là khoảng cách đến tần số trung tâm)
Mục đích: Làm mờ (lowpass) hoặc làm nổi biên (highpass).

Cách hoạt động:
Tạo bộ lọc trong miền tần số.
Nhân phổ FFT với bộ lọc → IFFT để trở về miền không gian.

​#b1: 
Công nghệ sử dụng
Thư viện chính:
Pillow (PIL): Đọc/ghi ảnh, chuyển đổi định dạng (RGB ↔ Grayscale).
NumPy: Xử lý mảng pixel (phép toán số học, chuẩn hóa giá trị).
Matplotlib: Hiển thị ảnh gốc và ảnh đã xử lý.
Phương pháp: Biến đổi điểm ảnh (pixel-level transformations).

Thuật toán và cách hoạt động
Image Inverse (I):
Công thức: output=255−input.
Cách hoạt động: Đảo ngược giá trị pixel để tạo hiệu ứng âm bản.
inverted_img = Image.fromarray(255 - np.array(img))
​Gamma Correction (G):
Công thức:  output=255×(input/255)^γ
Cách hoạt động: Điều chỉnh độ sáng phi tuyến tính (gamma < 1: làm sáng, gamma > 1: làm tối).
corrected = np.power(img_array / 255.0, gamma) * 255
Log Transformation (L):
Công thức: 
output= (255×log(1+input))/log(1+max_pixel)
Cách hoạt động: Nén dải động, làm rõ chi tiết vùng tối.
c = 255 / np.log(1 + np.max(img_array))
log_transformed = c * np.log(1 + img_array)
Histogram Equalization (H):
Cách hoạt động: Cân bằng histogram để phân bố đều giá trị pixel.
cdf = hist.cumsum()
equalized = cdf[img_flatten].reshape(img_shape)
Contrast Stretching (C):
Công thức: 
output=255× (input−min / max−min)
Cách hoạt động: Kéo giãn dải cường độ về toàn bộ khoảng [0, 255].
stretched = 255 * (img_array - a) / (b - a)

#b2: 
Công nghệ sử dụng
Thư viện chính:
scipy.fftpack: Tính FFT 2D và dịch chuyển phổ tần số.
NumPy: Tạo bộ lọc Butterworth.
Phương pháp: Lọc tần số (Frequency-domain filtering).

Thuật toán và cách hoạt động
Fast Fourier Transform (F):
Bước 1: Tính FFT 2D → Dịch tần số 0 về trung tâm.
Bước 2: Hiển thị phổ biên độ (log scale).
fft = np.fft.fft2(img_array)
fft_shift = np.fft.fftshift(fft)
magnitude = np.log1p(np.abs(fft_shift))
Butterworth Lowpass Filter (L):
Công thức: 
H(u,v)= 1/(1+(D(u,v)/D0)^2n
Mục đích: Làm mờ ảnh bằng cách giữ lại tần số thấp.
for i in range(M):
    for j in range(N):
        r = np.sqrt((i - center)**2 + (j - center)**2)
        H[i,j] = 1 / (1 + (r / d0)**(2*n))
Butterworth Highpass Filter (H):
Công thức: H(u,v)= 1/(1+(D0/D(u,v))^2n
Mục đích: Làm nổi biên bằng cách giữ lại tần số cao.
H[i,j] = 1 / (1 + (d0 / r)**(2*n))

#b3: 
Công nghệ sử dụng
Thư viện:
random: Hoán vị kênh màu và chọn phép biến đổi ngẫu nhiên.
NumPy: Xử lý mảng màu RGB.
Phương pháp: Kết hợp nhiều phép biến đổi.

Thuật toán và cách hoạt động
RGB Permutation:
Hoán đổi vị trí các kênh R, G, B ngẫu nhiên.
perm = random.sample([0, 1, 2], 3)
new_arr[:,:,0] = arr[:,:,perm[0]] 
Random Transform:
Chọn ngẫu nhiên 1 trong 5 phương pháp (Inverse, Gamma, Log, Histogram, Contrast).
choice = random.choice(['inverse', 'gamma', 'log', 'histogram', 'contrast'])

#b4: 
Công nghệ sử dụng
Thư viện:
scipy.ndimage: Áp dụng bộ lọc Min/Max.
scipy.fftpack: Kết hợp FFT với lọc không gian.
Phương pháp: Hybrid (Tần số + Không gian).

Thuật toán và cách hoạt động
Min/Max Filter:
Min Filter: Thay pixel bằng giá trị nhỏ nhất trong lân cận (khử nhiễu sáng).
Max Filter: Thay pixel bằng giá trị lớn nhất (khử nhiễu tối).
min_filtered = scipy.ndimage.minimum_filter(img, size=3)
max_filtered = scipy.ndimage.maximum_filter(img, size=3)
Random Transform với FFT:
Áp dụng Lowpass/Highpass Filter → Lọc Min/Max kết hợp.
if choice == 'lowpass':
    fft_shift = fft_shift * mask_lowpass  # Nhân với bộ lọc