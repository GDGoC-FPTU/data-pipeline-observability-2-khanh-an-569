[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112802&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** annqk569@gmail.com
**Name:** Nguyễn Quang Khánh An

---

## Mo ta

Bài Lab này tập trung vào việc thiết kế và triển khai một quy trình ETL (Extract, Validate, Transform, Load) tự động bằng Python nhằm làm sạch dữ liệu trước khi cung cấp cho các AI Agent (RAG). 

Trong bài làm này, tôi đã:
1. Xây dựng hàm `extract` đọc dữ liệu đầu vào từ file JSON `raw_data.json` và xử lý ngoại lệ an toàn.
2. Xây dựng hàm `validate` lọc bỏ các bản ghi không hợp lệ (ví dụ: giá âm hoặc danh mục trống).
3. Xây dựng hàm `transform` chuẩn hóa danh mục sản phẩm thành Title Case, tính toán cột giá chiết khấu `discounted_price` (giảm 10%), và thêm nhãn thời gian xử lý `processed_at`.
4. Xây dựng hàm `load` lưu kết quả đã được làm sạch và định dạng dưới dạng tệp CSV `processed_data.csv`.
5. Đánh giá chất lượng dữ liệu thông qua bài kiểm tra Stress Test và viết báo cáo trong `experiment_report.md`.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas pytest
```

### Chay ETL Pipeline

Chạy pipeline để lấy dữ liệu từ `raw_data.json`, làm sạch và lưu ra `processed_data.csv`:
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)

1. Tạo file dữ liệu lỗi `garbage_data.csv`:
```bash
python generate_garbage.py
```
2. Chạy giả lập AI Agent trên cả hai nguồn dữ liệu sạch (`processed_data.csv`) và dữ liệu rác (`garbage_data.csv`) để kiểm chứng hành vi:
```bash
python agent_simulation.py
```

---

## Cau truc thu muc

```text
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
├── generate_garbage.py      # Script tao du lieu rac
├── agent_simulation.py      # Gia lap Agent stress test
├── tests/
│   └── test_autograder.py   # Test kiem thu tu dong
└── README.md                # Huong dan su dung nay
```

---

## Ket qua

Pipeline đã xử lý thành công file nguồn `raw_data.json` chứa 5 bản ghi ban đầu:
- **Số lượng bản ghi giữ lại (Valid):** 3 bản ghi (Laptop, Chair, Monitor).
- **Số lượng bản ghi bị loại bỏ (Dropped):** 2 bản ghi (Mystery Box bị loại do giá âm, Phone bị loại do danh mục rỗng).
- **Kết quả đầu ra:** Tệp dữ liệu sạch `processed_data.csv` đã được lưu thành công kèm theo trường thông tin chiết khấu mới và thời gian xử lý chi tiết.
