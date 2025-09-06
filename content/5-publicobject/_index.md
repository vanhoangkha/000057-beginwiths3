---
title : "Configuring public objects"
date : "2025-09-06"
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

#### Configure public object access

{{% notice warning %}}
**Security Warning**: Making objects public means anyone on the internet can access them. Only do this for content you intend to be publicly accessible, such as website files. Never make sensitive data public.
{{% /notice %}}

#### Understanding S3 Object Permissions

Before making objects public, it's important to understand S3's permission model:

- **Bucket-level permissions**: Control access to the bucket itself
- **Object-level permissions**: Control access to individual objects
- **ACLs (Access Control Lists)**: Legacy permission system, still supported
- **Bucket policies**: JSON-based policies for fine-grained control
- **IAM policies**: User and role-based permissions

#### Step-by-Step Configuration

1. **Access Bucket Permissions**

   In your S3 bucket interface, select the **Permissions** tab

   {{% notice info %}}
**What you'll see**: The Permissions tab contains all security-related settings including Block public access, Bucket policy, Access control list (ACL), and CORS configuration.
{{% /notice %}}

![Public Object](/images/5-publicobject/0001.png?featherlight=false&width=90pc)

2. **Locate Access Control List Settings**

   Scroll down to find the **Access control list (ACL)** section
   - You'll see **Bucket owner enforced** is currently selected
   - This means ACLs are disabled and the bucket owner controls all objects

   {{% notice tip %}}
**Current State**: With "Bucket owner enforced", you cannot use ACLs to make objects public. We need to enable ACLs first.
{{% /notice %}}

![Public Object](/images/5-publicobject/0002.png?featherlight=false&width=90pc)

3. **Enable ACLs for Object-Level Control**

    Select **Edit** in the Object Ownership section, then configure:

    - **Object ownership**: Select **ACLs enabled**
    - **Acknowledgment**: Check **I acknowledge that ACLs will be restored**
    - **Object ownership setting**: Select **Bucket owner preferred**
    - Select **Save changes**

    {{% notice info %}}
**Understanding Object Ownership Options:**
- **Bucket owner enforced**: Disables ACLs, bucket owner owns all objects
- **Bucket owner preferred**: Bucket owner owns objects uploaded with bucket-owner-full-control ACL
- **Object writer**: The account that uploads an object owns it
{{% /notice %}}

    **Why "Bucket owner preferred"?**
    - Maintains security while allowing ACL flexibility
    - Ensures you retain control over objects in your bucket
    - Prevents accidental loss of object ownership

![Public Object](/images/5-publicobject/0003.png?featherlight=false&width=90pc)

4. **Verify ACL Configuration**

    After saving, you should see **ACLs enabled** in the Object Ownership section.

    {{% notice success %}}
**Configuration Updated**: Your bucket now supports ACLs, allowing you to set object-level permissions including public access.
{{% /notice %}}

![Public Object](/images/5-publicobject/0004.png?featherlight=false&width=90pc)

5. **Make Objects Public Using ACLs**

   Navigate back to your bucket's **Objects** tab:
   - Select the objects or folders you want to make public
   - Select **Actions** from the toolbar
   - Choose **Make public using ACL**

   {{% notice warning %}}
**Selective Approach**: Only select the objects that need to be publicly accessible. Typically, this includes HTML, CSS, JavaScript, and image files for your website.
{{% /notice %}}

   **What this action does:**
   - Adds a public-read ACL to selected objects
   - Allows anonymous internet users to download these objects
   - Enables your website to load properly in browsers

![Public Object](/images/5-publicobject/0005.png?featherlight=false&width=90pc)

6. **Confirm Public Access**

   On the **Make public** confirmation page:
   - Review the objects that will be made public
   - Understand that these objects will be accessible to anyone
   - Select **Make public** to confirm

   {{% notice danger %}}
**Final Warning**: Once you click "Make public", these objects will be immediately accessible to anyone on the internet who knows the URL.
{{% /notice %}}

![Public Object](/images/5-publicobject/0006.png?featherlight=false&width=90pc)

7. **Verify Public Configuration**

    Success! Your objects are now publicly accessible.

    {{% notice success %}}
**What you've achieved:**
- Objects now have public-read permissions
- Your website files can be accessed by web browsers
- The static website hosting will work properly
- Objects show "Public" status in the S3 console
{{% /notice %}}

    **Visual Indicators:**
    - Objects will show "Public" badge in the S3 console
    - The permissions column will indicate public access
    - You can now test your website endpoint

![Public Object](/images/5-publicobject/0007.png?featherlight=false&width=90pc)

#### Alternative Methods for Public Access

While this lab uses ACLs, there are other ways to make S3 objects public:

**1. Bucket Policy Method:**
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

**2. CloudFront Distribution (Recommended for Production):**
- Keeps S3 bucket private
- Uses Origin Access Control (OAC)
- Provides HTTPS and global CDN
- Better security and performance

#### Security Best Practices

- **Principle of Least Privilege**: Only make necessary objects public
- **Regular Audits**: Periodically review public objects
- **CloudTrail Logging**: Monitor access to public objects
- **Bucket Notifications**: Get alerts when objects are made public
- **Use CloudFront**: For production websites, use CloudFront instead of direct S3 public access

#### What You've Accomplished

- ✅ Enabled ACLs on your S3 bucket
- ✅ Configured appropriate object ownership settings
- ✅ Made website objects publicly accessible
- ✅ Prepared your bucket for static website hosting

#### Next Steps

Now that your objects are public, you can:
1. Test your website using the S3 website endpoint
2. Verify all resources load correctly
3. Consider implementing CloudFront for better performance and security
