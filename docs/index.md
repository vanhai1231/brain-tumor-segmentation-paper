# Phân đoạn khối u não: Kiến trúc nào hiệu quả nhất?

<p align="center">
  <strong>Hoang-Dan Pham¹, Van-Hai Ha¹, Phuc-Dat Nguyen¹</strong><br>
  <em>¹Khoa Công nghệ thông tin, Đại học HUTECH, TP.HCM, Việt Nam</em><br>
  📧 peterdan1905@gmail.com, vanhai11203@gmail.com, phucdat231003@gmail.com
</p>

---

## 📝 Tóm tắt

Nghiên cứu này đánh giá toàn diện hiệu suất của bốn cấu hình mô hình **3D U-Net** trong bài toán phân đoạn khối u não trên ảnh MRI 3D. Chúng tôi so sánh các kiến trúc **U-Net**, **nnU-Net** và **Swin UNETR** thông qua việc thử nghiệm với các cấu hình khác nhau về độ sâu và độ rộng của mạng neural.

### 🎯 Mục tiêu
- So sánh hiệu quả các kiến trúc U-Net với cấu hình khác nhau
- Đánh giá sự đánh đổi giữa hiệu suất và chi phí tính toán
- Tìm ra cấu hình tối ưu cho phân đoạn khối u não 3D

---

## 🔬 Phương pháp nghiên cứu

### 📊 Dữ liệu
- **Dataset**: BraTS2020 (369 bệnh nhân)
- **Chia tập dữ liệu**: 
  - Huấn luyện: 250 bệnh nhân (68%)
  - Xác thực: 74 bệnh nhân (20%)
  - Kiểm tra: 45 bệnh nhân (12%)

### 🏗️ Kiến trúc mô hình
Nghiên cứu thử nghiệm **4 cấu hình 3D U-Net**:

| Cấu hình | Số lớp | Bộ lọc khởi tạo | Tham số (M) | Thời gian huấn luyện (h) |
|----------|---------|-----------------|--------------|--------------------------|
| **4L-16F** | 4 | 16 | 5.6 | 3.9 |
| **4L-32F** | 4 | 32 | 22.6 | 6.8 |
| **5L-16F** | 5 | 16 | 22.6 | 4.0 |
| **5L-32F** | 5 | 32 | 90.5 | 6.9 |

### 🎛️ Xử lý dữ liệu
- **Xung MRI sử dụng**: T1ce và T2-FLAIR
- **Kích thước patch**: 128 × 128 × 128
- **Chuẩn hóa**: Min-Max scaling [0,1]
- **Hàm mất mát**: Kết hợp Soft Dice + Categorical Cross-entropy

---

## 📈 Kết quả chính

### 🏆 Hiệu suất phân đoạn (Điểm Dice)

| Cấu hình | Toàn bộ khối u (WT) | Lõi khối u (TC) | Vùng trương phù (ET) | Trung bình |
|----------|---------------------|-----------------|---------------------|-------------|
| 4L-16F | 0.4159 | 0.3014 | 0.2632 | **0.3268** |
| 4L-32F | 0.4270 | 0.3106 | 0.2778 | **0.3385** |
| 5L-16F | 0.4218 | 0.2878 | 0.2529 | **0.3208** |
| **5L-32F** | **0.4873** | **0.3667** | **0.3121** | **🥇 0.3887** |

### 📊 So sánh hiệu quả tính toán

<div align="center">

```
Cải thiện hiệu suất vs Chi phí tính toán:

4L-16F → 4L-32F: +3.6% hiệu suất, +74% thời gian
4L-16F → 5L-16F: +1.8% hiệu suất, +2.6% thời gian  
4L-16F → 5L-32F: +18.9% hiệu suất, +77% thời gian
```

</div>

---

## 🔍 Phân tích chi tiết

### ✅ Phát hiện chính
1. **Cấu hình 5L-32F** đạt hiệu suất cao nhất nhưng yêu cầu tài nguyên lớn
2. **Độ rộng bộ lọc** quan trọng hơn **độ sâu mạng** trong cải thiện hiệu suất
3. **Cấu hình 4L-32F** cân bằng tốt giữa hiệu suất và chi phí tính toán
4. **Cấu hình 5L-16F** hiệu quả về thời gian nhưng hiệu suất hạn chế

### 📉 Phân tích định lượng
- Việc tăng bộ lọc từ 16→32: **cải thiện 3.6%** hiệu suất
- Việc tăng độ sâu từ 4→5 lớp: **cải thiện 1.8%** hiệu suất
- **Khoảng cách Hausdorff**: 5L-32F (5mm) vs 4L-16F (8mm)

---

## 🎯 Kết luận

### 🏅 Khuyến nghị sử dụng

| Tình huống | Cấu hình đề xuất | Lý do |
|------------|------------------|-------|
| **Hiệu suất tối đa** | 5L-32F | Điểm Dice cao nhất (0.3887) |
| **Cân bằng thực tế** | 4L-32F | Hiệu suất tốt với chi phí hợp lý |
| **Tài nguyên hạn chế** | 4L-16F | Nhẹ nhất, nhanh nhất |
| **Hiệu quả thời gian** | 5L-16F | Thời gian huấn luyện thấp |

### 🔮 Hướng phát triển
- Tối ưu hóa chi phí tính toán (model pruning, quantization)
- Cải thiện khả năng khái quát hóa với dữ liệu đa nguồn
- Tích hợp cơ chế attention cho vùng nhỏ và khó
- Ứng dụng các kiến trúc tiên tiến (Transformer-based)

---

## 📚 Tài liệu tham khảo chính

- Ronneberger, O., Fischer, P., & Brox, T. (2015). U-Net: Convolutional Networks for Biomedical Image Segmentation
- Menze, B. H., et al. (2015). The Multimodal Brain Tumor Image Segmentation Benchmark (BRATS)
- Isensee, F., et al. (2018). nnU-Net: Self-adapting Framework for U-Net-Based Medical Image Segmentation

---

<div align="center">
  <strong>🧠 Nghiên cứu góp phần phát triển AI trong y tế, hỗ trợ chẩn đoán và điều trị khối u não chính xác hơn</strong>
</div>
