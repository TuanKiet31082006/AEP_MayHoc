# EXPERIMENT LOG
## Đề tài: Appliances Energy Prediction (Regression)

**Người thực hiện:** Nguyễn Tuấn Kiệt - 3124411145

**Nội dung phụ trách:** Thu thập dữ liệu, khám phá dữ liệu và tiền xử lý.

---

## 1. Thu thập dữ liệu

- Nguồn dữ liệu: UCI Machine Learning Repository.
- Tên bộ dữ liệu: Appliances Energy Prediction.
- File dữ liệu: `energydata_complete.csv`.
- Kết quả: Tải và đọc dữ liệu thành công.

## 2. Khám phá dữ liệu (EDA)

### 2.1. Kiểm tra tổng quan

- Sử dụng Pandas để đọc và kiểm tra dữ liệu.
- Các hàm sử dụng: `head()`, `info()`, `describe()`, `shape`.
- Kết quả ban đầu: 19.735 dòng và 29 cột.

### 2.2. Kiểm tra chất lượng dữ liệu

- Kiểm tra giá trị thiếu bằng `isnull().sum()`.
- Kiểm tra dòng trùng lặp bằng `duplicated().sum()`.

### 2.3. Trực quan hóa dữ liệu

Đã thực hiện 6 biểu đồ:

1. Phân phối mức tiêu thụ điện Appliances.
2. Ma trận tương quan giữa các biến.
3. Mức tiêu thụ điện trung bình theo giờ.
4. Mức tiêu thụ điện trung bình theo thứ trong tuần.
5. Mức tiêu thụ điện trung bình hằng ngày.
6. Biểu đồ hộp kiểm tra ngoại lệ Appliances.

## 3. Kiểm tra ngoại lệ

- Phương pháp sử dụng: IQR.
- Biểu đồ sử dụng: Boxplot.
- Kết quả: Phát hiện nhiều giá trị ngoại lệ ở biến Appliances.
- Cách xử lý: Chưa loại bỏ ngoại lệ vì các giá trị này có thể phản ánh mức tiêu thụ điện thực tế.

## 4. Tạo đặc trưng mới

Đã tạo 5 đặc trưng:

- `hour`: Giờ trong ngày.
- `day_of_week`: Thứ trong tuần.
- `is_weekend`: Xác định ngày cuối tuần.
- `lag_1`: Mức tiêu thụ điện tại thời điểm trước đó.
- `rolling_mean`: Giá trị tiêu thụ điện trung bình trượt của 3 thời điểm trước đó.

## 5. Tiền xử lý dữ liệu

- Chuyển đổi cột `date` sang kiểu dữ liệu thời gian.
- Sắp xếp dữ liệu theo thời gian.
- Loại bỏ 3 dòng đầu tiên phát sinh giá trị thiếu do tạo đặc trưng trễ và trung bình trượt.
- Kiểm tra lại dữ liệu sau xử lý.

## 6. Kết quả đầu ra

- Số dòng sau xử lý: 19.732.
- Số cột sau xử lý: 34.
- Số giá trị thiếu: 0.
- File đầu ra: `appliances_processed.csv`.
- Vị trí lưu: `data/processed/`.
- Các biểu đồ được lưu trong thư mục `images/`.

## 7. Công việc chưa thực hiện

- Chưa chia dữ liệu thành tập huấn luyện và kiểm tra.
- Chưa chuẩn hóa dữ liệu.
- Chưa huấn luyện mô hình hồi quy.
- Chưa đánh giá kết quả mô hình.

Các công việc này sẽ được phối hợp thực hiện trong giai đoạn xây dựng và đánh giá mô hình.

## 8. Tài liệu thực hiện

- Notebook: `notebooks/01_EDA_Preprocessing.ipynb`.
- Dữ liệu gốc: `data/raw/energydata_complete.csv`.
- Dữ liệu sau xử lý: `data/processed/appliances_processed.csv`.
- Biểu đồ: `images/`.