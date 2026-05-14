# 🫀 Hệ thống Phân loại Nhịp tim ECG (ECG Heartbeat Classifier)

Một ứng dụng Full-stack tích hợp Machine Learning toàn diện dùng để phân loại nhịp tim thông qua điện tâm đồ (ECG). Dự án này kết hợp dữ liệu thu thập từ phần cứng (Arduino), một backend Python mạnh mẽ với nhiều mô hình Machine Learning cùng trí tuệ nhân tạo có thể giải thích được (Explainable AI - XAI), và một giao diện người dùng hiện đại được xây dựng bằng React.

## ✨ Tính năng chính

- **Phân loại Đa mô hình**: Phân loại tín hiệu ECG thành 5 nhóm (Normal - Bình thường, Supraventricular Ectopic - Ngoại tâm thu trên thất, Ventricular Ectopic - Ngoại tâm thu thất, Fusion - Nhịp hỗn hợp, Unknown - Không xác định) sử dụng các mô hình khác nhau:
  - Logistic Regression (Tự code từ đầu & dùng Scikit-learn)
  - Support Vector Classifier (SVC - Tự giải bằng thuật toán tối ưu QP & Scikit-learn)
  - Gradient Boosting Classifier
  - XGBoost
- **Xử lý Dữ liệu Nâng cao**: Xử lý tình trạng mất cân bằng dữ liệu và trích xuất đặc trưng bằng:
  - **SMOTE** (Sinh thêm dữ liệu cho nhóm thiểu số)
  - **Class Weight** (Cân bằng bằng trọng số lớp)
  - **FFT** (Fast Fourier Transform - Biến đổi Fourier nhanh) để trích xuất đặc trưng miền tần số.
- **Explainable AI (XAI)**: Hiểu và diễn giải các quyết định của mô hình thông qua biểu đồ:
  - **SHAP** (SHapley Additive exPlanations)
  - **LIME** (Local Interpretable Model-agnostic Explanations)
- **Tích hợp Phần cứng**: Scripts thu thập tín hiệu theo thời gian thực (real-time) sử dụng vi điều khiển Arduino và cảm biến điện tâm đồ AD8232.
- **Giao diện hiện đại**: Giao diện (UI) tương tác và phản hồi nhanh được xây dựng với Vite, React, và Tailwind CSS.

## 🛠️ Công nghệ sử dụng

- **Frontend**: React 19, Vite, Tailwind CSS, Shadcn UI / Radix UI, Chart.js
- **Backend**: Python 3.10, Flask, Scikit-learn, XGBoost, CVXOPT
- **Phần cứng**: Arduino, Cảm biến ECG AD8232
- **Xử lý dữ liệu & XAI**: Pandas, NumPy, SHAP, LIME

## 📂 Cấu trúc Thư mục

- `/backend/`: Chứa API máy chủ Flask (`app.py`), các file mô hình ML đã train (`.pkl`), scripts giải thích mô hình (`shap_xgboost.py`, `lime_xgboost.py`), và danh sách thư viện cài đặt.
- `/src/` & `/public/`: Mã nguồn của giao diện web frontend React.
- `/ecg/`: Mã nguồn cho Arduino (`.ino`) và các scripts Python để giao tiếp với phần cứng, đọc dữ liệu ECG qua cổng Serial và vẽ biểu đồ theo thời gian thực.
- `mitbih_train.csv`: Tập dữ liệu huấn luyện (MIT-BIH Arrhythmia Database).

## 🚀 Hướng dẫn Cài đặt & Chạy dự án

### 1. Cài đặt Backend

1. Mở terminal và di chuyển vào thư mục dự án:
   ```bash
   cd ECG-heartbeat-classifier
   ```
2. Tạo và kích hoạt môi trường ảo Python (khuyên dùng Python 3.10):
   ```bash
   python -m venv venv
   
   # Trên Windows:
   venv\Scripts\activate
   # Trên macOS/Linux:
   source venv/bin/activate
   ```
3. Di chuyển vào thư mục backend:
   ```bash
   cd backend
   ```
4. Cài đặt các thư viện yêu cầu:
   ```bash
   pip install numpy==1.26.4 scikit-learn==1.2.2 flask flask-cors joblib pandas xgboost cvxopt matplotlib
   ```
   *(Lưu ý: Nếu gặp lỗi phiên bản numpy, hãy thử cài `numpy==1.24.4`)*
5. Chạy máy chủ Flask:
   ```bash
   python app.py
   ```
   *Backend API sẽ chạy tại địa chỉ `http://localhost:5000`.*

### 2. Cài đặt Frontend

1. Mở một **cửa sổ terminal mới** và di chuyển vào thư mục gốc của dự án (`ECG-heartbeat-classifier`).
2. Cài đặt các gói thư viện Node.js:
   ```bash
   npm install
   ```
3. Chạy máy chủ phát triển (development server) của Vite:
   ```bash
   npm run dev
   ```
   *Giao diện web sẽ hiển thị tại địa chỉ `http://localhost:5173` (hoặc cổng được hiển thị trong terminal).*

### 3. Cài đặt Phần cứng (Tuỳ chọn cho Dữ liệu Thời gian thực)

Nếu bạn đang sử dụng cảm biến AD8232 để lấy dữ liệu thực tế:
1. Nạp mã code `ecg/ad8232.ino` vào mạch Arduino của bạn.
2. Chạy các scripts Python trong thư mục `ecg/` (ví dụ: `python ecg_test_realtime_flaskplot.py`) để đọc, xử lý và vẽ biểu đồ tín hiệu trực tiếp.

## 📖 Hướng dẫn Sử dụng

1. Mở giao diện web trên trình duyệt.
2. Chọn một mẫu ECG từ menu thả xuống (các mẫu này được trích xuất ngẫu nhiên từ file `mitbih_train.csv` đảm bảo có đủ 5 phân lớp nhịp tim).
3. Bấm nút **"Classify"** (Phân loại).
4. Xem kết quả dự đoán từ các mô hình học máy khác nhau.
5. Khám phá các biểu đồ **SHAP** và **LIME** để xem cụ thể các khoảng thời gian nào (timestep) hoặc đặc trưng nào của tín hiệu đã ảnh hưởng nhiều nhất đến quyết định của mô hình XGBoost.

## 📚 Tài liệu Tham khảo

- [1] Radford, A., Metz, L., & Chintala, S. (2016). *Unsupervised Representation Learning with Deep Convolutional Generative Adversarial Networks*. arXiv:1805.00794. [Link](https://arxiv.org/abs/1805.00794)

