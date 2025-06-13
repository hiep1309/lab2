1. Image Inverse Transformation (Biến đổi nghịch đảo ảnh)
Công nghệ sử dụng:

Thư viện: PIL (Pillow), NumPy, Matplotlib

Phương pháp: Xử lý điểm ảnh trực tiếp

Thuật toán:

python
img = Image.open('exercise/pagoda.jpg').convert('L')
im_1 = np.asarray(img)
im_2 = 255 - im_1
new_img = Image.fromarray(im_2)
Giải thích cách hoạt động:

Mở ảnh và chuyển sang grayscale (L)

Chuyển ảnh thành mảng NumPy

Áp dụng phép biến đổi nghịch đảo: 255 - giá trị pixel

Chuyển mảng kết quả trở lại thành ảnh

Kết quả: Ảnh âm bản với các vùng sáng thành tối và ngược lại

2. Gamma Correction (Hiệu chỉnh Gamma)
Công nghệ sử dụng:

Thư viện: PIL, NumPy, Matplotlib

Phương pháp: Biến đổi phi tuyến tính

Thuật toán:

python
gamma = 5
D1 = im_1.astype(float)
D2 = np.max(D1)
D3 = D1/D2
D3 = np.where(D3 == 0, 1e-10, D3)
gamma_corrected = np.exp(np.log(D3) * gamma) * 255.0
Giải thích cách hoạt động:

Chuẩn hóa giá trị pixel về khoảng [0,1]

Tránh log(0) bằng cách thay thế giá trị 0

Áp dụng công thức gamma: output = input^gamma

Scale lại về khoảng [0,255]

Kết quả: Điều chỉnh độ sáng phi tuyến (gamma > 1 làm tối ảnh, gamma < 1 làm sáng ảnh)

3. Histogram Equalization (Cân bằng histogram)
Công nghệ sử dụng:

Thư viện: PIL, NumPy

Phương pháp: Xử lý histogram

Thuật toán:

python
pixels = im1.flatten()
hist, bins = np.histogram(im1, 256, [0, 255])
cdf = hist.cumsum()
cdf_m = np.ma.masked_equal(cdf, 0)
num_cdf_m = (cdf_m - cdf_m.min()) * 255
den_cdf_m = (cdf.max() - cdf_m.min())
cdf_m = num_cdf_m / den_cdf_m
cdf = np.ma.filled(cdf_m, 0).astype('uint8')
im2 = cdf[pixels]
Giải thích cách hoạt động:

Tính histogram của ảnh

Tính hàm phân phối tích lũy (CDF)

Chuẩn hóa CDF về khoảng [0,255]

Ánh xạ lại các giá trị pixel dựa trên CDF

Kết quả: Cải thiện độ tương phản bằng cách phân bố đều histogram

4. Contrast Stretching (Kéo giãn tương phản)
Công nghệ sử dụng:

Thư viện: PIL, NumPy

Phương pháp: Biến đổi tuyến tính

Thuật toán:

python
a, b = im.min(), im.max()
stretched = 255 * (im.astype(float) - a) / (b - a)
Giải thích cách hoạt động:

Tìm giá trị pixel min (a) và max (b)

Áp dụng biến đổi tuyến tính để kéo giãn về toàn dải [0,255]

Kết quả: Tăng cường độ tương phản bằng cách sử dụng toàn bộ dải động

5. Fast Fourier Transform (Biến đổi Fourier nhanh)
Công nghệ sử dụng:

Thư viện: PIL, SciPy, NumPy

Phương pháp: Xử lý miền tần số

Thuật toán:

python
fft = np.abs(scipy.fftpack.fft2(im))
shifted = scipy.fftpack.fftshift(fft)
log_fft = np.log(1 + shifted)
Giải thích cách hoạt động:

Tính biến đổi Fourier 2D của ảnh

Dịch chuyển tần số 0 về trung tâm

Áp dụng log để hiển thị rõ hơn

Kết quả: Biểu diễn ảnh trong miền tần số