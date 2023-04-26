+++
title = "Block all public access"
date = 2021
weight = 1
chapter = false
pre = "<b> 7.1 </b>"
+++

1. In the **S3 bucket** interface

   - Select **Permissions**
   - Currently, we see **Block all public access** is **Off** because we turned Off in step 4
   - Select **Edit**

   ![CF](/images/cf/7.1/0001.png?featherlight=false&width=90pc)

   - Select **Block all public access**
   - Select **Save changes**

   ![CF](/images/cf/7.1/0002.png?featherlight=false&width=90pc)

   - Another window appears to confirm the **edit**, enter ``confirm``
   - Select **confirm**

   ![CF](/images/cf/7.1/0003.png?featherlight=false&width=90pc)

   - **Block all public access** has been enabled, now no public access will be able to connect to your S3 Bucket.

   ![CF](/images/cf/7.1/0004.png?featherlight=false&width=90pc)

2. Test function **Block all public access**

   - In the **S3 bucket** interface
   - Select **Properties**

![CF](/images/cf/7.1/0005.png?featherlight=false&width=90pc)

   - Scroll to the bottom of the page, at **Static website hosting**
   - Select the **square** symbol to copy the URL

![CF](/images/cf/7.1/0006.png?featherlight=false&width=90pc)

   - Press the key combination: Ctrl + Shift + N to open a new incognito browser (avoid the browser re-caching the website in step 6) & paste the copied URL above.

![CF](/images/cf/7.1/0007.png?featherlight=false&width=90pc)

-> Congratulations you have successfully **Block all public access**