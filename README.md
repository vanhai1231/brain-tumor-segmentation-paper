# Brain Tumor Segmentation: Which Architecture Is Most Effective?

[![Paper](https://img.shields.io/badge/Paper-Vietnamese-blue.svg)](https://github.com/user/repo)
[![Institution](https://img.shields.io/badge/Institution-HUTECH-orange.svg)](https://www.hutech.edu.vn/)
[![Dataset](https://img.shields.io/badge/Dataset-BraTS2020-green.svg)](https://www.med.upenn.edu/cbica/brats2020/)
[![Framework](https://img.shields.io/badge/Framework-3D%20U--Net-red.svg)](https://github.com/user/repo)
[![Modalities](https://img.shields.io/badge/MRI-T1ce%20%7C%20T2--FLAIR-purple.svg)](https://github.com/user/repo)

> **Phân đoạn khối u não: Kiến trúc nào hiệu quả nhất?**  
> *Nghiên cứu so sánh hiệu quả giữa các kiến trúc U-Net, nnU-Net và Swin UNETR trong việc phân đoạn khối u não thông qua ảnh 3D MRI*

## 📝 Tóm tắt

Nghiên cứu này đánh giá toàn diện hiệu suất của bốn cấu hình mô hình **3D U-Net** trong bài toán phân đoạn khối u não trên ảnh MRI 3D. Chúng tôi so sánh các kiến trúc khác nhau về độ sâu (số lượng lớp) và độ rộng (số lượng bộ lọc) để tìm ra cấu hình tối ưu cho việc phân đoạn các vùng khối u não.

## 👥 Tác giả

- **Hoang-Dan Pham** - *Khoa Công nghệ thông tin, Đại học HUTECH*
- **Van-Hai Ha** - *Khoa Công nghệ thông tin, Đại học HUTECH*  
- **Phuc-Dat Nguyen** - *Khoa Công nghệ thông tin, Đại học HUTECH*

## 🎯 Mục tiêu nghiên cứu

- So sánh hiệu quả của các cấu hình U-Net khác nhau (4L-16F, 4L-32F, 5L-16F, 5L-32F)
- Đánh giá tác động của độ sâu và độ rộng mạng đến hiệu suất phân đoạn
- Phân tích sự đánh đổi giữa độ chính xác và chi phí tính toán

## 🔧 Cấu hình thử nghiệm

| Cấu hình | Số lớp | Số bộ lọc ban đầu | Số tham số (M) | Thời gian huấn luyện (h) |
|-----------|--------|-------------------|----------------|---------------------------|
| **4L-16F** | 4 | 16 | 5.6 | 3.9 |
| **4L-32F** | 4 | 32 | 22.6 | 6.8 |
| **5L-16F** | 5 | 16 | 22.6 | 4.0 |
| **5L-32F** | 5 | 32 | 90.5 | 6.9 |

## 📊 Kết quả chính

### Điểm Dice trung bình trên tập kiểm tra

| Cấu hình | Toàn bộ khối u (WT) | Lõi khối u (TC) | Vùng trương phù (ET) |
|-----------|---------------------|-----------------|---------------------|
| **4L-16F** | 0.4159 | 0.3014 | 0.2632 |
| **4L-32F** | 0.4270 | 0.3106 | 0.2778 |
| **5L-16F** | 0.4218 | 0.2878 | 0.2529 |
| **5L-32F** | **0.4873** | **0.3667** | **0.3121** |

### 🏆 Kết quả nổi bật

- **Cấu hình tốt nhất**: 5L-32F với điểm Dice trung bình cao nhất (0.3887)
- **Cấu hình hiệu quả**: 4L-32F cân bằng tốt giữa hiệu suất và chi phí tính toán
- **Tác động độ rộng**: Tăng số bộ lọc từ 16 → 32 cải thiện 3.6% hiệu suất
- **Tác động độ sâu**: Thêm 1 lớp chỉ cải thiện 1.8% hiệu suất

## 🔬 Dữ liệu và phương pháp

### Dataset
- **BraTS2020**: 369 bệnh nhân
- **Phân chia**: Training (250) | Validation (74) | Test (45)
- **Modalities**: T1ce và T2-FLAIR
- **Kích thước**: 240×240×155 voxels

### Kiến trúc mô hình
- **Kiến trúc**: 3D U-Net với cấu trúc encoder-decoder
- **Kích thước patch**: 128×128×128×2
- **Hàm mất mát**: Kết hợp Soft Dice + Categorical Cross-entropy (α=0.5)
- **Chuẩn hóa**: Min-Max normalization [0,1]

## 📈 Phân tích chi tiết

### Hiệu quả tính toán
- Thời gian huấn luyện không tăng tuyến tính theo số tham số
- 5L-16F hiệu quả hơn 4L-32F về thời gian (4.0h vs 6.8h) với cùng số tham số
- 5L-32F đạt hiệu suất cao nhất nhưng yêu cầu tài nguyên lớn nhất

### Khuyến nghị sử dụng
- **Tài nguyên hạn chế**: 4L-16F (nhẹ nhất, 5.6M tham số)
- **Cân bằng hiệu suất-chi phí**: 4L-32F (hiệu quả thực tiễn)
- **Ưu tiên độ chính xác**: 5L-32F (hiệu suất cao nhất)

## 🛠️ Công nghệ sử dụng

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat&logo=tensorflow&logoColor=white)
![GPU](https://img.shields.io/badge/GPU-P100-76B900?style=flat&logo=nvidia&logoColor=white)
![Kaggle](https://img.shields.io/badge/Kaggle-20BEFF?style=flat&logo=kaggle&logoColor=white)

## 📚 Trích dẫn

```bibtex
@article{pham2024brain,
  title={Phân đoạn khối u não: Kiến trúc nào hiệu quả nhất?},
  author={Pham, Hoang-Dan and Ha, Van-Hai and Nguyen, Phuc-Dat},
  journal={Khoa Công nghệ thông tin, Đại học HUTECH},
  year={2024},
  address={TP.HCM, Việt Nam}
}
```

## 🔗 Liên hệ

- **Email**: peterdan1905@gmail.com, vanhai11203@gmail.com, phucdat231003@gmail.com
- **Tổ chức**: Khoa Công nghệ thông tin, Đại học HUTECH, TP.HCM

---

<div align="center">
  <img src="https://img.shields.io/badge/Made%20with-❤️-red.svg"/>
  <img src="https://img.shields.io/badge/For-Medical%20AI-blue.svg"/>
</div>
