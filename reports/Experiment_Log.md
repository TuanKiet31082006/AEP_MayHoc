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

Kết quả kiểm tra ban đầu:

- Tổng số giá trị thiếu: 0.

- Tổng số dòng trùng lặp: 0.

Sau khi tạo các đặc trưng lag_1 và rolling_mean:

- Phát sinh 4 giá trị thiếu do không đủ dữ liệu quá khứ.

- Tiến hành loại bỏ 3 dòng đầu tiên chưa có đủ dữ liệu quá khứ.

- Sau xử lý, dữ liệu không còn giá trị thiếu.

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

Sau khi huấn luyện và lựa chọn mô hình Linear Regression,

nhóm tiến hành trực quan hóa kết quả dự đoán trong Notebook 02.

Nhóm sử dụng hai biểu đồ:

- Actual vs Predicted: So sánh giá trị thực tế với giá trị dự đoán.

- Residual Plot: Thể hiện sự phân bố sai số giữa giá trị thực tế

  và giá trị dự đoán.

Hai biểu đồ được tạo và lưu trong thư mục `images/`:

- `images/actual_vs_predicted.png`

- `images/residual_plot.png`

Notebook 03 tiếp tục sử dụng mô hình đã lưu để thực hiện dự đoán,

đánh giá kết quả và xuất dữ liệu dự đoán ra file CSV.

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

### 7.9. Thực nghiệm bổ sung: So sánh 5 mô hình theo tỷ lệ chia dữ liệu

**Ngày thực hiện: 27/11/2026**

### 7.9.1. Mục tiêu

Tiến hành thực nghiệm bổ sung nhằm đánh giá ảnh hưởng của tỷ lệ chia dữ liệu huấn luyện và kiểm tra đến hiệu suất của 5 mô hình hồi quy.

### 7.9.2. Phương pháp thực hiện

Sử dụng bộ dữ liệu `appliances_processed.csv` đã tiền xử lý, giữ nguyên dữ liệu gốc và thứ tự thời gian.

Thử nghiệm 5 mô hình:

- Baseline.

- Linear Regression.

- Ridge Regression.

- Random Forest.

- Gradient Boosting.

Các tỷ lệ chia dữ liệu:

- 70% Train – 30% Test.

- 80% Train – 20% Test.

- 90% Train – 10% Test.

Tổng cộng thực hiện 15 lượt huấn luyện và đánh giá.

### 7.9.3. Kết quả thực nghiệm

| Tỷ lệ | Mô hình | MAE | RMSE | R² |

|---|---|---:|---:|---:|

| 70/30 | Baseline | 53.4086 | 91.6539 | -0.0016 |

| 70/30 | Linear Regression | 29.6113 | 62.2602 | 0.5378 |

| 70/30 | Ridge | 29.6159 | 62.2609 | 0.5378 |

| 70/30 | Random Forest | 64.7515 | 111.0613 | -0.4706 |

| 70/30 | Gradient Boosting | 106.9155 | 153.9727 | -1.8266 |

| 80/20 | Baseline | 52.6886 | 91.0536 | -0.0003 |

| 80/20 | Linear Regression | 29.0102 | 62.0053 | 0.5361 |

| 80/20 | Ridge | 29.0117 | 62.0055 | 0.5361 |

| 80/20 | Random Forest | 77.3325 | 114.3738 | -0.5783 |

| 80/20 | Gradient Boosting | 110.9029 | 144.9163 | -1.5339 |

| 90/10 | Baseline | 52.9527 | 93.9460 | -0.0007 |

| 90/10 | Linear Regression | 27.9618 | 62.7410 | 0.5537 |

| 90/10 | Ridge | 27.9564 | 62.7403 | 0.5537 |

| 90/10 | Random Forest | 35.0628 | 67.2875 | 0.4867 |

| 90/10 | Gradient Boosting | 30.6437 | 62.4601 | 0.5577 |

### 7.9.4. Nhận xét kết quả

- Baseline có R² gần bằng 0 ở cả ba tỷ lệ, đóng vai trò làm mô hình đối chứng.

- Linear Regression và Ridge có kết quả tương đối ổn định qua các tỷ lệ chia dữ liệu.

- Random Forest và Gradient Boosting có kết quả chưa tốt ở tỷ lệ 70/30 và 80/20, thể hiện qua R² âm.

- Ở tỷ lệ 90/10, hai mô hình trên cải thiện đáng kể.

- Gradient Boosting đạt R² cao nhất là 0.5577.

- Ridge đạt MAE thấp nhất là 27.9564.

Kết quả cho thấy tỷ lệ chia dữ liệu có ảnh hưởng đến hiệu suất đánh giá. Không thể kết luận rằng cứ tăng tỷ lệ dữ liệu huấn luyện thì tất cả mô hình đều tốt hơn.

### 7.9.5. Trường hợp kết quả không tốt và phân tích

Trong quá trình thực nghiệm, chương trình chạy thành công và không ghi nhận lỗi thực thi.

Tuy nhiên, có các trường hợp mô hình cho kết quả đánh giá không tốt:

- Random Forest ở tỷ lệ 70/30 và 80/20 có R² lần lượt là -0.4706 và -0.5783.

- Gradient Boosting ở tỷ lệ 70/30 và 80/20 có R² lần lượt là -1.8266 và -1.5339.

**Phân tích:** R² âm cho thấy mô hình dự đoán kém hơn phương pháp dự đoán bằng giá trị trung bình trên tập kiểm tra. Cần tiếp tục kiểm tra sự khác biệt giữa các giai đoạn dữ liệu và phân phối biến mục tiêu để xác định nguyên nhân cụ thể.

