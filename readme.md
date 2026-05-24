# BÀI THỰC HÀNH 6: TÌM HIỂU VÀ SỬ DỤNG CÔNG CỤ GÁN NHÃN

## Thành viên nhóm
- **Phạm Đình Quang Huy** - MSSV: 24520689
- **Phạm Ngọc Minh** - MSSV: 24521082
- **Nguyễn Thị Kim Ngân** - MSSV: 24521130

## Mô tả project

Project này dùng để:

- Hợp nhất kết quả gán nhãn từ nhiều người gán nhãn (annotators).
- Phân tích độ đồng thuận bằng chỉ số Cohen’s Kappa.
- Tính toán Kappa cho từng cặp (Pairwise Kappa) và Kappa trung bình.
- Phân tích các trường hợp không đồng nhất (disagreement analysis).
- Trực quan hóa kết quả thông qua Confusion Matrix.


---

## Cấu trúc thư mục
```text
LAB5/
│
├── data/
│   ├── raw/                   # Chứa file gán nhãn thô của từng thành viên (.csv)
│   │   ├── choe.csv
│   │   ├── huy.csv
│   │   └── nganguyen.csv
│   │
│   └── processed/             # Chứa dữ liệu đã được hợp nhất
│       └── merged_annotations.csv
│
├── notebooks/                 # Quy trình xử lý dữ liệu
│   ├── 01_merge_annotations.ipynb    # Hợp nhất dữ liệu gán nhãn
│   └── 02_agreement_analysis.ipynb   # Phân tích độ đồng thuận
│
├── outputs/                   # Kết quả phân tích
│   ├── disagreement_files/    # Các file CSV lưu trường hợp không đồng nhất
│   └── confusion_matrices/    # Hình ảnh ma trận nhầm lẫn
│
├── requirements.txt           # Các thư viện cần thiết
└── README.md                  # Tài liệu hướng dẫn
```

---

# Dataset Format

Mỗi file annotator phải có format:

| id | data | label |
|---|---|---|
| 1 | example text | positive |

---

## ⚙️ Quy trình thực hiện (Workflow)

### 1. Hợp nhất nhãn (Merge Annotations)
**Notebook:** `01_merge_annotations.ipynb`
- Đọc dữ liệu từ các file CSV thô.
- Chuẩn hóa tên cột nhãn theo từng annotator.
- Hợp nhất (merge) tất cả nhãn vào một file duy nhất để phục vụ phân tích.

### 2. Phân tích độ đồng thuận (Agreement Analysis)
**Notebook:** `02_agreement_analysis.ipynb`
- **Tính toán Cohen’s Kappa:** Đo lường độ đồng thuận giữa 2 người gán nhãn, loại bỏ yếu tố ngẫu nhiên.
- **Phân tích cặp:** So sánh (Huy vs Ngân), (Huy vs Choe), (Ngân vs Choe).
- **Đánh giá:** Tính Kappa trung bình cho toàn bộ nhóm.
- **Trực quan hóa:** Vẽ Confusion Matrix để xác định các nhãn thường bị nhầm lẫn.
- **Trích xuất sai sót:** Lưu các dòng dữ liệu có sự mâu thuẫn giữa các annotators để xem xét lại guideline.

---

## Công thức tính toán

**Chỉ số Cohen’s Kappa:**
$$
\kappa = \frac{P_o - P_e}{1 - P_e}
$$
*Trong đó:*
- $P_o$: Tỷ lệ đồng thuận quan sát được (Observed Agreement).
- $P_e$: Tỷ lệ đồng thuận ngẫu nhiên (Expected Agreement).

**Kappa trung bình (Average Pairwise Kappa):**
$$
\bar{\kappa} = \frac{\kappa_{1,2} + \kappa_{1,3} + \kappa_{2,3}}{3}
$$


---

## Hướng dẫn cài đặt và chạy

### Cài đặt môi trường
```bash
pip install -r requirements.txt
```

---


### Chạy phân tích
Mở Jupyter Notebook hoặc VSCode và chạy tuần tự các file trong thư mục `notebooks/`.

---

## Ý nghĩa và Kết luận
Thông qua bài thực hành, nhóm đánh giá được:
1. **Độ tin cậy:** Mức độ đồng thuận cao $\rightarrow$ Dataset có độ tin cậy cao.
2. **Chất lượng Guideline:** Nếu nhiều trường hợp disagreement $\rightarrow$ Guideline gán nhãn chưa rõ ràng, cần điều chỉnh.
3. **Tính nhất quán:** Đảm bảo việc gán nhãn không bị cảm tính và tuân thủ quy tắc chung.