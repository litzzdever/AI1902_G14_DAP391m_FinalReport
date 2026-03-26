# AI1902_G14_DAP391m_FinalReport
# 🏦 German Credit Risk Scoring Application
### Project 20 — DAP Final Project

---

## 📁 Cấu Trúc Thư Mục

```
DAP_PRroject_Final/
│
├── 📄 README.md                          ← File này
│
├── 📁 Data/
│   ├── german.data                       ← Dữ liệu gốc (categorical codes)
│   ├── german.data-numeric               ← Dữ liệu đã mã hóa số
│   ├── german.doc                        ← Mô tả dataset gốc
│   └── Index                             ← Index file
│
├── 📓 2. Data Analysis.ipynb             ← Mục 2: EDA
├── 📓 3. Advanced Visualization.ipynb    ← Mục 3: Visualization nâng cao
├── 📓 4. Chatbot.ipynb                   ← Mục 4: Chatbot AI
├── 📓 5. Model Training.ipynb            ← Mục 5: Xây dựng & đánh giá model
│
└── 📄 MUC1_BUSINESS_UNDERSTANDING.txt   ← Mục 1: Business Understanding
```

---

## ⚙️ Yêu Cầu Hệ Thống

| Yêu cầu | Phiên bản tối thiểu |
|---------|-------------------|
| Python  | 3.8+              |
| VS Code | Bất kỳ            |
| Jupyter Extension (VS Code) | Bất kỳ |

---

## 📦 Cài Đặt Thư Viện

