[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23572333&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** daothang28032003@gmail.com
**Name:** Đào Quang Thắng
**Student ID**: AI20K-2A202600030
---

## Mo ta

Bai lab ngay 10 xay dung mot ETL Pipeline tu dong bang Python de xu ly du lieu san pham tu file JSON. Pipeline thuc hien 4 buoc: Extract (doc du lieu), Validate (loai bo record khong hop le), Transform (tinh gia giam va chuan hoa category), va Load (luu ra CSV). Ngoai ra, bai lab con thuc hien Stress Test de so sanh hieu qua cua Agent khi su dung du lieu sach va du lieu "rac", tu do chung minh tam quan trong cua Data Quality.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
# Buoc 1: Tao du lieu rac
python generate_garbage.py

# Buoc 2: Chay Agent voi ca 2 bo du lieu (clean va garbage)
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

- **Tong so records trong raw_data.json:** 5
- **Records hop le (valid):** 3 (Laptop, Chair, Monitor)
- **Records bi loai (dropped):** 2
  - ID=3 (Mystery Box): Gia am (-10)
  - ID=4 (Phone): Category rong
- **Output file:** `processed_data.csv` voi cac cot `id`, `product`, `price`, `category`, `discounted_price`, `processed_at`
- **Stress Test:** Agent voi Clean Data cho ra ket qua chinh xac (Laptop $1200). Agent voi Garbage Data bi lech boi outlier (Nuclear Reactor $999,999).