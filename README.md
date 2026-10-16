<h1 align="center">Hi, I'm Masego 👋</h1>
<h3 align="center">Cloud & AI Software Engineer · DevOps · ZA 📍</h3>
<p align="center">
  <img src="https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExM29tdnI0MXZoYmd1eTVneXY3djAxN3Bha3BlcnYwdHJib2dnYnpsdiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/JpLVqOg8xTY3EmoYF7/giphy.gif" alt="Banner" width="850" height="450" />
</p>
<p align="center">
  <a href="https://linkedin.com/in/masego-mashigo-68a1b3240">
    <img src="https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white" />
  </a>
  <a href="mailto:mashigokk@outlook.com">
    <img src="https://img.shields.io/badge/Email-D14836?logo=gmail&logoColor=white" />
  </a>
</p>

---

## 💫 About Me

I'm a Cloud & AI Software Engineer with a background in Systems Engineering, grounded in Information Systems and Computer Science, and a foundation in data analytics and BI. I design, build, automate, and deploy systems end-to-end — from defining requirements and architecture, to writing clean Python and SQL, to provisioning AWS infrastructure with Terraform, integrating AI into real products, and shipping them through reliable CI/CD pipelines.

Systems engineering taught me to see the whole picture: how components, people, and processes fit together, and how to design solutions that are reliable, scalable, and easy to maintain. My data background means I think in terms of outcomes — every system I build should produce something people can trust and act on. I also bring a project management mindset: planning clearly, managing the full system lifecycle, owning delivery, and communicating progress in plain language to technical and non-technical stakeholders alike.

> *"I don't just write code — I deliver working solutions."*
>
> 👉 **See the proof:** six AWS projects built end-to-end with Terraform, tests and CI/CD in **[Discovering-Cloud-Engineering](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering)**

---

## 🎯 What I'm Working On

- ☁️ Growing my **cloud engineering** skills — six AWS projects shipped, now bringing the same patterns to **Azure**
- 🤖 Building **AI-powered applications** and learning to deploy and monitor models in production (MLOps)
- 🔁 Automating build, test, scan, and deployment with **GitHub Actions CI/CD pipelines**
- 📊 Building toward **Microsoft PL-300**, with **DP-600** and **DP-700** (Microsoft Fabric) on the roadmap
- 🏗️ Building end-to-end projects on real sports and business datasets

---

## 💡 Core Skills

| Area | Tools & Technologies |
|---|---|
| **Software Development** | Python (FastAPI, boto3) · C# · Java · C++ · HTML5 · SQL · Bash |
| **Cloud Engineering** | AWS (S3, Lambda, API Gateway, DynamoDB, VPC, EC2, ECS Fargate, ECR, Step Functions, EventBridge, SQS, CloudTrail, Config, IAM) · Azure (Data Factory, Synapse) · Microsoft Fabric |
| **Infrastructure as Code** | Terraform (including `terraform test`) |
| **DevOps & Automation** | GitHub Actions · Docker (multi-stage builds) · Trivy image scanning · OIDC to AWS · Git · GitHub · Bitbucket |
| **Testing** | pytest · moto · httpx |
| **AI & Data Engineering** | Python (pandas, scikit-learn) · Apache Airflow · ETL pipeline design |
| **Databases** | MS SQL Server · DynamoDB · PostgreSQL · MySQL · MongoDB · Firebase |
| **BI & Visualisation** | Power BI (DAX, semantic modelling, report design) |
| **Project Management** | End-to-end delivery · requirements gathering · ADRs & runbooks · stakeholder communication |

### 🚀 Currently Expanding Into
Azure (rebuilding my AWS projects on Azure) · Kubernetes · LLM integration · Agile/Scrum with Jira

---

## 🏆 Highlights for Recruiters

