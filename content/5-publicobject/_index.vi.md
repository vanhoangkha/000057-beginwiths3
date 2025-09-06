---
title: "Cấu hình public object"
date: "2025-09-06"
weight: 5
chapter: false
pre: "<b> 5. </b>"
---

#### Cấu hình truy cập đối tượng công khai

{{% notice warning %}}
**Cảnh báo Bảo mật**: Làm cho các đối tượng công khai có nghĩa là bất kỳ ai trên internet đều có thể truy cập chúng. Chỉ làm điều này cho nội dung bạn dự định công khai, chẳng hạn như các tệp website. Không bao giờ làm công khai dữ liệu nhạy cảm.
{{% /notice %}}

#### Hiểu về Mô hình Quyền S3 Object

Trước khi làm công khai các đối tượng, điều quan trọng là hiểu mô hình quyền của S3:

- **Quyền cấp bucket**: Kiểm soát truy cập vào chính bucket
- **Quyền cấp đối tượng**: Kiểm soát truy cập vào từng đối tượng riêng lẻ
- **ACLs (Access Control Lists)**: Hệ thống quyền cũ, vẫn được hỗ trợ
- **Bucket policies**: Chính sách dựa trên JSON cho kiểm soát chi tiết
- **IAM policies**: Quyền dựa trên người dùng và vai trò

#### Cấu hình Từng Bước

1. **Truy cập Quyền Bucket**

   Trong giao diện S3 bucket của bạn, chọn tab **Permissions**

   {{% notice info %}}
**Những gì bạn sẽ thấy**: Tab Permissions chứa tất cả cài đặt liên quan đến bảo mật bao gồm Block public access, Bucket policy, Access control list (ACL), và cấu hình CORS.
{{% /notice %}}

![Public Object](/images/5-publicobject/0001.png?featherlight=false&width=90pc)

2. **Tìm Cài đặt Access Control List**

   Cuộn xuống để tìm phần **Access control list (ACL)**
   - Bạn sẽ thấy **Bucket owner enforced** hiện đang được chọn
   - Điều này có nghĩa là ACL bị tắt và chủ sở hữu bucket kiểm soát tất cả đối tượng

   {{% notice tip %}}
**Trạng thái Hiện tại**: Với "Bucket owner enforced", bạn không thể sử dụng ACL để làm công khai các đối tượng. Chúng ta cần bật ACL trước.
{{% /notice %}}

![Public Object](/images/5-publicobject/0002.png?featherlight=false&width=90pc)

3. **Bật ACL cho Kiểm soát Cấp Đối tượng**

    Chọn **Edit** trong phần Object Ownership, sau đó cấu hình:

    - **Object ownership**: Chọn **ACLs enabled**
    - **Acknowledgment**: Đánh dấu **I acknowledge that ACLs will be restored**
    - **Object ownership setting**: Chọn **Bucket owner preferred**
    - Chọn **Save changes**

    {{% notice info %}}
**Hiểu về Tùy chọn Object Ownership:**
- **Bucket owner enforced**: Tắt ACL, chủ sở hữu bucket sở hữu tất cả đối tượng
- **Bucket owner preferred**: Chủ sở hữu bucket sở hữu các đối tượng được tải lên với ACL bucket-owner-full-control
- **Object writer**: Tài khoản tải lên đối tượng sở hữu nó
{{% /notice %}}

    **Tại sao "Bucket owner preferred"?**
    - Duy trì bảo mật trong khi cho phép tính linh hoạt của ACL
    - Đảm bảo bạn giữ quyền kiểm soát các đối tượng trong bucket của mình
    - Ngăn chặn mất quyền sở hữu đối tượng ngoài ý muốn

![Public Object](/images/5-publicobject/0003.png?featherlight=false&width=90pc)

4. **Xác minh Cấu hình ACL**

    Sau khi lưu, bạn sẽ thấy **ACLs enabled** trong phần Object Ownership.

    {{% notice success %}}
**Cấu hình Đã Cập nhật**: Bucket của bạn giờ hỗ trợ ACL, cho phép bạn thiết lập quyền cấp đối tượng bao gồm truy cập công khai.
{{% /notice %}}

