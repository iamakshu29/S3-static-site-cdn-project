# 🧾 Manual Deployment: Static Website Hosting on AWS (S3 + CloudFront + Route 53)

This file contains step-by-step instructions to manually deploy a static website using AWS services.

---

## 🪣 Step 1: Create and Configure S3 Bucket

1. Go to **S3 → Create Bucket**
   - Bucket name: `your-bucket-name`
   - Region: Choose your region
   - Uncheck **Block all public access**
   - (Optional) Enable **Versioning**

2. Upload your site files (e.g., `index.html`, `style.css`, `images/`).

3. Create the bucket.

---

## 📤 Step 2: Upload Website Files to the S3 Bucket

1. Open your bucket.
2. Click **Upload** → Add files:
   - `index.html`
   - `style.css`
   - `script.js`
   - Any images or other assets
3. Click **Upload** to complete.

---

## 🌐 Step 3: Setup CloudFront Distribution (CDN)
1. Go to CloudFront → Create Distribution

2. Set:

    - Origin domain: Select your S3 bucket (not the website endpoint)

    - Origin Access: Create Origin Access Control (OAC) and attach it

    - Viewer Protocol Policy: Redirect HTTP to HTTPS

    - Default Root Object: index.html

    - (Optional) Add CNAME: www.yourdomain.com

    - SSL Certificate: Select ACM certificate (must be in us-east-1)

3. Wait for the distribution to deploy (~10–15 mins)

```json
https://<your-cloudfront-id>.cloudfront.net/index.html
```
## 📛 Step 3: Setup Custom Domain with Route 53
1. Go to Route 53 → Hosted Zones → yourdomain.com

2. Click Create Record

    - Record Type: A

    - Name: www (or blank for root domain)

    - Alias: Yes

    - Alias target: Select your CloudFront distribution from the dropdown

3. Wait for DNS propagation (~minutes to hours)

4. Test:

```json
https://www.yourdomain.com
```

## 🔒 Step 4: Setup HTTPS with ACM
1. Go to ACM → us-east-1 (N. Virginia)

2. Request a public certificate

    - Add: www.yourdomain.com

    - Choose DNS validation

3. ACM will give a CNAME to validate

    - Go to Route 53 → Hosted Zone → Create Record

    - Paste the ACM CNAME as provided

4. Wait for validation → status becomes "Issued"
   
5. Add the ACM in CloudFront


## 🧹 Step 5: Cleanup (To Avoid Charges)
   - ❌ Delete the S3 bucket (after backing up)

   - ❌ Disable & delete CloudFront distribution

   - ❌ Delete Route 53 hosted zone (or domain if no longer needed)

   - ❌ Remove ACM cert (optional, it’s free)

   - ❌ Delete records or disable auto-renewal for domain name (optional)


