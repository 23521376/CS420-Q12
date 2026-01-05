# CS420-Q12  
**Phân loại nhóm tuổi từ ảnh khuôn mặt**

## 1. Giới thiệu
Repository này chứa mã nguồn và kết quả thực nghiệm cho **Câu 12 (Q12)** của học phần **CS420**.  
Mục tiêu của đề tài là **phân loại nhóm tuổi từ ảnh khuôn mặt**, dựa trên hai hướng tiếp cận chính:

- Phương pháp phân loại ảnh truyền thống với đặc trưng thủ công  
- Phương pháp học sâu sử dụng **học chuyển giao (Transfer Learning)**  

Toàn bộ thí nghiệm được thực hiện trên **tập dữ liệu UTKFace**.

---

## 2. Tập dữ liệu
- **Tên tập dữ liệu:** UTKFace  
- **Số lượng ảnh:** 23.625 ảnh (19.742 ảnh sau khi lọc)  
- **Định dạng:** JPEG  
- **Độ phân giải:** 200 × 200  
- **Khoảng tuổi:** 1–116  

### Phân chia nhóm tuổi
| Nhóm | Khoảng tuổi |
|------|-------------|
| 1 | 1–12 (Trẻ em) |
| 2 | 13–19 (Thiếu niên) |
| 3 | 20–39 (Thanh niên) |
| 4 | 40–59 (Trung niên) |
| 5 | 60+ (Người cao tuổi) |

Tập dữ liệu được chia theo tỷ lệ **80% huấn luyện – 10% kiểm định – 10% kiểm thử**, sử dụng phương pháp **stratified split**.

---

## 3. Phương pháp

### 3.1. Phân loại ảnh truyền thống
**Quy trình thực hiện:**
1. Chuyển ảnh sang ảnh xám  
2. Chuẩn hóa kích thước về 48 × 48  
3. Trích xuất đặc trưng  
4. Giảm chiều dữ liệu bằng PCA (giữ 95% phương sai)  
5. Huấn luyện mô hình phân loại  

**Các đặc trưng sử dụng:**
- Histogram of Oriented Gradients (HOG)  
- Local Binary Patterns (LBP)  
- Histogram cường độ xám  

**Các mô hình phân loại:**
- Linear Support Vector Machine (Linear SVM)  
- K-Nearest Neighbors (KNN)  
- Decision Tree  

---

### 3.2. Học chuyển giao (Transfer Learning)
Các mô hình học sâu được khởi tạo bằng trọng số huấn luyện trước trên **ImageNet** và được tinh chỉnh cho bài toán phân loại 5 nhóm tuổi.

**Các mô hình được sử dụng:**
- EfficientNet-B0  
- EfficientNet-B3  
- ResNet-18  
- ResNet-34  
- Vision Transformer (ViT-B/16)  

**Cấu hình huấn luyện chung:**
- Batch size: 64  
- Hàm mất mát: Cross-Entropy Loss  
- Bộ tối ưu: Adam  
- Scheduler: ReduceLROnPlateau  
- Early stopping  

---

## 4. Độ đo đánh giá
Các mô hình được đánh giá bằng những độ đo phổ biến trong bài toán phân loại nhiều lớp:

- Accuracy  
- Precision, Recall, F1-score theo từng lớp  
- Macro Recall (Balanced Accuracy)  
- Macro F1-score  
- Ma trận nhầm lẫn (Confusion Matrix)  

---

## 5. Kết quả thực nghiệm

### Phương pháp truyền thống
| Mô hình | Accuracy | Macro F1 |
|--------|----------|----------|
| Linear SVM | 0.66 | 0.51 |
| KNN | 0.62 | 0.48 |
| Decision Tree | 0.54 | 0.38 |

### Phương pháp học chuyển giao
| Mô hình | Accuracy | Macro F1 |
|--------|----------|----------|
| EfficientNet-B0 | 0.80 | 0.74 |
| EfficientNet-B3 | **0.80** | **0.75** |
| ResNet-18 | 0.78 | 0.72 |
| ResNet-34 | 0.78 | 0.73 |
| ViT-B/16 | 0.76 | 0.69 |

Kết quả cho thấy các mô hình học chuyển giao vượt trội hơn rõ rệt so với phương pháp truyền thống, đặc biệt trong việc cải thiện hiệu năng trên các lớp dữ liệu thiểu số.

---

## 6. Cấu trúc thư mục
```text
CS420-Q12/
├── data/                # Dữ liệu và tập chia
├── features/            # Đặc trưng trích xuất
├── models/              # Mô hình đã huấn luyện
├── notebooks/           # Thực nghiệm và phân tích
├── scripts/             # Script huấn luyện và đánh giá
├── results/             # Kết quả và confusion matrix
└── README.md