Mở **Terminal** trong VS Code (`Ctrl + `` ` ``) và chạy:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn ipywidgets
```

Kiểm tra cài đặt thành công:

```bash
python -c "import pandas, numpy, matplotlib, seaborn, sklearn, ipywidgets; print('OK')"
```

> **Lưu ý:** Nếu dùng Anaconda, thay `pip` bằng `conda install`.

---

## 🚀 Hướng Dẫn Chạy Từng Notebook

### ✅ Bước chung (áp dụng cho tất cả notebooks)

1. Mở VS Code
2. Mở thư mục `DAP_PRroject_Final` (`File → Open Folder`)
3. Mở file `.ipynb` muốn chạy
4. Chọn **kernel**: nhấn góc trên bên phải → chọn `Python 3`
5. Nhấn **Run All** hoặc chạy từng cell bằng `Shift + Enter`

> **Quan trọng:** Notebook tự động tìm file `german.data` trong thư mục `Data/`.
> Nếu báo lỗi không tìm thấy, sửa dòng sau trong cell đầu tiên:
> ```python
> DATA_PATH = r'C:\DAP_PRroject_Final\Data\german.data'
> ```

---

## 📋 Mục 1 — Business Understanding

**File:** `MUC1_BUSINESS_UNDERSTANDING.txt`

File text thuần, mở bằng bất kỳ trình soạn thảo nào (Notepad, VS Code).

**Nội dung:**
- Tổng quan bài toán phân loại Good/Bad Credit
- Mô tả 20 features của German Credit Dataset
- Thống kê cơ bản từ dữ liệu thực tế
- Cost Matrix và ý nghĩa kinh doanh
- Pipeline tiền xử lý dữ liệu
- Các mô hình dự kiến và tiêu chí đánh giá

---

## 📊 Mục 2 — Data Analysis (EDA)

**File:** `2. Data Analysis.ipynb`

**Các bước thực hiện:**

| Bước | Nội dung | Output |
|------|----------|--------|
| 1 | Cấu hình & tìm đường dẫn tự động | — |
| 2 | Import thư viện | — |
| 3 | Load dữ liệu & tổng quan | Bảng thống kê |
| 4 | Kiểm tra Class Imbalance | `class_distribution.png` |
| 5 | Default Rate theo Purpose | `default_by_purpose.png` |
| 6 | Default Rate theo Duration, Amount, Age | `default_by_duration_amount_age.png` |
| 7 | Default Rate theo Savings & Checking | `default_by_savings_checking.png` |
| 8 | Phân phối Numeric Features | `numeric_distributions.png` |
| 9 | Correlation Heatmap | `correlation_heatmap.png` |
| 10 | Default Rate theo Employment & History | `default_by_employment_history.png` |
| 11 | Key Insights & Tóm tắt | In ra console |

**Key Insights quan trọng:**
- 🔴 Vay > 36 tháng: default rate **47.9%** (gấp 3× so với < 12 tháng)
- 🔴 Số tiền > 10K DM: default rate **60%**
- 🔴 Tài khoản âm (< 0 DM): default rate cao nhất ~**50%+**
- 🟢 Tiết kiệm > 1000 DM: default rate chỉ **12.5%**

---

## 📉 Mục 3 — Advanced Visualization

**File:** `3. Advanced Visualization.ipynb`

**Các bước thực hiện:**

| Bước | Nội dung | Output |
|------|----------|--------|
| 1–2 | Cấu hình, import | — |
| 3 | Load & tiền xử lý (One-Hot + StandardScaler) | — |
| 4 | Train Logistic Regression & SVM | AUC scores |
| 5 | ROC Curve | `roc_curve.png` |
| 6 | Precision-Recall Curve | `pr_curve.png` |
| 7 | Confusion Matrix theo 5 threshold | `confusion_by_threshold.png` |
| 8 | Bảng metrics theo threshold | DataFrame |
| 9 | Expected Cost Curve | `cost_curve.png` |
| 10 | Dashboard tổng hợp | `visualization_dashboard.png` |
| 11 | Tóm tắt & kết luận | In ra console |

**Kết quả chính:**

```
Logistic Regression  ROC-AUC : 0.779
SVM (RBF)            ROC-AUC : 0.761
Optimal Threshold (LR)       : ~0.37–0.40
```

> **Lý do không dùng threshold 0.5:** Cost matrix 5:1 → cần giảm FN (Bad→Good)
> bằng cách hạ threshold → tăng Recall cho lớp Bad.

---

## 🤖 Mục 4 — Chatbot

**File:** `4. Chatbot.ipynb`

**Các bước thực hiện:**

| Bước | Nội dung |
|------|----------|
| 1–2 | Cấu hình, import |
| 3 | Load & train model (Logistic Regression) |
| 4 | Knowledge base (8 chủ đề) + Scoring engine |
| 5 | Scoring engine: chấm điểm từng khách hàng |
| 6 | **Chatbot UI tương tác** (ipywidgets) |
| 7 | Demo chấm điểm 3 khách hàng mẫu |
| 8 | Interactive Scoring Widget (sliders + dropdowns) |

**Chatbot trả lời được về:**

| Từ khoá | Nội dung |
|---------|----------|
| `threshold` | Bảng so sánh threshold theo risk appetite |
| `drivers` | Top 8 risk drivers + impact score |
| `improve` | 7 bước cải thiện điểm tín dụng |
| `model` | Bảng so sánh Baseline vs LR vs SVM |
| `dataset` | Thông tin German Credit Dataset |
| `checking` | Phân tích Checking Account |
| `duration` | Thời hạn vay vs Default Rate |
| `savings` | Tiết kiệm vs Default Rate |

**Cách dùng Chatbot UI:**
1. Chạy cell **Bước 6**
2. Gõ câu hỏi vào ô text → nhấn **Gửi** hoặc `Enter`
3. Hoặc nhấn các nút **Quick Questions** bên dưới

**Cách dùng Interactive Scoring (Bước 8):**
1. Kéo các slider / chọn dropdown để nhập thông tin khách hàng
2. Kết quả cập nhật **tự động** theo thời gian thực
3. Kéo slider **Threshold** để thay đổi ngưỡng phân loại

> **Lưu ý:** Cần cài `ipywidgets`. Nếu chưa cài, notebook tự chuyển sang
> chế độ text đơn giản (Fallback mode).

---

## 🧠 Mục 5 — Model Training & Evaluation

**File:** `5. Model Training.ipynb`

**Các bước thực hiện:**

| Bước | Nội dung | Output |
|------|----------|--------|
| 1–2 | Cấu hình, import | — |
| 3 | Load & tiền xử lý | Shape info |
| 4 | Train 3 models | AUC scores |
| 5 | Tìm Optimal Threshold | Threshold + Cost |
| 6 | Đánh giá toàn diện | Bảng so sánh |
| 7 | Cross Validation 5-fold | Mean ± Std |
| 8 | Classification Report chi tiết | Per-class metrics |
| 9 | Visualization tổng hợp | `model_comparison.png` |
| 10 | Feature Importance (coefficients) | `feature_importance.png` |
| 11 | Threshold Analysis | `threshold_analysis.png` |
| 12 | Tóm tắt & Kết luận | In ra console |

**Kết quả đầy đủ:**

```
Model                 Acc     AUC     PR-AUC  F1-Bad  Cost
─────────────────────────────────────────────────────────────
Majority Baseline     70.0%   0.500   0.300   0.000    450
Logistic Reg ⭐       74.5%   0.779   0.621   0.588    198
SVM (RBF)             72.0%   0.761   0.598   0.560    221
```

**Kết luận:** Logistic Regression thắng toàn diện — AUC cao nhất,
Expected Cost thấp nhất, và giải thích được qua coefficients.

---

## ❗ Xử Lý Lỗi Thường Gặp

### Lỗi 1: `NameError: name '__file__' is not defined`
**Nguyên nhân:** Chạy code `.py` trong Jupyter (biến `__file__` không tồn tại trong notebook).

**Cách sửa:** Tất cả notebook đã được sửa — dùng `find_data_path()` thay thế.
Nếu vẫn lỗi, sửa thủ công dòng `DATA_PATH` trong cell đầu tiên:
```python
DATA_PATH = r'C:\DAP_PRroject_Final\Data\german.data'
```

---

### Lỗi 2: `FileNotFoundError: german.data not found`
**Nguyên nhân:** Notebook không tìm thấy thư mục `Data/`.

**Cách sửa:** Kiểm tra cấu trúc thư mục:
```
DAP_PRroject_Final/
    Data/
        german.data        ← Phải có file này
    2. Data Analysis.ipynb
    ...
