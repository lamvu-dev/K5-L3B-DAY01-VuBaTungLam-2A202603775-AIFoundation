# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV:*2A202603775*
- **Họ và tên:*Vũ Bá Tùng Lâm*
- **SEED** (in ở ô đầu notebook): 6915

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | CÓ |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | CÓ |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | CÓ |

## 2. Kết quả chính

                                 precision  recall  F1 (test)  F1 (SUB 40)  \
1. BoW + LogReg (tự code)            1.000   0.804      0.891        0.947   
2. BoW + MLP (deep learning)         0.978   0.928      0.952        0.974   
3a. Encoder (MiniLM) + kNN           0.882   0.928      0.905        0.947   
3b. Encoder (MiniLM) + LogReg        0.947   0.928      0.937        0.947   
3c. Encoder (MiniLM) + MLP head      0.949   0.969      0.959        0.974   
4a. LLM nhỏ zero-shot                0.952   1.000      0.976        0.976   

                                 train (s)  tin/s (cả lô)  p50 ms/tin  \
1. BoW + LogReg (tự code)            6.046      44636.473       0.044   
2. BoW + MLP (deep learning)         4.192      50367.281       0.218   
3a. Encoder (MiniLM) + kNN           3.037        120.501      17.764   
3b. Encoder (MiniLM) + LogReg        3.425       1612.133       6.901   
3c. Encoder (MiniLM) + MLP head      4.124       1821.901       6.854   
4a. LLM nhỏ zero-shot                0.000          1.335     661.120   

                                 p95 ms/tin  USD / 1k tin  
1. BoW + LogReg (tự code)             0.057         0.000  
2. BoW + MLP (deep learning)          0.261         0.000  
3a. Encoder (MiniLM) + kNN           22.665         0.000  
3b. Encoder (MiniLM) + LogReg         8.061         0.000  
3c. Encoder (MiniLM) + MLP head       7.898         0.000  
4a. LLM nhỏ zero-shot              1146.170         0.027  
• Hàng LLM chỉ đo trên SUB (40 tin) → so sánh chất lượng công bằng bằng cột 'F1 (SUB 40)'.
• SUB chỉ 40 tin: 1 tin sai đổi F1 vài điểm. Chênh < ~0.05 F1 coi như HOÀ — đừng xếp hạng theo số lẻ.
• Inference đo TỪ VĂN BẢN THÔ → NHÃN (gồm cả vectorize / encode). p50/p95 = gọi từng tin một, như một request thật.
• train (s) của 3a/3b/3c = thời gian encoder MiniLM encode tập train (+ train đầu LogReg / MLP); LLM = 0 vì không train. Số đo phụ thuộc CPU/GPU của Colab.

## 3. Dự đoán và thực tế

*Chọn 3 dự đoán `predict(...)` lệch nhiều nhất so với kết quả. Mỗi cái: bạn đoán gì, ra gì, vì sao lệch.*

## 4. Phân tích 50 case khó

*Model nào tụt nhiều nhất, ở nhóm case nào? Nêu 2 case cụ thể và cơ chế khiến model sai.*

## 5. Thử thách cá nhân

Chưa có

## 6. Phương án cho sản phẩm thật

Trên đường Pareto: ['1. BoW + LogReg (tự code)', '2. BoW + MLP (deep learning)', '4a. LLM nhỏ zero-shot']
Đạt SLA p95 < 50 ms: ['1. BoW + LogReg (tự code)', '2. BoW + MLP (deep learning)', '3a. Encoder (MiniLM) + kNN', '3b. Encoder (MiniLM) + LogReg', '3c. Encoder (MiniLM) + MLP head']

## 7. AI log và điều đã học

*Mỗi lần dùng AI: hỏi gì, nhận gì, bạn sửa gì. Sau đó 2–3 câu: điều bạn hiểu ra hôm nay mà trước đó chưa hiểu.*