- ✅ **Full lifecycle ownership** — every project goes from architecture and ADRs, through build and tests, to a runbook and a teardown script
- ✅ **Cloud + code + data** — six AWS projects in Terraform, Python services with tests, and SQL Server analytics work
- ✅ **Secure CI/CD** — pipelines that test, build, scan with Trivy, and deploy to ECS Fargate using OIDC (no stored AWS keys)
- ✅ **Delivery-focused** — I plan, prioritise, and communicate progress like a project manager, not just a developer
- ✅ **Currently available** for Cloud Engineer, DevOps Engineer, Software Developer, and AI Software Engineer roles in Johannesburg or remote

---

## 🗂️ Featured Projects

> ✅ *All six projects below are built and documented, each with its own architecture notes, runbook, and screenshots, in **[Discovering-Cloud-Engineering](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering)**.*

---

### 🚢 Containerised API with Secure CI/CD on ECS Fargate
A FastAPI service packaged in a multi-stage Docker image. Every push runs pytest, builds the image, scans it with Trivy, pushes to ECR, and deploys to ECS Fargate behind a load balancer. GitHub Actions signs in to AWS with OIDC, so no long-lived keys are stored, and the ECS circuit breaker automatically rolls back a failed release.

```mermaid
flowchart LR
  push[git push] --> gha[GitHub Actions]
  gha --> test[pytest] --> build[Docker build] --> scan[Trivy scan] --> ecr[(Amazon ECR)]
  gha -. OIDC, no stored keys .-> iam[AWS IAM]
  ecr --> ecs[ECS Fargate]
  alb[Load Balancer] --> ecs
  ecs -- failed deploy --> rb[Auto rollback]
```

**Tools:** Python · FastAPI · Docker · Trivy · GitHub Actions · AWS (ECS Fargate, ECR, ALB, IAM) · Terraform

> 📁 *[View project](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering/tree/main/cloud-pro_5/05-ecs-fargate-cicd)*

---

### 🔄 Event-Driven CSV Data Pipeline
A serverless pipeline: a CSV dropped into S3 triggers EventBridge, which starts a Step Functions workflow that validates and loads the data with Lambda into DynamoDB. Bad records go to an SQS dead-letter queue instead of being lost.

**Tools:** AWS (S3, EventBridge, Step Functions, Lambda, DynamoDB, SQS) · Python · pytest · moto · Terraform · GitHub Actions

> 📁 *[View project](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering/tree/main/cloud-pro_6/06-event-driven-csv-pipeline)*

---

### ⚡ Serverless Notes API
A REST API built on Lambda, API Gateway, and DynamoDB in Python, with a pytest suite and a CI pipeline that runs tests and `terraform validate` on every push.

**Tools:** AWS (Lambda, API Gateway, DynamoDB) · Python · pytest · Terraform · GitHub Actions

> 📁 *[View project](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering/tree/main/cloud-pro_3)*

---

### 🛡️ More AWS Builds

