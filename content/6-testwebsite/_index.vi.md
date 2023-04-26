---
title : "Kiểm tra website"
date :  "`r Sys.Date()`" 
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

#### Kiểm tra website

Sau khi cài đặt và cấu hình thành công. Tiếp theo chúng ta sẽ kiểm tra lại website.

1. Truy cập vào **S3** bucket đã tạo.

    - Chọn **Object**
    - Chọn **S3-Website-main** folder đã tải lên.

![Website](/images/6-website/0001.png?featherlight=false&width=90pc)

2. Chọn **index.html**

![Website](/images/6-website/0002.png?featherlight=false&width=90pc)

3. Trong thông tin chi tiết về **index.html**, chúng ta sẽ chọn **Object URL**

![Website](/images/6-website/0003.png?featherlight=false&width=90pc)

4. Mở tab trình duyệt mới và dán **Object URL** của **index.html** vào.

   - Chúng ta trải nghiệm giao diện website về du lịch


![Website](/images/6-website/0004.png?featherlight=false&width=90pc)

5. Kiểm tra thời gian load website

- Để thấy rõ vai trò của CloudFront trong việc phân phối nội dung với độ trễ thấp và tốc độ truyền nhanh chóng, chúng ta sẽ tiến hành kiểm tra thời gian load webiste tĩnh được host trên S3 & tiến hành bước thứ 7 để thấy rõ sự khác biệt về thời gian.

- Tại giao diện website về du lịch, nhấp chuột phải và chọn **Inspect**

![Website](/images/6-website/0005'.png?featherlight=false&width=90pc)

- Phái trên cùng bên phải, chọn **Netword**
- Phía trên cùng bên trái, chọn biểu tượng **reload**

![Website](/images/6-website/0007'.png?featherlight=false&width=90pc)

- Tại mục URL của Bucket website endpoint, bạn sẽ thấy cột thời gian hiển thị giá trị là 614 ms (milliseconds)  = 0.614 giây (lưu ý: giá trị này chỉ mang tính tương đối, tùy thuộc từng thời điểm - thời gian này sẽ tăng hoặc giảm)

![Website](/images/6-website/0008.png?featherlight=false&width=90pc)
