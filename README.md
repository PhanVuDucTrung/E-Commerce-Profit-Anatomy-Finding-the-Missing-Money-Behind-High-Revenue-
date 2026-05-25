# E-Commerce Profitability Anatomy: Uncovering Profit Leaks & Sales Forecasting
**Giải pháp Tối ưu hóa Lợi nhuận và Dự báo Doanh thu Thương mại điện tử - VinUni Datathon 2026**

![Project Status](https://img.shields.io/badge/Status-Completed-success)
![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![SQL](https://img.shields.io/badge/SQL-Advanced-orange.svg)
![Power BI](https://img.shields.io/badge/Power_BI-Dashboard-yellow.svg)
![LightGBM](https://img.shields.io/badge/Model-LightGBM-brightgreen.svg)

---

## Tổng quan Dự án (Executive Summary)
Dự án này phân tích tập dữ liệu lịch sử 10 năm của một doanh nghiệp thương mại điện tử thời trang (gồm 15 bảng dữ liệu phức tạp). Vấn đề lớn nhất của doanh nghiệp là **"Nghịch lý Tăng trưởng"**: Tổng giá trị giao dịch (GMV) đạt mức rất cao nhưng Lợi nhuận ròng (Net Profit) lại bị bào mòn nghiêm trọng, biên lợi nhuận mỏng và dòng tiền bị kẹt.

**Mục tiêu của dự án:**
1. **Phân tích Chẩn đoán (Diagnostic):** Bóc tách cấu trúc chi phí, rà soát các rủi ro vận hành và tìm ra nguyên nhân gốc rễ gây thất thoát dòng tiền.
2. **Đề xuất Hành động (Prescriptive):** Xây dựng trình giả lập tài chính (What-If Simulator) để định lượng số tiền có thể thu hồi.
3. **Dự báo Doanh thu (Predictive):** Xây dựng mô hình Machine Learning dự báo doanh thu cấp độ ngày nhằm tối ưu hóa chuỗi cung ứng.

---

## Các Phát hiện Kinh doanh Nổi bật (Key Business Insights)
* **Voucher Tặc (Promo Cannibalization):** Phát hiện lỗ hổng từ tính năng cho phép cộng dồn mã giảm giá (`stackable_flag`). Tệp khách hàng này không chỉ bào mòn ngân sách khuyến mãi mà còn mang theo tỷ lệ hoàn hàng (Refund Rate) cực kỳ độc hại lên tới 28%, đẩy biên lợi nhuận của các sản phẩm chủ lực xuống mức âm.
* **Khủng hoảng Hàng tồn chết (Deadstock Burden):** Sử dụng phương pháp định chuẩn bằng phân vị (Percentile Data-driven), dự án đã khoanh vùng chính xác 813 mã sản phẩm "Tồn chết", đang đóng băng một lượng lớn vốn lưu động của công ty.
* **Lỗ hổng Vận hành (Operational Leakages):** Phân rã dòng tiền thất thoát cho thấy tỷ trọng lớn chi phí phạt Logistics ngược (x2 phí ship) đến từ các lỗi chủ quan của công ty như *giao sai kích cỡ* và *hàng lỗi*.

---

## Điểm nhấn Kỹ thuật (Technical Highlights)
* **Data Engineering & QA:** Xử lý hàng loạt các lỗi logic dữ liệu phức tạp (như khách hàng "xuyên không", lỗi hoàn tiền lố số lượng mua, lỗi sinh số ngẫu nhiên của hệ thống).
* **Data Modeling (Dual-Datamart):** Thiết kế kiến trúc 2 bảng Fact độc lập (`Profit_Datamart` và `Leakage_Datamart`) bằng SQL để triệt tiêu hoàn toàn rủi ro tính kép (Double-counting) trong hạch toán kế toán.
* **Machine Learning Pipeline:** 
  * Chuyển hóa các Insight từ EDA thành Features (Mùa vụ, Lịch sử tương tác, Tồn kho, Hành vi hoàn trả).
  * Xây dựng mô hình dự báo chuỗi thời gian (Time-series Forecasting) bằng thuật toán **LightGBM**.
  * Ứng dụng **SHAP Values** để giải thích mô hình (Explainable AI) bằng ngôn ngữ kinh doanh thay vì dùng mô hình hộp đen (Black-box).

---

## Cấu trúc Repository (Repository Structure)

Repository này được tổ chức theo luồng thực thi (Pipeline) từ khâu xử lý dữ liệu thô đến dự báo mô hình:

```text
├── dataset/             # Thư mục chứa dữ liệu đã được làm sạch (Cleaned data) & Data Dictionary
├── 01_sql/              # Scripts SQL truy vấn dữ liệu, xử lý Data QA và tạo Dual-Datamart
├── 02_eda/              # Jupyter Notebooks thực hiện Data Cleaning, EDA và file Power BI Dashboard (.pbix)
├── 03_model/            # Feature Engineering, LightGBM training pipeline, SHAP Explainability & Submission
├── report/              # Báo cáo kỹ thuật tổng kết dự án (Gồm eda_report và model_report)
└── README.md
```

## Đội ngũ thực hiện dự án
Dự án được thực hiện bởi nhóm 3 thành viên với sự phân chia vai trò rõ rệt giữa mảng Business Analytics và Data Science:
* **[Phan Vũ Đức Trung]** - Lead Data Analyst & Business insight
  * Vai trò: Phụ trách toàn bộ luồng Data Quality Assurance (Cleaning), thiết kế kiến trúc SQL Data Mart, trực quan hóa dữ liệu (Power BI/Dashboarding) và trích xuất Business Insights (Descriptive đến Prescriptive).
* **[Đặng Biên Phúc Lâm]** - Machine Learning Engineer / Data Scientist
  * Vai trò: Phụ trách trích xuất đặc trưng (Feature Engineering từ EDA), xử lý dữ liệu chuỗi thời gian, huấn luyện và tối ưu hóa siêu tham số cho mô hình dự báo, thiết lập pipeline dự báo trực tiếp (Direct Forecasting), đánh giá hiệu suất mô hình (MAE, RMSE, R²), và ứng dụng SHAP để giải thích mô hình (Model Explainability)
* **[Huỳnh Phúc Nguyên]** - Machine Learning Engineer / Data Scientist
  * Vai trò: Phụ trách trích xuất đặc trưng (Feature Engineering từ EDA), xử lý dữ liệu chuỗi thời gian, huấn luyện và tối ưu hóa siêu tham số cho mô hình dự báo, thiết lập pipeline dự báo trực tiếp (Direct Forecasting), đánh giá hiệu suất mô hình (MAE, RMSE, R²), và ứng dụng SHAP để giải thích mô hình (Model Explainability)
