---
title : "Config Amazon CloudFront"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 7.2 </b> "
---

Use the AWS management console, to create a **CloudFront distribution** and configure this service to serve the **S3 Bucket** we created earlier.

1. Open the Amazon CloudFront console at https://console.aws.amazon.com/cloudfront/home.
2. From the dashboard, click **Create a CloudFront distribution**.

  ![CF](/images/cf/7.2/0001.png?featherlight=false&width=90pc)

3. Specify the following settings for the distribution:

- In the **Origin domain** field, select the S3 bucket you created earlier.
- In the **Origin access** field, select **Legacy access identities**

  ![CF](/images/cf/7.2/0002.png?featherlight=false&width=90pc)
 
- Select **Create new OAI** -> keep the value **name** & select **Create** with OAI as Origin access identity

  ![CF](/images/cf/7.2/0003.png?featherlight=false&width=90pc)

  - In the **Bucket policy** field, select **Yes, update the bucket policy** to let AWS auto update the permission to let CloudFront access into the S3 bucket

  ![CF](/images/cf/7.2/0004.png?featherlight=false&width=90pc)

  - Scroll down near the bottom of the page:
     - In the **Web Application Firewall (WAF)** section & in this lab, select **Do not enable security protections**
     - In the **Settings** section,
         - We will choose **Use North America, Europe, Asia, Middle East, and Africa**!
         - In the **Default root object - optional** section, enter ``index.html`` which is the object you uploaded in step 2.2 (Loading data)

     - Keep the default values, select **Create distribution**

  ![CF](/images/cf/7.2/0005.png?featherlight=false&width=90pc)
 
  **Note**: In case, your actual customer is globally, you should select **Use all edge locations (best performance)** to deliver at [450+ Points of Presence(PoP),400+ Edge Locations](https://aws.amazon.com/about-aws/global-infrastructure/#:~:text=The%20AWS%20Cloud%20in%20North,two%20Regional%20Edge%20Cache%20locations.). 

4. Information **CloudFront**

- After completing item 3 above, AWS will automatically redirect you to CloudFront information page as shown below, with status as **Deploying**

![CF](/images/cf/7.2/0006.png?featherlight=false&width=90pc)

**Note**: please wait for this status for a few minutes - depending on the number of edge locations you chose to deploy in item 3. In the meantime, you can open another tab to return to the S3 bucket & see what values cloudfront has added to the bucket policy.

- In the S3 bucket interface, select Permissions

![CF](/images/cf/7.2/0007.png?featherlight=false&width=90pc)

- In the **Bucket policy** section, you review the important content

![CF](/images/cf/7.2/0008.png?featherlight=false&width=90pc)