![Public Object](/images/5-publicobject/0004.png?featherlight=false&width=90pc)

5. **Làm Công khai Đối tượng Sử dụng ACL**

   Điều hướng trở lại tab **Objects** của bucket:
   - Chọn các đối tượng hoặc thư mục bạn muốn làm công khai
   - Chọn **Actions** từ thanh công cụ
   - Chọn **Make public using ACL**

   {{% notice warning %}}
**Cách tiếp cận Có chọn lọc**: Chỉ chọn các đối tượng cần có thể truy cập công khai. Thông thường, điều này bao gồm các tệp HTML, CSS, JavaScript và hình ảnh cho website của bạn.
{{% /notice %}}

   **Hành động này làm gì:**
   - Thêm ACL public-read vào các đối tượng được chọn
   - Cho phép người dùng internet ẩn danh tải xuống các đối tượng này
   - Cho phép website của bạn tải đúng cách trong trình duyệt

![Public Object](/images/5-publicobject/0005.png?featherlight=false&width=90pc)

6. **Xác nhận Truy cập Công khai**

   Trên trang xác nhận **Make public**:
   - Xem lại các đối tượng sẽ được làm công khai
   - Hiểu rằng các đối tượng này sẽ có thể truy cập được bởi bất kỳ ai
   - Chọn **Make public** để xác nhận

   {{% notice danger %}}
**Cảnh báo Cuối cùng**: Khi bạn nhấp "Make public", các đối tượng này sẽ ngay lập tức có thể truy cập được bởi bất kỳ ai trên internet biết URL.
{{% /notice %}}

![Public Object](/images/5-publicobject/0006.png?featherlight=false&width=90pc)

7. **Xác minh Cấu hình Công khai**

    Thành công! Các đối tượng của bạn giờ có thể truy cập công khai.

    {{% notice success %}}
**Những gì bạn đã đạt được:**
- Các đối tượng giờ có quyền public-read
- Các tệp website của bạn có thể được truy cập bởi trình duyệt web
- Static website hosting sẽ hoạt động đúng cách
- Các đối tượng hiển thị trạng thái "Public" trong S3 console
{{% /notice %}}

    **Chỉ báo Trực quan:**
    - Các đối tượng sẽ hiển thị badge "Public" trong S3 console
    - Cột permissions sẽ chỉ ra truy cập công khai
    - Bạn giờ có thể kiểm tra website endpoint của mình

![Public Object](/images/5-publicobject/0007.png?featherlight=false&width=90pc)

#### Phương pháp Thay thế cho Truy cập Công khai

Trong khi bài lab này sử dụng ACL, có các cách khác để làm công khai đối tượng S3:

**1. Phương pháp Bucket Policy:**
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

**2. CloudFront Distribution (Khuyến nghị cho Production):**
- Giữ S3 bucket riêng tư
- Sử dụng Origin Access Control (OAC)
- Cung cấp HTTPS và CDN toàn cầu
- Bảo mật và hiệu suất tốt hơn

#### Thực hành Bảo mật Tốt nhất

- **Nguyên tắc Quyền Tối thiểu**: Chỉ làm công khai các đối tượng cần thiết
- **Kiểm tra Định kỳ**: Thường xuyên xem lại các đối tượng công khai
- **CloudTrail Logging**: Giám sát truy cập vào các đối tượng công khai
- **Bucket Notifications**: Nhận cảnh báo khi đối tượng được làm công khai
- **Sử dụng CloudFront**: Cho các website production, sử dụng CloudFront thay vì truy cập S3 công khai trực tiếp

#### Những gì Bạn Đã Hoàn thành

- ✅ Bật ACL trên S3 bucket của bạn
- ✅ Cấu hình cài đặt object ownership phù hợp
- ✅ Làm cho các đối tượng website có thể truy cập công khai
- ✅ Chuẩn bị bucket của bạn cho static website hosting

#### Các Bước Tiếp theo

Giờ khi các đối tượng của bạn đã công khai, bạn có thể:
1. Kiểm tra website của bạn sử dụng S3 website endpoint
2. Xác minh tất cả tài nguyên tải đúng cách
3. Cân nhắc triển khai CloudFront để có hiệu suất và bảo mật tốt hơn
