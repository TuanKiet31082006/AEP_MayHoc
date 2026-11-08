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

## 7. Kết quả xây dựng và đánh giá mô hình

### 7.1. Chia dữ liệu
- Sử dụng dữ liệu sau tiền xử lý `appliances_processed.csv`.
- Biến mục tiêu: `Appliances`.
- Loại bỏ cột `date` khỏi tập đặc trưng đầu vào.
- Chia dữ liệu theo thứ tự thời gian với tỷ lệ 80% Train và 20% Test.
- Tập Train: 15.785 mẫu.
- Tập Test: 3.947 mẫu.

### 7.2. Các mô hình đã thử nghiệm

Nhóm đã thực hiện huấn luyện và đánh giá 5 mô hình:
- Baseline: DummyRegressor với chiến lược dự đoán giá trị trung bình.
- Linear Regression: mô hình hồi quy tuyến tính.
- Ridge Regression: sử dụng StandardScaler và Ridge với alpha = 1.0.
- Random Forest: n_estimators = 100, max_depth = 15, random_state = 42.
- Gradient Boosting: n_estimators = 100, learning_rate = 0.1, max_depth = 3, random_state = 42.

### 7.3. Kết quả đánh giá

| Mô hình | MAE | RMSE | R² |
|---|---:|---:|---:|
| Baseline | 52.689 | 91.054 | -0.000 |
| Linear Regression | 29.010 | 62.005 | 0.536 |
| Ridge Regression | 29.012 | 62.005 | 0.536 |
| Random Forest | 77.332 | 114.374 | -0.578 |
| Gradient Boosting | 110.903 | 144.916 | -1.533 |

### 7.4. Kết quả lựa chọn mô hình
- Linear Regression được lựa chọn làm mô hình tốt nhất trong các mô hình đã thử nghiệm.
- Mô hình đạt MAE = 29.010, RMSE = 62.005 và R² = 0.536.
- Mô hình được lưu tại `models/best_model.pkl`.
- Kết quả dự đoán được lưu tại `reports/prediction_results.csv`.
- Các biểu đồ Actual vs Predicted và Residual Plot được lưu trong thư mục `images/`.

## 8. Tài liệu thực hiện

- Notebook: `notebooks/01_EDA_Preprocessing.ipynb`.
- Dữ liệu gốc: `data/raw/energydata_complete.csv`.
- Dữ liệu sau xử lý: `data/processed/appliances_processed.csv`.
- Biểu đồ: `images/`.