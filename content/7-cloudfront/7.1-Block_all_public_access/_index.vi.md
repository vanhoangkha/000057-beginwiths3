---
title : "Chặn tất cả truy cập công cộng vào S3"
date: 2024-01-01
weight : 1 
chapter : false
pre : " <b> 7.1 </b> "
---

1. Trong giao diện **S3 bucket**

   - Chọn **Permissions**
   - Hiện tại, chức năng **Block all public access** đang **Off** do chúng ta đã bật tắt tại bước 4
   - Chọn **Edit**

   ![CF](/images/cf/7.1/0001.png?featherlight=false&width=90pc)

   - Chọn **Block all public access**
   - Chọn **Save changes**

   ![CF](/images/cf/7.1/0002.png?featherlight=false&width=90pc)

   - Một cửa số khác xuất hiện để xác nhận việc **edit**, điền ``confirm``
   - Chọn **confirm**

   ![CF](/images/cf/7.1/0003.png?featherlight=false&width=90pc)

   - **Block all public access** đã được bật, lúc này sẽ không có bất kỳ một truy cập công cộng nào có thể kết nối được với S3 Bucket của bạn.

   ![CF](/images/cf/7.1/0004.png?featherlight=false&width=90pc)

2. Kiểm tra chức năng  **Block all public access**

   - Trong giao diện **S3 bucket**
   - Chọn **Properties**

![CF](/images/cf/7.1/0005.png?featherlight=false&width=90pc)

   - Cuộn xuống cuối trang, tại mục **Static website hosting**
   - Chọn ký hiệu **ô vuông** để copy URL

![CF](/images/cf/7.1/0006.png?featherlight=false&width=90pc)  

   - Nhấn tổ hợp phím: Ctrl + Shift + N để mở trình duyệt ẩn danh mới (để tránh việc: trình duyệt cache lại trang web trong bước 6) & dán URL đã copy ở trên. 

![CF](/images/cf/7.1/0007.png?featherlight=false&width=90pc)  

-> Chúc mứng bạn đã **Block all public access** thành công