- **VPC + Hardened Web Server** — custom network design, EC2 hardening, and SSM access with no open SSH · [View](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering/tree/main/cloud-pro_4)
- **AWS Security Baseline** — CloudTrail logging and AWS Config compliance rules, with real non-compliance findings captured · [View](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering/tree/main/cloud-pro_7)
- **Static Website on S3** — S3 hosting provisioned with Terraform · [View](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering/tree/main/cloud-pro_1)
- **UCL 2021/22 SQL Analysis** — SQL Server scripts analysing Champions League data · [View](https://github.com/masegoleroux-commits/SQL_Boulevard)

---

### 🔜 Coming Next

- 📊 **Sports Analytics & AI Platform** — PostgreSQL warehouse, scikit-learn models, and Power BI dashboards for coaching, sports science, scouting, and commercial teams
- ☁️ **Cloud Business Reporting Solution** — SQL Server → Azure Data Factory → Power BI semantic model with automated daily refresh
- 🔄 **Airflow ETL Pipeline** — daily CSV loads into PostgreSQL with data quality checks, Docker, and GitHub Actions

---

## 💻 Tech Stack

**Languages**

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![C#](https://img.shields.io/badge/c%23-%23239120.svg?style=for-the-badge&logo=csharp&logoColor=white)
![C++](https://img.shields.io/badge/c++-%2300599C.svg?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
![Bash](https://img.shields.io/badge/bash-%234EAA25.svg?style=for-the-badge&logo=gnubash&logoColor=white)

**Cloud & DevOps**

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Terraform](https://img.shields.io/badge/terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)
![Azure](https://img.shields.io/badge/azure-%230072C6.svg?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Apache Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?style=for-the-badge&logo=Apache%20Airflow&logoColor=white)

**AI & Data**

![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)
![Pytest](https://img.shields.io/badge/pytest-%230A9EDC.svg?style=for-the-badge&logo=pytest&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![Power Bi](https://img.shields.io/badge/power_bi-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Microsoft Fabric](https://img.shields.io/badge/Microsoft%20Fabric-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)

**Databases**

![MicrosoftSQLServer](https://img.shields.io/badge/Microsoft%20SQL%20Server-CC2927?style=for-the-badge&logo=microsoft%20sql%20server&logoColor=white)
![DynamoDB](https://img.shields.io/badge/Amazon%20DynamoDB-4053D6?style=for-the-badge&logo=Amazon%20DynamoDB&logoColor=white)
![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=for-the-badge&logo=mongodb&logoColor=white)
![Firebase](https://img.shields.io/badge/firebase-a08021?style=for-the-badge&logo=firebase&logoColor=ffcd34)

**Version Control & Project Management**

![Git](https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)
![Bitbucket](https://img.shields.io/badge/bitbucket-%230047B3.svg?style=for-the-badge&logo=bitbucket&logoColor=white)
![Jira](https://img.shields.io/badge/jira-%230A0FFF.svg?style=for-the-badge&logo=jira&logoColor=white)

---

## 🤝 Let's Work Together

I also take on **freelance projects**. I can help with:

- ☁️ **Cloud solutions** — setting up and automating infrastructure on AWS with Terraform
- 💻 **Software & automation** — Python tools, APIs, and scripts that save time
- 🔁 **CI/CD pipelines** — automated testing, security scanning, and deployment with GitHub Actions
- 🔄 **Data pipelines** — automated ingestion, validation, and loading
- 📋 **Project delivery** — planning, coordinating, and seeing tech projects through to launch

No jargon, no fluff — just working solutions your team will actually use.

📧 **[mashigokk@outlook.com](mailto:mashigokk@outlook.com)** · 💼 **[LinkedIn](https://linkedin.com/in/masego-mashigo-68a1b3240)**

---

## 😄 A Bit About Me

- 🏟️ I build projects on **real sports datasets** — because tech is more fun when you care about the subject
- ☕ My best code is written after a strong cup of coffee
- 🚀 I love the moment a pipeline runs green end-to-end for the first time
- 🌍 Based in **Johannesburg** (SAST, UTC+2) — working with clients locally and remotely across Africa and beyond
- 📚 I believe the best engineers are the ones who **never stop asking "why?"**

---

## 📊 GitHub Stats

![Masego's GitHub Stats](https://github-readme-stats.vercel.app/api?username=masegoleroux-commits&theme=dark&hide_border=false)

![GitHub Streak](https://streak-stats.demolab.com/?user=masegoleroux-commits&theme=dark&hide_border=false)

![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=masegoleroux-commits&theme=dark&hide_border=false&layout=compact)

![Activity Graph](https://github-readme-activity-graph.vercel.app/graph?username=masegoleroux-commits&theme=react-dark&hide_border=true)

![Profile Views](https://visitcount.itsverts.com/api?id=masegoleroux-commits&icon=0&color=0)

---

## ✍️ Random Dev Quote

![Dev Quote](https://quotes-github-readme.vercel.app/api?type=horizontal&theme=radical)

---

## 🔝 Top Contributed Repos

![Top Contributions](https://github-contributor-stats.vercel.app/api?username=masegoleroux-commits&limit=5&theme=dark&combine_all_yearly_contributions=true)

---

<p align="center">
  <i>Open to Cloud Engineer · DevOps Engineer · Software Developer · AI Software Engineer roles · Johannesburg or Remote</i>
</p>
