# Báo cáo Kiểm thử Hiệu năng Trang web với JMeter

## 1. Mục tiêu bài tập
* Làm quen và sử dụng thành thạo công cụ Apache JMeter để kiểm thử hiệu năng.
* Thiết kế kịch bản kiểm thử (Thread Groups) với các tham số khác nhau nhằm đánh giá khả năng chịu tải của hệ thống.
* Phân tích các chỉ số kỹ thuật quan trọng: **Response Time (Thời gian phản hồi)**, **Throughput (Thông lượng)**, và **Error Rate (Tỉ lệ lỗi)**.

## 2. Đối tượng kiểm thử
* **Trang web:** Wikipedia Tiếng Việt (`https://vi.wikipedia.org`).
* **Công cụ:** Apache JMeter

## 3. Cấu hình kịch bản kiểm thử
Em đã thiết lập 3 nhóm người dùng (Thread Groups) với các hành vi và tham số khác nhau:

| Kịch bản | Số lượng User | Ramp-up (s) | Thời gian chạy/Lặp | Hành vi |
| :--- | :--- | :--- | :--- | :--- |
| **TG 1: Cơ bản** | 10 | 1 | 5 lần lặp | Truy cập Trang chủ |
| **TG 2: Tải nặng** | 50 | 30 | N/A | Truy cập Trang chủ và Trang giới thiệu |
| **TG 3: Tùy chỉnh** | 20 | 40 | 60 giây | Truy cập Trang Tiêu điểm và Trang Portal |

### Cấu hình bổ sung:
* **HTTP Header Manager:** Thêm thuộc tính `User-Agent` để giả lập trình duyệt Chrome để tránh lỗi 403.
* **HTTP Request Defaults:** Quản lý tập trung URL `vi.wikipedia.org` và giao thức `https`.

## 4. Phân tích kết quả
* **Tính ổn định:** Hệ thống đạt tỉ lệ lỗi tuyệt đối **0.00%**. Điều này cho thấy việc áp dụng User-Agent và Timer đã giải quyết hoàn toàn vấn đề bị máy chủ chặn truy cập ban đầu.
* **Thời gian phản hồi:** Thời gian phản hồi trung bình toàn hệ thống là **503ms**. Trang chủ phản hồi rất nhanh (358ms), trong khi Trang Portal tốn nhiều thời gian nhất (1021ms), có thể do chứa nhiều nội dung hoặc tài nguyên nặng hơn.
* **Thông lượng:** Hệ thống xử lý ổn định ở mức **2.7 yêu cầu mỗi giây** với cấu hình tải đã thiết lập.

## 5. Kết luận
Qua bài tập này, em đã nắm vững quy trình kiểm thử hiệu năng từ khâu thiết lập cấu hình đến khâu đọc và phân tích biểu đồ. Kết quả cho thấy trang web Wikipedia đáp ứng rất tốt các kịch bản tải đã đề ra.
