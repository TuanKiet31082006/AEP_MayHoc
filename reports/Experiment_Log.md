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
### 7.5. Kiểm tra và xử lý lỗi trong quá trình dự đoán

Trong quá trình sử dụng mô hình Linear Regression để thực hiện dự đoán trên tập dữ liệu kiểm tra, nhóm gặp lỗi do số lượng đặc trưng đầu vào không khớp với số lượng đặc trưng mà mô hình đã được huấn luyện.

Cụ thể:

Tập dữ liệu đầu vào X_test ban đầu có 33 đặc trưng.

Mô hình Linear Regression được huấn luyện với 32 đặc trưng.

Nguyên nhân là cột date vẫn còn trong tập dữ liệu dự đoán.

Cách khắc phục:

Nhóm tiến hành loại bỏ cột date khỏi tập đặc trưng đầu vào trước khi thực hiện dự đoán, nhằm đảm bảo dữ liệu đầu vào có cùng cấu trúc với dữ liệu huấn luyện.

Kết quả:

Sau khi điều chỉnh, mô hình thực hiện dự đoán thành công trên tập kiểm tra và có thể tiếp tục sử dụng kết quả để đánh giá hiệu suất.
### 7.6. Trực quan hóa kết quả dự đoán

Sau khi hoàn thành quá trình dự đoán, nhóm tiến hành trực quan hóa kết quả nhằm đánh giá trực quan khả năng dự đoán của mô hình Linear Regression.

Nhóm sử dụng hai biểu đồ:

Actual vs Predicted: So sánh giá trị tiêu thụ năng lượng thực tế với giá trị do mô hình dự đoán.

Residual Plot: Thể hiện phần sai số giữa giá trị thực tế và giá trị dự đoán, giúp quan sát mức độ phân bố sai số của mô hình.

Các biểu đồ được lưu trong thư mục images/ để phục vụ việc phân tích và đánh giá kết quả thực nghiệm.
### 7.7. Nhận xét và phân tích kết quả thực nghiệm

Dựa trên kết quả đánh giá năm mô hình, nhóm đưa ra một số nhận xét như sau:

- **Baseline:** Có MAE = 52.689 và RMSE = 91.054. Đây là mô hình cơ sở, được sử dụng làm mốc so sánh với các mô hình còn lại.
- **Linear Regression:** Đạt MAE = 29.010, RMSE = 62.005 và R² = 0.536. Đây là mô hình có kết quả tốt nhất trong các mô hình được thử nghiệm.
- **Ridge Regression:** Đạt MAE = 29.012, RMSE = 62.005 và R² = 0.536. Kết quả gần tương đương Linear Regression.
- **Random Forest:** Đạt MAE = 77.332, RMSE = 114.374 và R² = -0.578. Kết quả chưa tốt trên tập dữ liệu kiểm tra.
- **Gradient Boosting:** Đạt MAE = 110.903, RMSE = 144.916 và R² = -1.533. Đây là mô hình có kết quả kém nhất trong năm mô hình.

Qua kết quả trên, nhóm nhận thấy Linear Regression và Ridge Regression có hiệu suất tốt hơn các mô hình còn lại.

Các chỉ số MAE và RMSE càng thấp thì sai số dự đoán càng nhỏ. Chỉ số R² càng gần 1 thì khả năng giải thích sự biến thiên của biến mục tiêu càng tốt.

Hai mô hình Random Forest và Gradient Boosting có R² âm, cho thấy khả năng dự đoán trên tập kiểm tra chưa đạt hiệu quả tốt.

### 7.8. Tổng hợp kết quả thực nghiệm

Sau quá trình xây dựng và đánh giá, nhóm đã đạt được các kết quả:

- Hoàn thành quá trình chuẩn bị và chia dữ liệu huấn luyện, kiểm tra.
- Huấn luyện và đánh giá thành công năm mô hình hồi quy.
- So sánh kết quả dựa trên ba chỉ số MAE, RMSE và R².
- Lựa chọn Linear Regression làm mô hình tốt nhất.
- Lưu mô hình đã lựa chọn tại `models/best_model.pkl`.
- Xuất kết quả dự đoán tại `reports/prediction_results.csv`.
- Lưu các biểu đồ đánh giá trong thư mục `images/`.

Kết quả thực nghiệm là cơ sở để nhóm tiếp tục hoàn thiện bài toán dự đoán mức tiêu thụ năng lượng của các thiết bị gia dụng.
## 8. Tài liệu thực hiện

- Notebook 01: `notebooks/01_EDA_Preprocessing.ipynb`.
- Notebook 02: Notebook huấn luyện và đánh giá mô hình.
- Notebook 03: Notebook dự đoán và tổng hợp kết quả.
- Dữ liệu gốc: `data/raw/energydata_complete.csv`.
- Dữ liệu sau xử lý: `data/processed/appliances_processed.csv`.
- Mô hình tốt nhất: `models/best_model.pkl`.
- Kết quả dự đoán: `reports/prediction_results.csv`.
- Biểu đồ: `images/`.
## 9. Kết luận và hướng phát triển

### 9.1. Kết luận

Qua quá trình thực hiện đề tài Appliances Energy Prediction, nhóm đã hoàn thành các bước cơ bản trong quy trình xây dựng mô hình học máy, bao gồm thu thập dữ liệu, khám phá dữ liệu, tiền xử lý, xây dựng đặc trưng, huấn luyện và đánh giá mô hình.

Trong quá trình thực nghiệm, nhóm đã thử nghiệm năm mô hình hồi quy khác nhau. Kết quả cho thấy Linear Regression đạt hiệu suất tốt nhất với MAE = 29.010, RMSE = 62.005 và R² = 0.536.

Qua đó, nhóm đã có được mô hình dự đoán ban đầu và các kết quả cần thiết để tiếp tục phát triển đề tài.

### 9.2. Hướng phát triển

Trong giai đoạn tiếp theo, nhóm dự kiến:

- Nghiên cứu và thử nghiệm thêm các thuật toán học máy khác.
- Tối ưu hóa tham số để cải thiện hiệu suất dự đoán.
- Tiếp tục lựa chọn và xây dựng các đặc trưng đầu vào phù hợp.
- Phân tích sâu hơn các sai số dự đoán của mô hình.
- Hoàn thiện kết quả thực nghiệm và báo cáo cuối kỳ.

### 9.3. Tổng kết

Quá trình thực hiện đề tài giúp nhóm củng cố kiến thức về bài toán hồi quy, kỹ năng xử lý dữ liệu, trực quan hóa dữ liệu và xây dựng mô hình học máy. Đây là nền tảng để nhóm tiếp tục hoàn thiện đề tài trong giai đoạn tiếp theo.