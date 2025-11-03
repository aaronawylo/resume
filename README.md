# Aaron Lo - Resume Website CI/CD Pipeline Documentation

## 1. Overview
This project hosts a static resume website for Aaron Lo on **AWS S3**.  
The site is automatically deployed through a **CI/CD pipeline** using **AWS CodePipeline** whenever changes are committed to the repository.

**Pipeline Features:**
- Monitors GitHub repository for code changes.
- Automatically builds and packages the website.
- Deploys updates to an S3 bucket configured for static website hosting.
- Demonstrates CI/CD automation for static websites.

---

## 2. Architecture

   +-------------+          +---------------+          +----------------+
   | GitHub Repo |  ---->   | CodePipeline  |  ---->   | S3 Bucket      |
   |  (Source)   |          |    (CI/CD)    |          | (Hosting Site) |
   +-------------+          +---------------+          +----------------+
          ^                          |
          |                          |
   Developer commits ----------------+

- **GitHub Repo (Source Stage):** Contains the `index.html` file and other static assets.
- **CodePipeline:** Watches for commits on the main branch. Triggers build (optional for static sites) and deployment stages.
- **S3 Bucket (Deploy Stage):** Hosts the static website and serves it via the S3 website endpoint.

---

## 3. Prerequisites

- AWS Account with access to S3 and CodePipeline.
- GitHub repository with your website code.
- AWS CLI installed (optional for manual deployments).
- Basic knowledge of Git for commits and pushes.

---

## 4. Setting Up the CI/CD Pipeline

### Step 1: Create S3 Bucket
1. Log in to AWS Console → S3 → Create Bucket.
2. Name the bucket (e.g., `aaronlo-resume-site`).
3. Enable **Static website hosting**.
4. Set the **Index document** to `index.html`.

### Step 2: Create GitHub Repository
1. Push your website files (at minimum `index.html`) to GitHub.
2. Add a `.gitignore` file to exclude unnecessary files (e.g., `.DS_Store`).

### Step 3: Configure CodePipeline
1. Go to AWS Console → CodePipeline → Create Pipeline.
2. Name the pipeline (e.g., `ResumeWebsitePipeline`).
3. **Source Stage:** Connect to your GitHub repo and select the branch (e.g., `main`).
4. **Build Stage:** Optional for static sites. Can skip or use CodeBuild if you want to process assets.
5. **Deploy Stage:** Choose **Amazon S3** as the deployment target.
   - Select your S3 bucket created in Step 1.

### Step 4: Grant Permissions
- Ensure CodePipeline and CodeBuild roles have permissions to access your S3 bucket.
- Example permissions: `s3:PutObject`, `s3:GetObject`, `s3:ListBucket`.

### Step 5: Test the Pipeline
1. Make a change to your `index.html` (e.g., update a title or add a skill).
2. Commit and push to GitHub.
3. Watch the pipeline automatically trigger and deploy changes to S3.

---

## 5. Maintenance

- **Updating Content:** Make changes to the website files locally → commit → push → pipeline automatically deploys updates.
- **Pipeline Monitoring:** Use AWS Console → CodePipeline to check status and logs.
- **Cost Management:** Delete the S3 bucket or pipeline when no longer needed to avoid charges.
- **Security:** Ensure S3 bucket policy only exposes public access if intended. Otherwise, use CloudFront with signed URLs for restricted access.

---

## 6. Troubleshooting

| Issue | Solution |
|-------|---------|
| Website not updating | Check that pipeline completed successfully; verify files are in S3. |
| Access denied | Update S3 bucket policy to allow public read (if desired). |
| Build stage fails | For static websites, you can skip the build stage or configure CodeBuild correctly. |

---

## 7. Demo Video

A demonstration of the CI/CD pipeline in action will show:
1. Walkthrough explaining the pipeline.
2. Feature list: source monitoring, automatic deployment, S3 hosting.
3. Demo: changing `index.html` triggers pipeline → updates website.

**Video Link:** [Your Video URL Here]

---

## 8. Clean-Up

- Delete the S3 bucket and its contents.
- Delete the CodePipeline to prevent ongoing costs.
- Remove IAM roles or policies created for this project (if not reused).
