---
title: "Bật tính năng static website"
date: "2025-09-06"
weight: 3
chapter: false
pre: "<b> 3. </b>"
---

#### Bật tính năng lưu trữ website tĩnh

#### Lưu trữ Website Tĩnh là gì?

Lưu trữ website tĩnh cho phép bạn lưu trữ một website trực tiếp từ S3 bucket. Không giống như các website động cần xử lý phía máy chủ, các website tĩnh bao gồm nội dung cố định (HTML, CSS, JavaScript, hình ảnh) được gửi trực tiếp đến trình duyệt của người dùng. S3 có thể phục vụ các tệp này một cách hiệu quả và tiết kiệm chi phí.

#### Lợi ích của S3 Static Website Hosting

- **Tiết kiệm Chi phí**: Chỉ trả tiền cho storage và data transfer
- **Có thể Mở rộng**: Tự động xử lý các đợt tăng lưu lượng
- **Đáng tin cậy**: Được xây dựng trên cơ sở hạ tầng mạnh mẽ của AWS
- **Nhanh**: Nội dung được phục vụ từ các edge location của AWS
- **Đơn giản**: Không cần quản lý máy chủ

#### Cấu hình Từng Bước

1. **Truy cập Properties của Bucket**

    Trong giao diện **S3 bucket** của bạn, chọn tab **Properties**

    {{% notice info %}}
**Những gì bạn sẽ tìm thấy:** Tab Properties chứa tất cả các tùy chọn cấu hình cho bucket của bạn, bao gồm versioning, encryption, logging và cài đặt website hosting.
{{% /notice %}}

![Static website](/images/3-staticwebsite/0001.png?featherlight=false&width=90pc)

2. **Tìm Static Website Hosting**

   Trong giao diện **Properties**:
   - Cuộn xuống để tìm phần **Static website hosting**
   - Chọn **Edit** để sửa đổi cài đặt

   {{% notice tip %}}
**Mẹo Điều hướng:** Phần Static website hosting thường nằm ở giữa trang Properties. Tìm biểu tượng quả địa cầu bên cạnh tên phần.
{{% /notice %}}

![Static website](/images/3-staticwebsite/0002.png?featherlight=false&width=90pc)

3. **Cấu hình Cài đặt Website Hosting**

    Trong cấu hình **Static website hosting**:

    - **Static website hosting**: Chọn **Enable**
    - **Hosting type**: Chọn **Host a static website**
    - **Index document**: Nhập **```index.html```**
    - **Error document** (tùy chọn): Nhập **```error.html```** nếu bạn có trang lỗi tùy chỉnh

    {{% notice info %}}
**Hiểu về Cài đặt:**
- **Index document**: Trang mặc định được phục vụ khi người dùng truy cập root website của bạn
- **Error document**: Trang tùy chỉnh hiển thị cho lỗi 4xx (404 Not Found, v.v.)
- **Redirection rules**: Quy tắc định tuyến nâng cao cho các tình huống phức tạp
{{% /notice %}}

    **Tại sao index.html?**
    - Quy ước tiêu chuẩn cho trang chủ web
    - Tự động được phục vụ khi người dùng truy cập root domain của bạn
    - Phải tồn tại trong thư mục root của bucket

![Static website](/images/3-staticwebsite/0003.png?featherlight=false&width=90pc)

4. **Lưu Cấu hình**

    Xem lại cài đặt của bạn và chọn **Save changes**

    {{% notice warning %}}
**Quan trọng**: Sau khi bật static website hosting, bucket của bạn sẽ có URL website endpoint, nhưng nội dung sẽ không thể truy cập được cho đến khi bạn:
1. Tải lên các tệp website của bạn
2. Cấu hình quyền truy cập công khai
3. Thiết lập chính sách bucket phù hợp
{{% /notice %}}

![Static website](/images/3-staticwebsite/0004.png?featherlight=false&width=90pc)

5. **Xác minh Cấu hình**

    **Static website hosting** giờ đã được bật cho bucket của bạn.

    {{% notice success %}}
**Những gì bạn đã đạt được:**
- Bucket của bạn giờ có URL website endpoint
- S3 sẽ phục vụ index.html như trang mặc định
- Bucket được cấu hình để lưu trữ nội dung tĩnh
- Bạn đã sẵn sàng tải lên các tệp website
{{% /notice %}}

    **Thông tin Quan trọng được Hiển thị:**
    - **Website endpoint**: URL nơi website của bạn sẽ có thể truy cập được
    - **Hosting type**: Xác nhận static website hosting đang hoạt động
    - **Index document**: Hiển thị trang mặc định bạn đã cấu hình

![Static website](/images/3-staticwebsite/0005.png?featherlight=false&width=90pc)

#### Hiểu về Website Endpoint

Website endpoint của bạn sẽ trông như:
```
http://bucket-name.s3-website-region.amazonaws.com
```

**Điểm Chính:**
- Sử dụng HTTP theo mặc định (HTTPS cần CloudFront)
- Định dạng endpoint cụ thể theo vùng
- Khác với REST API endpoint
- Chỉ hoạt động khi static website hosting được bật

#### Những gì Bạn Đã Hoàn thành

- ✅ Bật static website hosting trên S3 bucket của bạn
- ✅ Cấu hình index.html làm tài liệu mặc định
- ✅ Tạo URL website endpoint
- ✅ Chuẩn bị bucket để phục vụ nội dung web

#### Các Bước Tiếp theo

Giờ khi static website hosting đã được bật, bạn sẽ cần:
1. Tải lên các tệp website của bạn (HTML, CSS, JavaScript, hình ảnh)
2. Cấu hình quyền truy cập công khai
3. Kiểm tra khả năng truy cập website của bạn

#### Các Trường hợp Sử dụng Phổ biến cho S3 Static Websites

- **Portfolio cá nhân và blog**
- **Trang landing của công ty**
- **Trang tài liệu**
- **Single Page Applications (SPAs)**
- **Trang chiến dịch marketing**
- **Website sự kiện**
