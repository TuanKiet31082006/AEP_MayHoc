## 1. Giới thiệu đề tài

**Tên đề tài:** Appliances Energy Prediction (Dự đoán mức tiêu thụ năng lượng của các thiết bị điện trong gia đình).

**Môn học:** Máy học.

**Trường:** Trường Đại học Sài Gòn.

### Mục tiêu
Xây dựng mô hình học máy nhằm dự đoán mức tiêu thụ năng lượng của các thiết bị điện trong gia đình dựa trên các thông số nhiệt độ, độ ẩm và điều kiện môi trường.

## 2. Dữ liệu sử dụng

- **Tên bộ dữ liệu:** Appliances Energy Prediction.
- **Nguồn dữ liệu:** UCI Machine Learning Repository.
- **Link:** https://archive.ics.uci.edu/dataset/374/appliances+energy+prediction
- **Số lượng mẫu:** 19.735 dòng.
- **Số lượng thuộc tính:** 29 cột.
- **Biến mục tiêu:** `Appliances` (mức tiêu thụ năng lượng của thiết bị điện, đơn vị Wh).

### Các nhóm dữ liệu
- Nhiệt độ và độ ẩm trong nhà.
- Nhiệt độ và độ ẩm ngoài trời.
- Các thông số thời tiết.
- Thời gian đo và mức tiêu thụ năng lượng.

Dữ liệu được ghi nhận với chu kỳ 10 phút/lần.

## 3. Quy trình thực hiện dự án

Dự án được triển khai qua các giai đoạn sau:

### Bước 1: Khám phá dữ liệu (EDA)
- Tìm hiểu cấu trúc và đặc điểm bộ dữ liệu.
- Thống kê các thuộc tính.
- Phân tích mối tương quan giữa các biến.
- Trực quan hóa dữ liệu bằng biểu đồ.

### Bước 2: Tiền xử lý dữ liệu
- Kiểm tra dữ liệu thiếu và dữ liệu ngoại lệ.
- Xử lý và chuẩn hóa dữ liệu.
- Tạo thêm các đặc trưng như `hour`, `day_of_week`, `is_weekend`.
- Xây dựng đặc trưng trễ `lag_1` và trung bình trượt `rolling_mean`.

### Bước 3: Xây dựng mô hình
Tiến hành huấn luyện và so sánh 5 mô hình:
- Baseline.
- Linear Regression.
- Ridge Regression.
- Random Forest.
- Gradient Boosting.

### Bước 4: Đánh giá mô hình
Sử dụng các chỉ số:
- MAE (Mean Absolute Error).
- RMSE (Root Mean Squared Error).
- R² Score.

### Bước 5: Dự đoán
- Lựa chọn mô hình có kết quả tốt nhất.
- Lưu mô hình thành file `best_model.pkl`.
- Thực hiện dự đoán và lưu kết quả vào `prediction_results.csv`.

## 4. Kết quả thực nghiệm

Dự án tiến hành đánh giá 5 mô hình bằng các chỉ số MAE, RMSE và R².

| Mô hình | MAE | RMSE | R² |
|---|---:|---:|---:|
| Baseline | 52.688640 | 91.053578 | -0.000331 |
| Linear Regression | 29.010182 | 62.005309 | 0.536118 |
| Ridge Regression | 29.011724 | 62.005464 | 0.536116 |
| Random Forest | 77.332475 | 114.373797 | -0.578347 |
| Gradient Boosting | 110.902914 | 144.916317 | -1.533869 |

### Nhận xét

- Linear Regression đạt kết quả tốt nhất trong các mô hình được thử nghiệm.
- MAE đạt 29.010182.
- RMSE đạt 62.005309.
- R² đạt 0.536118.

Vì vậy, Linear Regression được lựa chọn làm mô hình dự đoán tốt nhất của dự án.

## 5. Công nghệ sử dụng

- **Ngôn ngữ lập trình:** Python.
- **Môi trường thực hiện:** Jupyter Notebook.
- **Xử lý dữ liệu:** Pandas, NumPy.
- **Trực quan hóa:** Matplotlib, Seaborn.
- **Xây dựng mô hình:** Scikit-learn.
- **Lưu trữ mô hình:** Joblib/Pickle.
- **Quản lý mã nguồn:** Git và GitHub.

## 6. Cài đặt và sử dụng

### 6.1. Clone dự án

```bash
git clone https://github.com/TuanKiet31082006/AEP_MayHoc.git
cd AEP_MayHoc
pip install -r requirements.txt

### 6.2. Thực hiện dự án

Mở Jupyter Notebook và lần lượt thực hiện các tệp sau:

1. `01_EDA_Preprocessing.ipynb`: Khám phá và tiền xử lý dữ liệu.
2. `02_Modeling.ipynb`: Huấn luyện và đánh giá các mô hình học máy.
3. `03_Prediction.ipynb`: Thực hiện dự đoán bằng mô hình tốt nhất và lưu kết quả.

**Lưu ý:** Cần thực hiện các Notebook theo đúng thứ tự để đảm bảo dữ liệu và mô hình được chuẩn bị đầy đủ.


## Phần 8. Kết luận

```markdown
## 8. Kết luận

Dự án đã thực hiện quá trình khám phá, tiền xử lý dữ liệu, xây dựng và đánh giá các mô hình học máy nhằm dự đoán mức tiêu thụ năng lượng của các thiết bị điện trong gia đình.

Thông qua quá trình thực nghiệm, Linear Regression cho kết quả tốt nhất trong 5 mô hình được thử nghiệm.

Kết quả dự án là cơ sở để tìm hiểu và ứng dụng các phương pháp học máy vào bài toán dự đoán mức tiêu thụ năng lượng.

## 9. Thành viên thực hiện

**Đơn vị:** Trường Đại học Sài Gòn.

**Môn học:** Máy học.

**Giảng viên hướng dẫn:** Đỗ Như Tài.

**Thành viên:** Nhóm 27.

- Nguyễn Tuấn Kiệt: Khám phá dữ liệu, phân tích dữ liệu và tiền xử lý dữ liệu.
- Dương Hùng Đại: Xây dựng, huấn luyện, đánh giá mô hình và thực hiện dự đoán.