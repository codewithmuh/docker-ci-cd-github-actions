# 🚀 GitHub Actions Multi-Registry Docker DevSecOps Pipeline

<p align="center">
  <a href="https://github.com/codewithmuh/docker-ci-cd-github-actions/releases"><img src="https://img.shields.io/github/v/release/codewithmuh/docker-ci-cd-github-actions?color=blue&label=version&style=flat-square" alt="GitHub Release"></a>
  <a href="https://github.com/codewithmuh/docker-ci-cd-github-actions/stargazers"><img src="https://img.shields.io/github/stars/codewithmuh/docker-ci-cd-github-actions?style=flat-square" alt="Stars"></a>
  <a href="https://github.com/codewithmuh/docker-ci-cd-github-actions/network/members"><img src="https://img.shields.io/github/forks/codewithmuh/docker-ci-cd-github-actions?style=flat-square" alt="Forks"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-green.svg?style=flat-square" alt="License: MIT"></a>
  <a href="https://youtube.com/@codewithmuh"><img src="https://img.shields.io/badge/YouTube-%40codewithmuh-FF0000?style=flat-square&logo=youtube&logoColor=white" alt="YouTube"></a>
  <br>
  <img src="https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF?style=flat-square&logo=github-actions&logoColor=white" alt="GitHub Actions">
  <img src="https://img.shields.io/badge/Registry-DockerHub%20%7C%20AWS%20ECR-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Multi-Registry">
  <img src="https://img.shields.io/badge/Security-Trivy%20Vulnerability%20Scan-4C6FFF?style=flat-square" alt="Trivy Scan">
  <img src="https://img.shields.io/badge/Alerts-SMTP%20Email%20Reports-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email Alerts">
</p>

A production-grade CI/CD pipeline using **GitHub Actions** for building Docker images, pushing concurrently to **DockerHub** and **AWS ECR**, scanning with **Trivy**, and sending email notifications with vulnerability reports.

```mermaid
flowchart TD
    Push["Developer Push to main"] --> Build["Stage 1: Build Docker Image<br/>(Tagged with short SHA)"]
    Build --> Scan["Stage 2: Trivy Container Vulnerability Scan"]
    
    Scan --> PushHub["Stage 3A: Authenticate & Push to DockerHub"]
    Scan --> PushECR["Stage 3B: Authenticate & Push to AWS ECR"]
    
    PushHub --> Email["Stage 4: Send Detailed Security Scan Report via Email"]
    PushECR --> Email
```

---

## 🔧 Features

* ✅ Build Docker images on every push to `main`
* 🔁 Push to both **DockerHub** and **AWS ECR**
* 🛡️ Scan images for vulnerabilities using **Trivy**
* 📧 Email detailed scan reports automatically

---

## 🗂️ Repository Structure

```
.
├── .github/workflows/
│   └── docker-multi-registry.yml   # Main GitHub Actions workflow
├── Dockerfile                      # Simple Python Flask app image
├── app.py                          # Flask app code
└── README.md                       # You're here
```

---

## 🚀 Quick Start

### 1. Setup GitHub Secrets

| Name                    | Description                         |
| ----------------------- | ----------------------------------- |
| `DOCKER_USERNAME`       | DockerHub username                  |
| `DOCKER_PASSWORD`       | DockerHub password or token         |
| `AWS_ACCESS_KEY_ID`     | AWS IAM access key                  |
| `AWS_SECRET_ACCESS_KEY` | AWS IAM secret key                  |
| `AWS_REGION`            | Your AWS region (e.g., `us-east-1`) |
| `AWS_ACCOUNT_ID`        | Your AWS account ID                 |
| `EMAIL_USER`            | SMTP username (e.g., Gmail)         |
| `EMAIL_PASS`            | SMTP password / App password        |
| `EMAIL_TO`              | Recipient email address             |

---

### 2. Clone & Push Code

```bash
git clone https://github.com/codewithmuh/docker-ci-cd-github-actions
cd docker-ci-cd-github-actions
git push origin main
```

---

## ⚙️ How It Works

1. **Docker Image Build**
   On push to `main`, the image is built and tagged using the commit SHA.

2. **Push to Registries**
   Image is pushed to DockerHub and AWS ECR using configured secrets.

3. **Security Scan**
   The same image is pulled and scanned using [Trivy](https://github.com/aquasecurity/trivy).

4. **Email Notification**
   Scan report is sent as an attachment to the configured email recipient.

---

## 📬 Example Email Report

You will receive an email like:

> **Subject:** Docker Image Scan Report
> **Attachment:** `trivy-report.json`
> **Body:** The Trivy scan report is attached.

---

## ✅ Future Enhancements

* Store scan reports to **Amazon S3**
* Slack/Discord integrations
* Scheduled nightly or weekly scans
* Add **Grype**, **Dockle**, or **Snyk** for advanced analysis

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

## 🙌 Contributions

Contributions are welcome! Open an issue or submit a PR with your improvements.

---

## 💡 Author

Made with ❤️ by [CodeWithMuh](https://github.com/codewithmuh)