**Cách xử lý:** Giữ nguyên kết quả thực nghiệm, không tự ý loại bỏ số liệu. Tiếp tục phân tích dữ liệu và xem xét điều chỉnh tham số mô hình trong các lần thử nghiệm tiếp theo.

### 7.9.6. Kết luận

Nhóm đã hoàn thành 15 lượt thực nghiệm với 5 mô hình và 3 tỷ lệ chia dữ liệu. Kết quả bổ sung giúp đánh giá rõ hơn sự thay đổi hiệu suất giữa các thuật toán khi thay đổi tỷ lệ huấn luyện và kiểm tra. Đây là cơ sở để tiếp tục phân tích và cải thiện mô hình dự đoán năng lượng.
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

## 10. NHẬT KÝ QUÁ TRÌNH THỰC HIỆN VÀ THỰC NGHIỆM

### Giai đoạn 1: Tìm hiểu và thu thập dữ liệu

**Ngày 23/10/2026 – Kiệt**

- Tìm hiểu đề tài Appliances Energy Prediction.

- Tìm kiếm và tải bộ dữ liệu từ UCI Machine Learning Repository.

- Kiểm tra cấu trúc và các thuộc tính của bộ dữ liệu.

**Ngày 26/10/2026 – Đại**

- Tìm hiểu mục tiêu dự đoán và các thuật toán học máy có thể áp dụng.

- Nghiên cứu các chỉ số đánh giá MAE, RMSE và R².

### Giai đoạn 2: Khám phá và tiền xử lý dữ liệu

**Ngày 29/10/2026 – Kiệt**

- Thực hiện khám phá dữ liệu (EDA).

- Kiểm tra dữ liệu thiếu, dữ liệu trùng lặp.

- Phân tích phân phối dữ liệu và mối tương quan giữa các thuộc tính.

- Xây dựng các biểu đồ trực quan hóa.

**Ngày 02/11/2026 – Kiệt**

- Phân tích các giá trị ngoại lệ.

- Thực hiện tạo đặc trưng mới như hour, day_of_week, is_weekend, lag_1 và rolling_mean.

- Xử lý dữ liệu sau khi tạo đặc trưng.

- Lưu dữ liệu đã tiền xử lý để sử dụng trong bước xây dựng mô hình.

**Ngày 05/11/2026 – Đại**

- Kiểm tra dữ liệu sau tiền xử lý.

- Tìm hiểu cách chia tập huấn luyện và kiểm tra theo thứ tự thời gian.

- Chuẩn bị dữ liệu đầu vào cho các mô hình.

### Giai đoạn 3: Xây dựng và huấn luyện mô hình

**Ngày 09/11/2026 – Đại**

- Xây dựng mô hình Baseline.

- Huấn luyện và đánh giá kết quả ban đầu.

- Sử dụng kết quả Baseline làm cơ sở so sánh.

**Ngày 12/11/2026 – Đại**

- Xây dựng và huấn luyện mô hình Linear Regression.

- Tính toán các chỉ số MAE, RMSE và R².

- Lưu kết quả thực nghiệm.

**Ngày 15/11/2026 – Đại**

- Xây dựng mô hình Ridge Regression.

- Sử dụng StandardScaler để chuẩn hóa dữ liệu trong Pipeline.

- So sánh kết quả với Linear Regression.

**Ngày 18/11/2026 – Đại**

- Xây dựng mô hình Random Forest.

- Thực hiện huấn luyện và đánh giá.

- Ghi nhận kết quả để so sánh với các mô hình trước.

**Ngày 20/11/2026 – Đại**

- Xây dựng mô hình Gradient Boosting.

- Huấn luyện và đánh giá mô hình.

- Tổng hợp kết quả của 5 mô hình.

### Giai đoạn 4: Phân tích kết quả và dự đoán

**Ngày 22/11/2026 – Kiệt và Đại**

- Tổng hợp kết quả thực nghiệm.

- So sánh các mô hình dựa trên MAE, RMSE và R².

- Nhận xét ưu điểm và hạn chế của từng mô hình.

- Thống nhất lựa chọn Linear Regression vì đạt kết quả tốt nhất trong các mô hình đã thử nghiệm.

**Ngày 24/11/2026 – Đại**

- Lưu mô hình tốt nhất thành file best_model.pkl.

- Thực hiện dự đoán trên tập dữ liệu kiểm tra.

- Xuất kết quả dự đoán ra file prediction_results.csv.

**Ngày 25/11/2026 – Kiệt**

- Kiểm tra kết quả dự đoán và các biểu đồ đánh giá.

- Kiểm tra lại quy trình sử dụng mô hình đã lưu.

- Ghi nhận và khắc phục lỗi không khớp số lượng đặc trưng đầu vào do cột date chưa được loại bỏ.

### Giai đoạn 5: Hoàn thiện dự án

**Ngày 26/11/2026 – Kiệt và Đại**

Kiểm tra lại các Notebook và những tệp kết quả.

Hoàn thiện nhật ký thực nghiệm và bảng phân công công việc.

Rà soát nội dung README và báo cáo.

**Ngày 27/11/2026 – Kiệt và Đại**

Kiểm tra tổng thể sản phẩm dự án.

Hoàn thiện tài liệu và chuẩn bị nội dung thuyết trình.

Chuẩn bị các nội dung giải thích quy trình thực hiện và kết quả mô hình.

**Tổng kết nhật ký**

Trong quá trình thực hiện đề tài, Kiệt phụ trách chính phần thu thập, khám phá và tiền xử lý dữ liệu; Đại phụ trách chính phần xây dựng, huấn luyện và đánh giá mô hình. Hai thành viên phối hợp trong quá trình phân tích kết quả, lựa chọn mô hình tốt nhất và hoàn thiện sản phẩm dự án.