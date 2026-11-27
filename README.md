# APPLIANCES ENERGY PREDICTION

## 1. Giới thiệu đề tài

**Tên đề tài:** Appliances Energy Prediction (Dự đoán mức tiêu thụ năng lượng của các thiết bị điện trong gia đình).

**Môn học:** Máy học.

**Trường:** Trường Đại học Sài Gòn.

**Nhóm:** 27.

### Mục tiêu

Xây dựng mô hình học máy nhằm dự đoán mức tiêu thụ năng lượng của các thiết bị điện trong gia đình dựa trên các thông số nhiệt độ, độ ẩm và điều kiện môi trường.

## 2. Dữ liệu sử dụng

- **Tên bộ dữ liệu:** Appliances Energy Prediction.
- **Nguồn dữ liệu:** UCI Machine Learning Repository.
- **Đường dẫn:** https://archive.ics.uci.edu/dataset/374/appliances+energy+prediction
- **Số lượng mẫu ban đầu:** 19.735 dòng.
- **Số lượng thuộc tính ban đầu:** 29 cột.
- **Biến mục tiêu:** `Appliances` (mức tiêu thụ năng lượng của thiết bị điện, đơn vị Wh).
- **Chu kỳ ghi nhận:** 10 phút/lần.

### Các nhóm dữ liệu

- Nhiệt độ và độ ẩm trong nhà.
- Nhiệt độ và độ ẩm ngoài trời.
- Các thông số thời tiết.
- Thời gian đo và mức tiêu thụ năng lượng.

## 3. Quy trình thực hiện dự án

Dự án được triển khai qua các giai đoạn sau:

### Bước 1: Khám phá dữ liệu (EDA)

- Tìm hiểu cấu trúc và đặc điểm bộ dữ liệu.
- Thống kê các thuộc tính.
- Kiểm tra dữ liệu thiếu và dữ liệu trùng lặp.
- Phân tích mối tương quan giữa các biến.
- Trực quan hóa dữ liệu bằng biểu đồ.

### Bước 2: Tiền xử lý dữ liệu

- Kiểm tra và phân tích các giá trị ngoại lệ.
- Xử lý dữ liệu phát sinh giá trị thiếu trong quá trình tạo đặc trưng.
- Chuyển đổi dữ liệu thời gian.
- Tạo thêm các đặc trưng `hour`, `day_of_week`, `is_weekend`.
- Xây dựng đặc trưng trễ `lag_1` và trung bình trượt `rolling_mean`.

### Bước 3: Xây dựng mô hình

Tiến hành huấn luyện và so sánh 5 mô hình:

1. Baseline.
2. Linear Regression.
3. Ridge Regression.
4. Random Forest.
5. Gradient Boosting.

### Bước 4: Đánh giá mô hình

Sử dụng các chỉ số đánh giá:

- **MAE:** Sai số tuyệt đối trung bình.
- **RMSE:** Căn bậc hai của sai số bình phương trung bình.
- **R² Score:** Hệ số xác định, đánh giá mức độ giải thích biến thiên của dữ liệu.

### Bước 5: Thực nghiệm bổ sung

Tiến hành so sánh hiệu suất của 5 mô hình với ba tỷ lệ chia dữ liệu theo thứ tự thời gian:

- 70/30.
- 80/20.
- 90/10.

Tổng cộng thực hiện 15 lần thực nghiệm và lưu kết quả vào `experiment_comparison.csv`.

### Bước 6: Dự đoán

- Sử dụng mô hình Linear Regression đã lựa chọn.
- Lưu mô hình thành file `best_model.pkl`.
- Thực hiện dự đoán trên tập kiểm tra.
- Xuất kết quả vào file `prediction_results.csv`.

## 4. Kết quả thực nghiệm

### 4.1. Kết quả thực nghiệm ban đầu với tỷ lệ 80/20

| Mô hình | MAE | RMSE | R² |
|---|---:|---:|---:|
| Baseline | 52.688640 | 91.053578 | -0.000331 |
| Linear Regression | 29.010182 | 62.005309 | 0.536118 |
| Ridge Regression | 29.011724 | 62.005464 | 0.536116 |
| Random Forest | 77.332475 | 114.373797 | -0.578347 |
| Gradient Boosting | 110.902914 | 144.916317 | -1.533869 |

Linear Regression cho kết quả tốt trong thực nghiệm ban đầu với tỷ lệ 80/20, đạt MAE = 29.010182, RMSE = 62.005309 và R² = 0.536118.

### 4.2. Kết quả thực nghiệm bổ sung

Nhóm tiếp tục thực nghiệm với ba tỷ lệ chia dữ liệu 70/30, 80/20 và 90/10. Kết quả cho thấy hiệu suất của các mô hình thay đổi tùy theo tỷ lệ chia dữ liệu.

Trong các lần thực nghiệm bổ sung:

- Linear Regression và Ridge có kết quả gần tương đương ở tỷ lệ 70/30 và 80/20.
- Gradient Boosting đạt R² cao nhất là 0.5577 tại tỷ lệ 90/10.
- Ridge đạt MAE thấp nhất là 27.9564 tại tỷ lệ 90/10.
- Random Forest và Gradient Boosting có R² âm tại tỷ lệ 70/30 và 80/20.

