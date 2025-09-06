---
title : "Configuring public access block"
date : "2025-09-06"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

{{% notice warning %}}
**AWS Security Best Practice Warning:** AWS strongly recommends keeping Block Public Access enabled. This tutorial disables it for learning purposes, but in production environments, you should use CloudFront with Origin Access Control (OAC) instead of making S3 buckets publicly accessible. See [AWS Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html) for secure alternatives.
{{% /notice %}}

#### Configure public access block

To be able to access the hosted website we will reconfigure **Block Public Access**

1. In the **S3 bucket** interface

- Select **Permissions**
- Currently, we see **Block all public access** is **On**

![Block Public Access](/images/4-Blockpublicaccess/0001.png?featherlight=false&width=90pc)

2. In the **Block public access** interface

- Uncheck **Block all public access**
- Select **Save changes**

![Block Public Access](/images/4-Blockpublicaccess/0002.png?featherlight=false&width=90pc)

3. Confirm **confirm** and select **Confirm**

![Block Public Access](/images/4-Blockpublicaccess/0003.png?featherlight=false&width=90pc)

4. Complete **Block public access** configuration

![Block Public Access](/images/4-Blockpublicaccess/0004.png?featherlight=false&width=90pc)