# Hosting a Static Website with Amazon S3

Deploy your personal or project website easily and cost-effectively using Amazon S3! In this guide, you'll learn step-by-step how to serve static content—HTML, CSS, JavaScript, images, and more—directly from AWS infrastructure, without managing any servers.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Step 1: Create an S3 Bucket](#step-1-create-an-s3-bucket)
3. [Step 2: Enable Static Website Hosting](#step-2-enable-static-website-hosting)
4. [Step 3: Upload Your Website Files](#step-3-upload-your-website-files)
5. [Step 4: Make Your Site Public](#step-4-make-your-site-public)
6. [Step 5: View Your Website Online](#step-5-view-your-website-online)
7. [Bonus: Connect a Custom Domain](#bonus-connect-a-custom-domain)
8. [Conclusion](#conclusion)
9. [References](#references)

---

## Prerequisites

Before you begin, ensure you have the following:

- An [AWS account](https://aws.amazon.com/)
- Basic understanding of static websites (HTML, CSS, JS)
- Your website files ready (at minimum, an `index.html` file)

---

## Step 1: Create an S3 Bucket

1. **Log in** to your [AWS Management Console](https://aws.amazon.com/).
2. Navigate to the **S3** service.
3. Click **Create bucket**.
4. Enter a globally unique **Bucket name** — this will form part of your website’s public URL (e.g., `my-website-bucket`).
5. Select the AWS **Region** closest to your main audience.
6. Leave other options at their default settings for now.
7. Click **Create bucket**.

> **Tip:** Choose a bucket name that matches your intended domain (e.g., `www.example.com`) if you plan to use a custom domain.

---

## Step 2: Enable Static Website Hosting

1. In your bucket list, **click** your new bucket to open it.
2. Go to the **Properties** tab.
3. Scroll to **Static website hosting** and click **Edit**.
4. Select **Enable**.
5. Specify your **Index document** (usually `index.html`).
6. (Optional) Set an **Error document** (e.g., `error.html`) for friendly error pages.
7. Click **Save changes**.

You’ll see an **Endpoint** URL—this is your website’s public address!

---

## Step 3: Upload Your Website Files

1. Open your bucket and go to the **Objects** tab.
2. Click **Upload**.
3. Choose **Add files** and select your website files (`index.html`, CSS, JS, images, etc.).
4. Click **Upload**.

> **Note:** Keep your file structure intact (e.g., folders for images or scripts) to avoid broken links.

---

## Step 4: Make Your Site Public

S3 buckets are private by default. To let the world see your site:

### A. Disable Block Public Access

1. Go to the **Permissions** tab.
2. Click **Edit** under **Block public access (bucket settings)**.
3. Uncheck **Block all public access**.
4. Confirm your selection and click **Save changes**.

### B. Attach a Bucket Policy

1. Still in **Permissions**, scroll to **Bucket policy** and click **Edit**.
2. Paste and adjust the following policy (replace `YOUR_BUCKET_NAME`):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
    }
  ]
}
```
3. Click **Save changes**.

> **Warning:** Making your bucket public means anyone on the internet can access its contents. Only use this for public sites!

---

## Step 5: View Your Website Online

- Return to the **Properties** tab.
- In **Static website hosting**, copy the **Endpoint** URL.
- Paste it in your browser—your static website should now be live!

---

## Bonus: Connect a Custom Domain

Give your website a professional touch by linking it to your own domain name:

1. **Register a Domain:** Use [Route 53](https://aws.amazon.com/route53/) or any registrar.
2. **Create a Hosted Zone:** If using Route 53, set up a hosted zone for your domain.
3. **Set DNS Records:** Point your domain (A or CNAME record) to the S3 site endpoint.
4. **Enable HTTPS (Recommended):** Use [CloudFront](https://aws.amazon.com/cloudfront/) and [AWS Certificate Manager](https://aws.amazon.com/certificate-manager/) to serve your site securely.

> For a detailed walkthrough, see [AWS: Using a custom domain for a static website](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html#website-hosting-custom-domain-walkthrough).

---

## Conclusion

Hurray! Your static website is now hosted on Amazon S3—scalable, reliable, and maintenance-free. For extra features like HTTPS, custom error pages, or caching, integrate AWS CloudFront or further explore AWS’s documentation.

---

## References

- [AWS S3 Static Website Hosting Docs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html)
- [HTTPS for communication between CloudFront and your Amazon S3 Docs](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-cloudfront-to-s3-origin.html)