Kết quả chi tiết của 15 lần thực nghiệm được lưu trong file `reports/experiment_comparison.csv`.

### 4.3. Lựa chọn mô hình

Nhóm lựa chọn Linear Regression làm mô hình chính trong quy trình dự đoán đã xây dựng. Mặc dù Gradient Boosting đạt R² cao hơn tại tỷ lệ 90/10, Linear Regression có cấu trúc đơn giản, dễ triển khai và giải thích.

Mô hình Linear Regression đã huấn luyện được lưu thành file `best_model.pkl` để sử dụng trong bước dự đoán.

## 5. Công nghệ sử dụng

| Công nghệ | Mục đích |
|---|---|
| Python | Ngôn ngữ lập trình |
| Jupyter Notebook | Môi trường thực hiện |
| Pandas, NumPy | Xử lý dữ liệu |
| Matplotlib, Seaborn | Trực quan hóa dữ liệu |
| Scikit-learn | Xây dựng và đánh giá mô hình |
| Joblib/Pickle | Lưu trữ mô hình |
| Git, GitHub | Quản lý mã nguồn |

## 6. Cấu trúc dự án

```text
AEP_MayHoc/
│
├── Data/
│   ├── raw/
│   │   └── energydata_complete.csv
│   └── processed/
│       └── appliances_processed.csv
│
├── images/
│   ├── actual_vs_predicted.png
│   ├── appliances_boxplot.png
│   ├── appliances_distribution.png
│   ├── correlation_heatmap.png
│   ├── daily_energy.png
│   ├── energy_by_day.png
│   ├── energy_by_hour.png
│   └── residual_plot.png
│
├── models/
│   └── best_model.pkl
│
├── notebooks/
│   ├── 01_EDA_Preprocessing.ipynb
│   ├── 02_Modeling.ipynb
│   ├── 03_Prediction.ipynb
│   └── 04_Experiment_Comparison.ipynb
│
├── reports/
│   ├── Appliances_Energy_Prediction.docx
│   ├── Appliances_Energy_Prediction_Presentation.pptx
│   ├── experiment_comparison.csv
│   └── prediction_results.csv
│
├── EXPERIMENT_LOG.md
├── Phan Cong.md
├── README.md
└── requirements.txt
```

## 7. Cài đặt và sử dụng

### 7.1. Clone dự án

Mở Terminal hoặc Command Prompt và thực hiện:

```bash
git clone https://github.com/TuanKiet31082006/AEP_MayHoc.git
cd AEP_MayHoc
```

### 7.2. Cài đặt thư viện

```bash
pip install -r requirements.txt
```

### 7.3. Thực hiện dự án

Mở Jupyter Notebook và lần lượt thực hiện các tệp:

1. `01_EDA_Preprocessing.ipynb`: Khám phá và tiền xử lý dữ liệu.
2. `02_Modeling.ipynb`: Huấn luyện và đánh giá các mô hình học máy.
3. `03_Prediction.ipynb`: Tải mô hình đã lưu, thực hiện dự đoán và lưu kết quả.
4. `04_Experiment_Comparison.ipynb`: Thực nghiệm và so sánh các mô hình theo ba tỷ lệ chia dữ liệu.

**Lưu ý:** Các notebook 01, 02 và 03 cần được thực hiện theo đúng thứ tự để chuẩn bị dữ liệu và mô hình. Notebook 04 sử dụng dữ liệu đã tiền xử lý để thực hiện thực nghiệm bổ sung.

## 8. Kết luận

Dự án đã thực hiện quá trình khám phá, tiền xử lý dữ liệu, xây dựng và đánh giá các mô hình học máy nhằm dự đoán mức tiêu thụ năng lượng của các thiết bị điện trong gia đình.

Nhóm đã tiến hành so sánh năm mô hình với ba tỷ lệ chia dữ liệu khác nhau. Kết quả cho thấy hiệu suất mô hình có sự thay đổi tùy theo tỷ lệ chia dữ liệu. Linear Regression được lựa chọn làm mô hình chính trong quy trình dự đoán đã triển khai, với R² đạt 0.536118 tại tỷ lệ 80/20.

Qua đề tài, nhóm đã vận dụng được các kiến thức về xử lý dữ liệu, phân tích dữ liệu và xây dựng mô hình hồi quy vào bài toán dự đoán mức tiêu thụ năng lượng.

## 9. Thành viên thực hiện

**Đơn vị:** Trường Đại học Sài Gòn.

**Môn học:** Máy học.

**Giảng viên hướng dẫn:** Đỗ Như Tài.

**Nhóm:** 27.

| Thành viên | Nhiệm vụ |
|---|---|
| Nguyễn Tuấn Kiệt | Thu thập dữ liệu, khám phá dữ liệu, phân tích, trực quan hóa và tiền xử lý dữ liệu. |
| Dương Hùng Đại | Tìm hiểu thuật toán, xây dựng, huấn luyện, đánh giá mô hình và thực hiện dự đoán. |

Hai thành viên cùng phối hợp phân tích kết quả thực nghiệm, hoàn thiện báo cáo và chuẩn bị thuyết trình.