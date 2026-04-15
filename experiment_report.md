# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600030
**Name:** Đào Quang Thắng
**Date:** 2026-04-15

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "Based on my data, the best choice is Laptop at $1200." | 9 | Dung san pham, dung gia, phan hoi hop ly |
| Garbage Data (`garbage_data.csv`) | "Based on my data, the best choice is Nuclear Reactor at $999999." | 1 | Tra loi sai vi outlier cuc doan lam lech ket qua |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi su dung `garbage_data.csv`, Agent da tra loi sai tram phan tram do nhieu van de chat luong du lieu:

- **Outlier cuc doan (Extreme Outlier):** Ban ghi `Nuclear Reactor` co gia `$999,999` la mot gia tri cuc doan khong thuc te. Vi Agent su dung logic chon san pham co gia cao nhat (`idxmax()`), no bi "danh lua" boi gia tri nay va tra ve ket qua sai hoan toan. Day la vi du dien hinh cua "Garbage In, Garbage Out".

- **Duplicate IDs:** Co 2 ban ghi voi `id = 1` (Laptop va Banana). Dieu nay co the gay ra xung dot du lieu khi he thong can truy van theo ID, dan den ket qua khong nhat quan.

- **Sai kieu du lieu (Wrong Data Types):** Ban ghi `Broken Chair` co `price = 'ten dollars'` (kieu string thay vi so). Neu Agent co phep tinh so hoc, day se gay loi runtime crash.

- **Gia tri Null:** Ban ghi `Ghost Item` co `id = None` va `category = None`. Cac gia tri null nay co the gay ra ngoai le hoac tao ra cac du doan sai khi model xu ly.

Tong hop lai, du lieu "rac" khong nhung lam Agent cho ra ket qua sai ma con co nguy co lam crash toan bo he thong.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Dong y.

Du ban viet prompt tot den mau nao, neu du lieu dau vao chua outlier, null values, hay sai kieu du lieu, Agent van se cho ra ket qua sai hoac bi crash. Bai thi nghiem nay chung minh rang **chat luong du lieu la nen tang cot loi** cua bat ky he thong AI nao. Validate va lam sach du lieu truoc khi nap vao pipeline la buoc bat buoc, khong tuy chon.
