# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-XXXX
**Name:** (Dien ten cua ban)
**Date:** (Dien ngay thuc hien)

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Based on my data, the best choice is Laptop at $1200. | 10 | |
| Garbage Data (`garbage_data.csv`) | Based on my data, the best choice is Nuclear Reactor at $999999. | 10 | |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi su dung `garbage_data.csv`, agent tra ve ket qua sai la **Nuclear Reactor gia $999,999** thay vi Laptop $1,200. Nguyen nhan den tu nhieu van de chat luong du lieu ton tai dong thoi trong file garbage:

**1. Duplicate IDs (ID trung lap):**
File garbage co hai dong co `id = 1` (Laptop va Banana). Du khong truc tiep gay ra loi o bai nay, duplicate ID la dau hieu cua du lieu khong duoc kiem soat, co the dan den ket qua sai khi join hoac group by theo ID.

**2. Wrong Data Types (Sai kieu du lieu):**
Truong `price` cua "Broken Chair" co gia tri la `"ten dollars"` thay vi so. Neu agent co logic tinh toan tren gia thi se bi loi kieu du lieu. Trong truong hop nay, Pandas doc cot `price` la kieu `object` thay vi `float`, khien `idxmax()` co the cho ket qua khong chinh xac.

**3. Outliers (Gia tri ngoai le):**
"Nuclear Reactor" co gia $999,999 — mot outlier cuc lon so voi cac san pham binh thuong. Agent dung logic `idxmax()` de chon san pham co gia cao nhat trong danh muc Electronics, nen no chon Nuclear Reactor du day la mot gia tri bat thuong, khong co y nghia thuc te.

**4. Null Values (Gia tri trong):**
Dong "Ghost Item" co `id` va `category` deu bi trong (null). Neu agent co filter theo category, dong nay se bi bo qua; nhung neu khong xu ly null dung cach, no co the gay ra crash hoac ket qua sai logic.

**Ket luan nho:** Agent chay `idxmax()` tren cot `price` ma khong co buoc validate hay lam sach du lieu truoc. Chinh vi vay, du prompt hoi dung ("best electronic product"), du lieu ban khien agent tra loi sai hoan toan — chon mot san pham phi thuc te voi gia phi ly.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** (Dong y hay khong? Giai thich ngan gon.)

(Viet ket luan cua ban o day)
Toi dong y voi ket qua nay vi neu data qua ban thi prompt du dung den dau cung van se chua ra ket qua sai.
