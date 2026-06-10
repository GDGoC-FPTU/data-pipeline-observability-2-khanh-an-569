# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-0569
**Name:** Khanh An
**Date:** 2026-06-10

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 10 | Agent hoạt động chính xác, tìm ra sản phẩm điện tử có giá cao nhất từ dữ liệu sạch đã được chuẩn hóa. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 1 | Agent phản hồi sai do chọn phải phần tử ngoại lệ (outlier) cực đoan được gán nhãn electronics một cách vô lý. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi sử dụng dữ liệu rác (Garbage Data), AI Agent đã đưa ra câu trả lời sai lệch hoàn toàn bởi vì dữ liệu đầu vào chứa nhiều vấn đề nghiêm trọng về chất lượng chưa qua xử lý:

1. **Lỗi giá trị ngoại lệ cực đoan (Outliers):** Sự hiện diện của sản phẩm "Nuclear Reactor" với giá trị cực lớn ($999999) trong danh mục `electronics` làm lệch hoàn toàn logic lựa chọn "best deal" (sản phẩm có giá cao nhất) của Agent. Agent không có khả năng tự nhận biết một giá trị có phi thực tế hay không nếu không được thiết lập bộ lọc từ trước.
2. **Lỗi sai kiểu dữ liệu (Wrong data types):** Cột price chứa cả dữ liệu dạng chữ như "ten dollars" thay vì số thực hay số nguyên, khiến hệ thống tính toán hoặc so sánh số học gặp lỗi runtime hoặc không thể sắp xếp chính xác.
3. **Trùng lặp khóa chính (Duplicate IDs):** Việc trùng lặp khóa chính (ID 1 có cả Laptop và Banana) vi phạm tính toàn vẹn của dữ liệu và có thể dẫn đến việc Agent lấy nhầm thông tin hoặc ghi đè dữ liệu sai lệch.
4. **Dữ liệu bị thiếu hoặc rỗng (Null / Missing values):** Sản phẩm "Ghost Item" bị khuyết thiếu cả ID và Category, làm suy giảm tính nhất quán của cơ sở dữ liệu và dễ gây lỗi null pointer khi truy vấn thông tin.

Tóm lại, nếu không có một pipeline ETL làm sạch và kiểm duyệt dữ liệu, các mô hình AI Agent/RAG sẽ hoạt động không tin cậy và đưa ra thông tin hoàn toàn sai lệch cho người dùng.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** (Dong y hay khong? Giai thich ngan gon.)

Tôi hoàn toàn đồng ý với nhận định này. Cho dù chúng ta có thiết kế các prompt chi tiết, thông minh hay tối ưu đến đâu (Quality Prompt), nếu dữ liệu cung cấp cho Agent là dữ liệu sai lệch, thiếu nhất quán và chứa nhiều thông tin rác (Garbage In, Garbage Out), AI vẫn sẽ đưa ra những kết quả sai trái hoặc bị lỗi hệ thống. Dữ liệu chất lượng cao (Quality Data) là nền tảng cốt lõi quyết định tính đúng đắn và độ tin cậy của bất kỳ ứng dụng AI nào trong thực tế sản xuất.
