# LAB5 — Inter-Annotator Agreement Analysis

## Mô tả project

Project này dùng để:

- Merge annotation results từ nhiều annotators
- Phân tích độ đồng thuận (Inter-Annotator Agreement)
- Tính Pairwise Cohen’s Kappa
- Phân tích disagreement cases
- Visualization confusion matrix

---

# Cấu trúc project

```text
LAB5/
│
├── data/
│   ├── raw/
│   │   ├── choe.csv
│   │   ├── huy.csv
│   │   └── nganguyen.csv
│   │
│   └── processed/
│       └── merged_annotations.csv
│
├── notebooks/
│   ├── 01_merge_annotations.ipynb
│   └── 02_agreement_analysis.ipynb
│
├── outputs/
│   ├── disagreement files
│   └── confusion matrix images
│
├── src/
│
├── README.md
└── requirements.txt
```

---

# Dataset Format

Mỗi file annotator phải có format:

| id | data | label |
|---|---|---|
| 1 | example text | positive |

---

# Workflow

## 1. Merge annotations

Notebook:
```text
01_merge_annotations.ipynb
```

Chức năng:
- Read CSV files
- Rename label columns
- Merge annotators
- Save merged dataset

---

## 2. Agreement Analysis

Notebook:
```text
02_agreement_analysis.ipynb
```

Chức năng:
- Pairwise Cohen’s Kappa
- Manual Kappa calculation
- sklearn verification
- Disagreement analysis
- Confusion matrix visualization

---

# Pairwise Annotator Comparison

Project tính agreement cho:

- huy vs ngan
- huy vs choe
- ngan vs choe

---

# Cohen’s Kappa Formula

$$
\kappa = \frac{P_o - P_e}{1 - P_e}
$$

Trong đó:

- $P_o$: Observed Agreement
- $P_e$: Expected Agreement

---

# Average Pairwise Kappa

$$
\bar{\kappa} =
\frac{
\kappa_1 + \kappa_2 + \kappa_3
}{3}
$$

---

# Cài đặt môi trường

```bash
pip install -r requirements.txt
```

---

# Chạy notebook

Mở Jupyter Notebook hoặc VSCode:

```bash
jupyter notebook
```

---

# Outputs

Project sẽ sinh ra:

- merged_annotations.csv
- disagreement CSV files
- confusion matrix images

---

# Ý nghĩa project

Project giúp đánh giá:
- độ đồng thuận giữa annotators
- chất lượng guideline labeling
- độ tin cậy của dataset
- consistency trong sentiment annotation