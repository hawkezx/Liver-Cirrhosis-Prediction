# 🩺 Dự Án Dự Đoán Giai Đoạn Xơ Gan (Liver Cirrhosis Stage Prediction)

## 📋 Tổng Quan Dự Án

Dự án này sử dụng Machine Learning để dự đoán giai đoạn bệnh xơ gan (Stage 1, 2, 3) dựa trên các chỉ số y tế và triệu chứng lâm sàng của bệnh nhân. Đây là một bài toán phân loại đa lớp (multi-class classification) với mục tiêu hỗ trợ chẩn đoán y tế.

## 📁 Cấu Trúc Thư Mục

```

├── 📊 Report.pdf              # Báo cáo chi tiết dự án
├── 🎯 Slide.pdf              # Bài thuyết trình
└── 💻 Code/
    ├── 📓 Code_Final.ipynb    # Notebook chính chứa toàn bộ code
    └── 🗂️ data/
        └── 📦 data.zip        # Dữ liệu gốc (liver_cirrhosis.csv)

```
        
## 🔬 Dataset

- **📄 File dữ liệu**: `liver_cirrhosis.csv` (nén trong `data.zip`)
- **📊 Kích thước**: 25,000 mẫu dữ liệu
- **🧬 Đặc trưng**: 19 features bao gồm:
  - 👤 **Thông tin cá nhân**: Age, Sex
  - 🩸 **Chỉ số xét nghiệm**: Bilirubin, Cholesterol, Albumin, Copper, Alk_Phos, SGOT, Tryglicerides, Platelets, Prothrombin
  - 🏥 **Triệu chứng lâm sàng**: Ascites, Hepatomegaly, Spiders, Edema
  - 💊 **Thông tin điều trị**: Status, Drug, N_Days
- **🎯 Biến mục tiêu**: Stage (1, 2, 3)

## 🔄 Quy Trình Thực Hiện

### 1. 🧹 Tiền Xử Lý Dữ Liệu
- **⏰ Chuyển đổi đơn vị**: Age từ ngày sang năm
- **🔄 Xử lý dữ liệu phân loại**: 
  - Binary encoding cho Sex, Drug, Ascites, Hepatomegaly, Spiders
  - One-hot encoding cho Edema, Status
- **📈 Xử lý outliers**: Sử dụng phương pháp IQR cho các biến số
- **⚖️ Chuẩn hóa**: StandardScaler cho toàn bộ dữ liệu

### 2. 📊 Phân Tích và Trực Quan Hóa
- **🔍 PCA (Principal Component Analysis)**: Giảm chiều dữ liệu
- **📐 LDA (Linear Discriminant Analysis)**: Phân tích khả năng phân biệt
- **📈 Visualization**: Boxplot, histogram, scatter plot theo giai đoạn bệnh

### 3. 🎯 Phân Cụm (Clustering)
- **🔵 K-Means Clustering**: Tìm cấu trúc tiềm ẩn trong dữ liệu
- **📊 Đánh giá**: Silhouette Score, Entropy analysis
- **✅ Kết quả**: K=6 cụm tối ưu

### 4. 🤖 Phân Loại (Classification)

#### 🛠️ Các Thuật Toán Được Áp Dụng:
1. **🏠 K-Nearest Neighbors (KNN)**
   - Tham số tối ưu: k=7, weights='distance', metric='manhattan'
2. **🧠 Multi-Layer Perceptron (MLP)**
   - Hidden layers: (100,), activation='relu', solver='adam'
3. **⚡ Support Vector Machine (SVM)**
   - Linear SVM, RBF Kernel, Polynomial Kernel, Sigmoid Kernel

#### 📊 Tỷ Lệ Chia Dữ Liệu:
- 🟢 Train:Test = 8:2 (80%-20%)
- 🟡 Train:Test = 7:3 (70%-30%)  
- 🔴 Train:Test = 6:4 (60%-40%)

### 5. 📈 Hồi Quy (Regression)
- 🔄 Chuyển đổi bài toán phân loại thành hồi quy
- 🎯 Sử dụng xác suất dự đoán của MLP cho Stage 3
- 🤖 Thuật toán: Linear Regression, Random Forest Regressor

## 🚀 Cách Chạy Dự Án

### 💻 Yêu Cầu Hệ Thống
```bash
🐍 Python 3.7+
📓 Jupyter Notebook hoặc Google Colab
```

### 📚 Thư Viện Cần Thiết
```python
numpy
pandas
matplotlib
seaborn
scikit-learn
scipy
```

### ⚙️ Cài Đặt Dependencies
```bash
pip install numpy pandas matplotlib seaborn scikit-learn scipy
```

### ☁️ Chạy Trên Google Colab (Khuyến nghị)
1. 📤 Upload thư mục `Project-ML-main` lên Google Drive
2. 📂 Mở [Code_Final.ipynb](Code/Code_Final.ipynb) trong Google Colab
3. ▶️ Chạy từng cell theo thứ tự từ trên xuống dưới

### 💾 Chạy Trên Máy Local
1. 📦 Giải nén file `data.zip` trong thư mục `data/`
2. 🖥️ Mở terminal/cmd và chạy:
```bash
jupyter notebook Code_Final.ipynb
```
3. 🔧 Sửa đường dẫn file dữ liệu trong notebook:
```python
# Thay đổi từ:
base_dir = 'liver_cirrhosis.csv'
# Thành:
base_dir = 'data/liver_cirrhosis.csv'
```
4. ▶️ Chạy từng cell theo thứ tự

## 🏆 Kết Quả Chính

### 📊 Hiệu Suất Mô Hình (Test Accuracy)
- **🏠 KNN**: ~85-90% accuracy
- **🧠 MLP**: ~88-92% accuracy  
- **⚡ SVM**: ~90-95% accuracy (RBF Kernel thường tốt nhất)

### 💡 Insights Từ Dữ liệu
- 🚨 Bệnh nhân Stage 3 có xu hướng:
  - 👴 Tuổi cao hơn (46-61 tuổi)
  - 📈 Mức Bilirubin và Prothrombin cao
  - ⚠️ Có triệu chứng Ascites, Spiders, Edema
  - 📉 Số lượng Platelets và Albumin thấp

## 📝 Cấu Trúc Code

### 🔧 Các Section Chính:
1. **📥 Data Loading & Preprocessing** (Section 2.1)
2. **📊 Data Analysis & Visualization** (Section 2.2)  
3. **🎯 Clustering Analysis** (Section 2.3)
4. **🤖 Classification Models** (Section 2.4a)
5. **📈 Regression Analysis** (Section 2.4c)

### ⚙️ Functions Quan Trọng:
- `handle_outliers_custom()`: 🧹 Xử lý outliers
- `plot_distributions()`: 📊 Vẽ phân phối dữ liệu
- `run_KNN()`, `run_MLP()`: 🚀 Chạy các mô hình phân loại
- `run_gridsearch_knn()`: 🎯 Tối ưu tham số KNN

## 📖 Tài Liệu Tham Khảo

- 📊 [Report.pdf](Report.pdf): Báo cáo chi tiết về phương pháp và kết quả
- 🎯 [Slide.pdf](Slide.pdf): Bài thuyết trình tổng kết dự án
