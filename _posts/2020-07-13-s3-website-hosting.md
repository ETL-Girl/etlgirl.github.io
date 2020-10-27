---
layout: post
title: Host a Static Website on Amazon S3 Within 5 Minutes
date: 2020-07-13 00:00:00 +0100
description: # Add post description (optional)
img:  2020-07-13-main-pic.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [S3, AWS]
---

Amazon S3 can be used to host a static website. For hosting dynamic websites, other AWS services can be used.

To configure an S3 bucket for a static website hosting, the AWS Management Console (their web UI) can be used, without a need to write any code. To do so, we first need to configure the bucket and then upload our website content.

# Create a new bucket with public access
To create a new bucket, open the AWS Management Console and go to the S3 service. On the left-hand side choose a section named **Buckets**. Once in the section, click on the **Create bucket** button. Give your new bucket a name. This name has to be unique across the whole global AWS infrastructure. Choose the bucket region, for now it will preferably be the closest region to where you are located. Click on **Next**. 

<img src="\assets\img\2020-07-13-s3-website\Screenshot 2020-10-27 at 14.45.09.png" width="100%"/>


For now, we do not need any additional settings in the **Configure options** tab, click on **Next**. In the **Set permissions** tab, we have the option of blocking all public access enabled by default. In order for our website to be accessible from the Internet, we need to allow that access. Untick the option. 

<img src="\assets\img\2020-07-13-s3-website\Screenshot 2020-10-27 at 14.50.49.png" width="100%"/>

You will see a warning, but as you can see it strictly relates to our use case:

_AWS recommends that you block all public access to your bucket, unless public access is required for specific and verified use cases such as static website hosting._

To proceed, you have to tick the acknowledgment box.

<img src="\assets\img\2020-07-13-s3-website\Screenshot 2020-10-27 at 14.50.58.png" width="100%"/>

Click on **Next** and then **Create bucket**.

# Create a policy for the bucket

Next, we have to create a bucket policy so that anyone has a read access to all objects inside it. The easiest way is to go inside our bucket, **Permissions**, **Bucket Policy** and at the bottom of the page there is a link to a policy generator. Open it in a separate tab. On this page you will also find the ARN (Amazon Resource Number) of your S3 bucket. Copy it as you will need it in a moment.

<img src="\assets\img\2020-07-13-s3-website\Screenshot 2020-10-27 at 16.19.20.png" width="100%"/>


The settings in the policy generator should be as follows:

Select Type of Policy: **S3 Bucket Policy**

Effect: **Allow**

Principal: **\*** (which means every object in the bucket)

AWS Service: **Amazon S3**

Action: **GetObject** (anyone will have read access to anything that is inside the bucket, which is exactly what we want for a publicly accessible website)

Amazon Resource Name: _paste the ARN you previously copied and add the slash and wildcard at the end, in my case it will be_ **arn:aws:s3:::some-super-unique-name/\***

Click on **Add Statement** and **Generate Policy**. The policy JSON document is generated. Copy it and paste back in the **Bucket policy editor**. Click on **Save**.

<img src="\assets\img\2020-07-13-s3-website\Screenshot 2020-10-27 at 16.26.46.png" width="100%"/>

<img src="\assets\img\2020-07-13-s3-website\Screenshot 2020-10-27 at 16.27.06.png" width="100%"/>


# Upload a website to the S3 bucket

Now it is time to upload your files to the bucket. You can download an HTML5 template for free from multiple sources in the Internet.

# Enable S3 website hosting

The last step will be to allow our S3 bucket to actually respond to requests from a browser. Go to **Properties** tab, **Static website hosting** and click on the option **Use this bucket to host a website**. You need to provide index document, which in general is stored in the _index.html_ file (check your HTML template for that). Click on **Save**. 

When you click on the **Static website hosting** option again, you will see your website endpoint at the top. 

<img src="\assets\img\2020-07-13-s3-website\Screenshot 2020-10-27 at 16.32.19.png" width="50%"/>

# Congratulations!

Your website is ready :) 


_Hope you enjoyed this article! In case of any questions and remarks, please leave a comment._





