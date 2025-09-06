---
title: "Tạo S3 bucket"
date: "2025-09-06"
weight: 1
chapter: false
pre: "<b> 2.1 </b>"
---

#### Tạo S3 bucket

#### S3 Bucket là gì?

S3 bucket là một container chứa các đối tượng được lưu trữ trong Amazon S3. Hãy nghĩ về nó như một thư mục cấp cao nhất chứa các tệp của bạn. Mỗi bucket có tên duy nhất trên toàn cầu và tồn tại trong một vùng AWS cụ thể. Bucket đóng vai trò là đơn vị tổ chức cơ bản trong S3 và cung cấp không gian tên cho việc lưu trữ đối tượng.

#### Hướng Dẫn Từng Bước

1. **Truy cập Dịch vụ S3**

    - Truy cập **AWS Management Console**
    - Tìm **S3** bằng thanh tìm kiếm hoặc điều hướng đến dịch vụ Storage
    - Chọn **S3**

    {{% notice tip %}}
**Mẹo Điều hướng:** Bạn cũng có thể truy cập trực tiếp S3 bằng cách gõ "S3" trong thanh tìm kiếm AWS Console để truy cập nhanh hơn.
{{% /notice %}}

![Create S3 Bucket](/images/2.1-Creates3bucket/0001.png?featherlight=false&width=90pc)

2. **Khởi tạo Tạo Bucket**

    Trong giao diện **S3**, chọn **Create bucket**

    {{% notice info %}}
**Những gì bạn sẽ thấy:** Dashboard S3 hiển thị các bucket hiện có (nếu có), mức sử dụng storage và hoạt động gần đây. Nút "Create bucket" được hiển thị nổi bật.
{{% /notice %}}

![Create S3 Bucket](/images/2.1-Creates3bucket/0002.png?featherlight=false&width=90pc)

3. **Cấu hình Cài đặt Bucket Cơ bản**

    Trong giao diện **Create bucket**:

    - **Bucket name**: Nhập **```aws-first-cloud-journey```** (hoặc thêm số nếu đã được sử dụng)
    - **AWS Region**: Chọn vùng gần nhất với người dùng của bạn hoặc theo yêu cầu
    - **Object Ownership**: Chọn **ACLs disabled (recommended)**

    {{% notice warning %}}
**Quy tắc Đặt tên Quan trọng:**
- Tên bucket phải duy nhất trên toàn cầu trong tất cả tài khoản AWS
- Phải dài 3-63 ký tự
- Chỉ có thể chứa chữ cái thường, số và dấu gạch ngang
- Không thể bắt đầu hoặc kết thúc bằng dấu gạch ngang
- Không thể chứa khoảng trắng hoặc chữ cái viết hoa
{{% /notice %}}

![Create S3 Bucket](/images/2.1-Creates3bucket/0003.png?featherlight=false&width=90pc)

    **Hiểu về Object Ownership:**
    - **ACLs disabled (khuyến nghị)**: Chủ sở hữu bucket tự động sở hữu tất cả đối tượng. Quản lý quyền đơn giản hơn.
    - **ACLs enabled**: Cho phép quyền cấp đối tượng. Phức tạp hơn nhưng cung cấp kiểm soát chi tiết.

    **Lưu ý**: Nếu tên bucket **```aws-first-cloud-journey```** đã được sử dụng, bạn sẽ thấy: "Bucket with the same name already exists." Thêm số hoặc tên viết tắt của bạn để tạo tên duy nhất (ví dụ: **```aws-first-cloud-journey-123```**).

![Create S3 Bucket](/images/2.1-Creates3bucket/0003'.png?featherlight=false&width=90pc)

4. **Cấu hình Cài đặt Truy cập Công khai**

    Đối với **Block Public Access settings for this bucket**, giữ mặc định (tất cả tùy chọn được đánh dấu).

    {{% notice info %}}
**Thực hành Bảo mật Tốt nhất:** Các cài đặt này ngăn chặn việc tiết lộ dữ liệu công khai ngoài ý muốn. Chúng ta sẽ sửa đổi chúng sau trong bài lab khi cần thiết cho việc lưu trữ website, nhưng bắt đầu với bảo mật tối đa luôn được khuyến nghị.
{{% /notice %}}

    **Chức năng của từng cài đặt:**
    - **Block all public access**: Công tắc chính cho tất cả truy cập công khai
    - **Block public access to buckets and objects granted through new ACLs**: Ngăn chặn ACL công khai mới
    - **Block public access to buckets and objects granted through any ACLs**: Chặn tất cả truy cập công khai dựa trên ACL
    - **Block public access to buckets and objects granted through new public bucket or access point policies**: Ngăn chặn chính sách bucket công khai mới
    - **Block public access to buckets and objects granted through any public bucket or access point policies**: Chặn tất cả truy cập công khai dựa trên chính sách

![Create S3 Bucket](/images/2.1-Creates3bucket/0004.png?featherlight=false&width=90pc)

5. **Tùy chọn Cấu hình Bổ sung**

    **Bucket Versioning**: Giữ tắt hiện tại (chúng ta sẽ bật sau trong bài lab)
    **Tags**: Tùy chọn - bạn có thể thêm tag để theo dõi chi phí và tổ chức
    **Default Encryption**: AWS tự động mã hóa đối tượng với SSE-S3
    **Advanced Settings**: Giữ mặc định

    Xem lại cài đặt của bạn và chọn **Create bucket**

![Create S3 Bucket](/images/2.1-Creates3bucket/0005.png?featherlight=false&width=90pc)

6. **Xác minh Tạo Bucket**

    Thành công! Bạn đã tạo **S3 bucket** để lưu trữ mã nguồn website.

    {{% notice success %}}
**Điều gì xảy ra tiếp theo:** Bucket của bạn giờ đã sẵn sàng nhận các đối tượng. Bạn có thể thấy nó được liệt kê trong S3 console với vùng bạn đã chọn và trạng thái hiện tại.
{{% /notice %}}

    **Thông tin Chính được Hiển thị:**
    - Tên bucket và ngày tạo
    - Vùng AWS nơi bucket tồn tại
    - Trạng thái truy cập (hiện tại là riêng tư)
    - Mức sử dụng storage (hiện tại là 0 đối tượng, 0 byte)

![Create S3 Bucket](/images/2.1-Creates3bucket/0006.png?featherlight=false&width=90pc)

#### Những gì Bạn Đã Hoàn thành

- ✅ Tạo một S3 bucket duy nhất trên toàn cầu
- ✅ Cấu hình cài đặt mặc định an toàn
- ✅ Chọn vùng phù hợp cho trường hợp sử dụng của bạn
- ✅ Thiết lập nền tảng cho việc lưu trữ website tĩnh

#### Các Bước Tiếp theo

Trong phần tiếp theo, chúng ta sẽ tải lên các tệp website vào bucket này và cấu hình nó cho việc lưu trữ website tĩnh.