```
Sau đó sửa `DATA_PATH` trong cell đầu tiên của notebook.

---

### Lỗi 3: `ModuleNotFoundError: No module named 'sklearn'`
**Cách sửa:**
```bash
pip install scikit-learn
```

---

### Lỗi 4: `ModuleNotFoundError: No module named 'ipywidgets'`
**Cách sửa:**
```bash
pip install ipywidgets
```
Notebook **4. Chatbot.ipynb** sẽ tự chuyển sang text mode nếu thiếu thư viện này — vẫn chạy được bình thường.

---

### Lỗi 5: Kernel chết giữa chừng khi train SVM
**Nguyên nhân:** SVM tốn nhiều RAM với dataset lớn.

**Cách sửa:** Giảm dataset hoặc thêm tham số:
```python
svm = SVC(kernel='rbf', C=0.5, cache_size=500, ...)
```

---

## 📊 Tóm Tắt Kết Quả Dự Án

| Hạng mục | Giá trị |
|----------|---------|
| Dataset | German Credit (1,000 mẫu, 20 features) |
| Tỷ lệ Good/Bad | 70% / 30% |
| Model tốt nhất | Logistic Regression |
| ROC-AUC | **0.779** |
| Optimal Threshold | **0.38** (theo cost matrix 5:1) |
| Expected Cost (optimal) | **198** (vs Baseline: 450) |
| Cost saving | **56%** so với Majority Baseline |

---

## 👤 Thông Tin Dự Án

| Thông tin | Chi tiết |
|-----------|----------|
| Dự án | Project 20 — German Credit Risk Scoring |
| Dataset | UCI ML Repository — German Credit Data |
| Nguồn data | Prof. Dr. Hans Hofmann, Universität Hamburg |
| Ngôn ngữ | Python 3.8+ |
| Framework | scikit-learn, pandas, matplotlib, seaborn |

---

*README này được tạo cho DAP Final Project — German Credit Risk Scoring Application.*
