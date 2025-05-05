# S3 Static Website Hosting Guide

This guide outlines how to configure an S3 bucket for static website hosting and optionally use it as part of your AWS 3-Tier Web App Lab for storing assets or serving frontend content.

---

## 📦 Step 1: Create an S3 Bucket

- Navigate to the **S3** service in the AWS Console.
- Click **Create bucket**.
- Bucket name: `your-bucket-name` (must be globally unique)
- Region: Same as your EC2/RDS (for simplicity)
- Uncheck **Block all public access** (for public website)
- Acknowledge warning and proceed

---

## 🌐 Step 2: Enable Static Website Hosting

1. After creating the bucket, go to the **Properties** tab.
2. Scroll to **Static website hosting**.
3. Click **Edit** and enable hosting.
4. Specify:
   - **Index document**: `index.html`
   - (Optional) **Error document**: `error.html`
5. Save changes.

---

## 🔐 Step 3: Add Bucket Policy for Public Access

Click the **Permissions** tab → **Bucket Policy** → paste the following:

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

Replace `your-bucket-name` with the actual name of your bucket.

---

## 📤 Step 4: Upload HTML Content

From your terminal:

```bash
aws s3 cp app/index.html s3://your-bucket-name/index.html --acl public-read
```

Or use the AWS Console to upload the file manually.

---

## ✅ Step 5: Test the Website

- Go back to **Properties** → **Static Website Hosting**
- Copy the **Endpoint** URL
- Paste into your browser
- You should see your `index.html` content

Example Output:

📸 `custom-ec2-webpage.png`  
📸 `apache-default-page.png` (for comparison if hosted locally)

---

## 🧠 Tips

- Use this to host error pages, frontend UIs, or image assets
- You can also integrate CloudFront for HTTPS + caching
- Don't forget to clean up your bucket if you're done testing

---

## 🔗 Related Files

- `/app/index.html` — sample webpage
- `/assets/` — where you can upload or sync content
