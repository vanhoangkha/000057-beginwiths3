---
title: "Kiểm Tra Website"
date: "2025-09-06"
weight: 6
chapter: false
pre: "<b> 6. </b>"
---

### Kiểm Tra Website

Sau khi cài đặt và cấu hình thành công, bước tiếp theo là kiểm tra lại website.

1. **Truy cập vào S3 bucket đã tạo:**
    - Chọn **Object**.
    - Chọn thư mục **S3-Website-main** đã tải lên.

   ![Website](/images/6-website/0001.png?featherlight=false&width=90pc)

2. **Chọn file `index.html`:**

   ![Website](/images/6-website/0002.png?featherlight=false&width=90pc)

3. **Tìm thông tin chi tiết của `index.html`:**
    - Chọn **Object URL**.

   ![Website](/images/6-website/0003.png?featherlight=false&width=90pc)

4. **Mở URL trong tab mới của trình duyệt:**
    - Trải nghiệm giao diện website du lịch.

   ![Website](/images/6-website/0004.png?featherlight=false&width=90pc)

5. **Kiểm tra thời gian tải trang:**
    - Mục đích là nhận thấy ảnh hưởng của CloudFront trong việc giảm độ trễ và tăng tốc độ tải trang.
    - Mở giao diện website du lịch, click chuột phải và chọn **Inspect**.

   ![Website](/images/6-website/0005'.png?featherlight=false&width=90pc)

    - Ở góc trên cùng bên phải, chọn **Network**.
    - Ở góc trên cùng bên trái, chọn biểu tượng **reload**.

   ![Website](/images/6-website/0007'.png?featherlight=false&width=90pc)

    - Trong thông tin URL của Bucket website endpoint, thời gian hiển thị là 614 ms (0.614 giây). Lưu ý: giá trị này chỉ mang tính chất tương đối.

   ![Website](/images/6-website/0008.png?featherlight=false&width=90pc)
