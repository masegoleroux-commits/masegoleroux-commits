<h1 align="center">Hi, I'm Masego 👋</h1>
<h3 align="center">Cloud & DevOps Engineer · AWS · Terraform · CI/CD · ZA 📍</h3>

<p align="center">
  <img src="https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExM29tdnI0MXZoYmd1eTVneXY3djAxN3Bha3BlcnYwdHJib2dnYnpsdiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/JpLVqOg8xTY3EmoYF7/giphy.gif" alt="Banner" width="850" height="450"/>
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

I'm a Cloud & DevOps Engineer with a background in Systems Engineering, Information Systems, Computer Science and BI. I build AWS infrastructure entirely as code (Terraform), ship services through pipelines that test, scan and deploy on every push, and design for failure from the start: automated rollback, dead-letter queues, and audit logging are defaults, not extras.

Every project I build ships with the same engineering artefacts a production team would expect: an architecture diagram, **Architecture Decision Records (ADRs)** explaining the trade-offs, a **runbook** for operating it, automated tests, and a **teardown script** so nothing is left running and costing money. Systems engineering taught me to reason about the whole system — components, failure modes, security boundaries, and the people who will operate it after me.

> *"I don't just write code — I deliver working, documented, operable systems."*
>
> 👉 **See the proof:** six AWS projects in **[Discovering-Cloud-Engineering](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering)**

---

## 🧭 Engineering Principles

| Principle | How it shows up in my work |
|---|---|
| **Everything as code** | All infrastructure provisioned with Terraform; no console click-ops. State and variable files are kept out of Git. |
| **Shift-left security** | Container images scanned with Trivy in CI before they reach ECR. CI authenticates to AWS through **OIDC federation**, so no long-lived access keys exist to leak. |
| **Design for failure** | ECS deployment circuit breaker rolls back bad releases automatically. Pipelines route bad records to an SQS dead-letter queue instead of dropping them. |
| **Test at every layer** | Unit tests with pytest, AWS services mocked with moto, API tests with httpx, and infrastructure tests with native `terraform test`. |
| **Operability is part of done** | Each project has a runbook, ADRs, and architecture diagrams, so someone else can run it without me. |
| **Cost awareness** | Every environment has a teardown path; resources are destroyed after verification and evidence is kept as screenshots. |

---

## 🎯 What I'm Working On

- ☁️ **Multi-cloud:** porting my AWS patterns to **Azure** (Terraform + GitHub Actions OIDC to Azure)
- 🤖 **MLOps:** deploying and monitoring models in production behind the same tested, scanned CI/CD pipelines
- 📊 **Data platform:** building toward **Microsoft PL-300**, with **DP-600** and **DP-700** (Microsoft Fabric) on the roadmap
- 🏗️ **Domain projects:** end-to-end builds on real sports and business datasets

---

## 💡 Core Skills

| Area | Tools & Technologies |
|---|---|
| **Cloud (AWS)** | Compute: Lambda, EC2, ECS Fargate · Networking: VPC, ALB, API Gateway · Data: S3, DynamoDB · Orchestration & events: Step Functions, EventBridge, SQS · Security & governance: IAM (OIDC), CloudTrail, AWS Config, SSM · Registry: ECR |
| **Infrastructure as Code** | Terraform (modules, variables/outputs, native `terraform test`, `terraform validate` in CI) |
| **CI/CD & Containers** | GitHub Actions · Docker (multi-stage builds on `python:3.12-slim`) · Trivy image scanning · OIDC federation to AWS |
| **Software Development** | Python (FastAPI, boto3) · SQL · Bash · C# · Java · C++ · HTML5 |
| **Testing** | pytest · moto (AWS mocking) · httpx · `terraform test` |
| **Databases** | DynamoDB · MS SQL Server (T-SQL) · PostgreSQL · MySQL · MongoDB · Firebase |
| **Data & BI** | ETL/ELT pipeline design · pandas · scikit-learn · Apache Airflow · Power BI (DAX, semantic modelling) · Azure Data Factory · Microsoft Fabric |
| **Engineering Practice** | ADRs · runbooks · architecture diagrams (draw.io) · requirements gathering · stakeholder communication |

### 🚀 Currently Expanding Into
Azure · Kubernetes · Observability (dashboards & alerting) · LLM integration · Agile/Scrum with Jira

---

## 🏆 Highlights for Hiring Managers

- ✅ **Secure delivery pipeline** — test → build → Trivy scan → push to ECR → deploy to ECS Fargate, authenticated with OIDC (zero stored AWS credentials), with automatic rollback on failed deployments
- ✅ **Event-driven architecture** — S3 → EventBridge → Step Functions orchestration with separate validate and load stages, and a dead-letter queue for failed records
- ✅ **Infrastructure tested like application code** — `terraform validate` and `terraform test` run alongside pytest suites in CI
- ✅ **Governance from day one** — CloudTrail audit logging and AWS Config compliance rules, with real non-compliance findings captured and documented
- ✅ **Documented decisions** — ADRs and runbooks for every project, written for the engineer who operates it next
- ✅ **Currently available** for Cloud Engineer, DevOps Engineer, Software Developer, and AI Software Engineer roles in Johannesburg or remote

---

## 🗂️ Featured Projects

> ✅ *All six projects are built, verified, documented, and torn down, with architecture notes, ADRs, runbooks, and screenshots in **[Discovering-Cloud-Engineering](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering)**.*

---

### 🚢 Containerised API with Secure CI/CD on ECS Fargate

**Problem:** ship a containerised service to AWS on every push without storing cloud credentials in CI, without letting vulnerable images reach production, and without a bad release taking the service down.

**Architecture:**

```mermaid
flowchart LR
  push[git push] --> gha[GitHub Actions]
  subgraph CI["CI pipeline"]
    gha --> test[pytest + httpx] --> build[Docker multi-stage build] --> scan[Trivy scan]
  end
  scan -->|image passes| ecr[(Amazon ECR)]
  gha -. OIDC: short-lived token .-> iam[AWS IAM role]
  ecr --> ecs[ECS Fargate service]
  alb[Application Load Balancer] --> ecs
  ecs -- deployment fails --> rb[Circuit breaker rollback]
  tf[Terraform + terraform test] -. provisions .-> alb & ecs & ecr & iam
```

| Decision | Why |
|---|---|
| **OIDC federation** instead of IAM access keys | CI gets short-lived credentials per run; there is no secret to rotate or leak |
| **Trivy scan as a pipeline gate** | Vulnerabilities are caught before the image is pushed, not after it is running |
| **Multi-stage Docker build** on a slim base | Smaller image, smaller attack surface, faster deploys |
| **ECS Fargate** over EC2 | No servers to patch; the team manages tasks, not hosts |
| **Deployment circuit breaker** | A failed release rolls back automatically — verified and captured in screenshots |
| **`terraform test`** for the CI auth setup | The IAM/OIDC trust configuration is tested like code, because a mistake there is a security issue |

**Stack:** Python · FastAPI · Docker · Trivy · GitHub Actions · AWS (ECS Fargate, ECR, ALB, IAM) · Terraform

> 📁 *[View project, ADRs and runbook](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering/tree/main/cloud-pro_5/05-ecs-fargate-cicd)*

---

### 🔄 Event-Driven CSV Data Pipeline

**Problem:** ingest CSV files reliably as they arrive, reject bad data without losing it, and make every step of processing visible.

```mermaid
flowchart LR
  s3[(S3 upload)] --> eb[EventBridge rule] --> sfn[Step Functions]
  sfn --> v[Validate Lambda] --> l[Load Lambda] --> ddb[(DynamoDB)]
  v -- invalid records --> dlq[[SQS dead-letter queue]]
```

| Decision | Why |
|---|---|
| **Event-driven** (S3 → EventBridge) instead of polling | Processing starts when data lands; nothing runs or costs money while idle |
| **Step Functions** to orchestrate separate validate and load stages | Each stage is small and testable, and the state machine shows exactly where a run failed |
| **Dead-letter queue** for failures | Bad data is kept for inspection and replay rather than silently dropped |
| **moto** for tests | AWS calls are tested locally in CI without deploying anything |

**Stack:** AWS (S3, EventBridge, Step Functions, Lambda, DynamoDB, SQS) · Python (boto3) · pytest · moto · Terraform · GitHub Actions

> 📁 *[View project](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering/tree/main/cloud-pro_6/06-event-driven-csv-pipeline)*

---

### ⚡ Serverless Notes API

**Problem:** a REST API with no servers to manage, that scales to zero when idle.

**Design:** API Gateway → Lambda (Python) → DynamoDB, provisioned in Terraform. CI runs the pytest suite and `terraform validate` on every push, so broken code or invalid infrastructure never merges.

**Stack:** AWS (API Gateway, Lambda, DynamoDB) · Python · pytest · Terraform · GitHub Actions

> 📁 *[View project](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering/tree/main/cloud-pro_3)*

---

### 🛡️ Platform & Security Foundations

| Project | Technical focus | Link |
|---|---|---|
| **VPC + Hardened Web Server** | Custom VPC network design, EC2 hardening, administrative access through SSM Session Manager | [View](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering/tree/main/cloud-pro_4) |
| **AWS Security Baseline** | CloudTrail audit logging, AWS Config managed rules, non-compliance findings documented | [View](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering/tree/main/cloud-pro_7) |
| **Static Website on S3** | S3 static hosting, Terraform fundamentals | [View](https://github.com/masegoleroux-commits/Discovering-Cloud-Engineering/tree/main/cloud-pro_1) |
| **UCL 2021/22 SQL Analysis** | T-SQL analysis of Champions League data on SQL Server | [View](https://github.com/masegoleroux-commits/SQL_Boulevard) |

---

### 🔜 Coming Next

- ☁️ **Azure port** — the event-driven pipeline rebuilt on Azure (Blob Storage → Event Grid → Functions) with Terraform and GitHub Actions OIDC
- 📊 **Sports Analytics & AI Platform** — PostgreSQL warehouse, scikit-learn models, and Power BI dashboards for coaching, sports science, scouting, and commercial teams
- ☁️ **Cloud Business Reporting Solution** — SQL Server → Azure Data Factory → Power BI semantic model with automated daily refresh
- 🔄 **Airflow ETL Pipeline** — scheduled CSV loads into PostgreSQL with data quality checks, Docker, and GitHub Actions

---

## 💻 Tech Stack

**Cloud, IaC & DevOps**

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Terraform](https://img.shields.io/badge/terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)
![Trivy](https://img.shields.io/badge/Trivy-1904DA?style=for-the-badge&logo=aqua&logoColor=white)
![Azure](https://img.shields.io/badge/azure-%230072C6.svg?style=for-the-badge&logo=microsoftazure&logoColor=white)

**Languages & Frameworks**

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)
![Bash](https://img.shields.io/badge/bash-%234EAA25.svg?style=for-the-badge&logo=gnubash&logoColor=white)
![C#](https://img.shields.io/badge/c%23-%23239120.svg?style=for-the-badge&logo=csharp&logoColor=white)
![C++](https://img.shields.io/badge/c++-%2300599C.svg?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)

**Testing**

![Pytest](https://img.shields.io/badge/pytest-%230A9EDC.svg?style=for-the-badge&logo=pytest&logoColor=white)

**Data & AI**

![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Apache Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?style=for-the-badge&logo=Apache%20Airflow&logoColor=white)
![Power Bi](https://img.shields.io/badge/power_bi-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Microsoft Fabric](https://img.shields.io/badge/Microsoft%20Fabric-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)

**Databases**

![DynamoDB](https://img.shields.io/badge/Amazon%20DynamoDB-4053D6?style=for-the-badge&logo=Amazon%20DynamoDB&logoColor=white)
![MicrosoftSQLServer](https://img.shields.io/badge/Microsoft%20SQL%20Server-CC2927?style=for-the-badge&logo=microsoft%20sql%20server&logoColor=white)
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

I also take on **freelance projects**:

- ☁️ **AWS infrastructure as code** — Terraform-managed environments that are reproducible and reviewable
- 🔁 **CI/CD pipelines** — GitHub Actions with automated tests, image scanning, and keyless (OIDC) cloud deployments
- 🔄 **Event-driven data pipelines** — serverless ingestion, validation, and loading with failure handling built in
- 🛡️ **Cloud governance baselines** — audit logging and compliance rules from day one
- 📋 **Project delivery** — requirements, architecture, ADRs, runbooks, and handover documentation

No jargon, no fluff — just working, documented systems your team can operate.

📧 **[mashigokk@outlook.com](mailto:mashigokk@outlook.com)** · 💼 **[LinkedIn](https://linkedin.com/in/masego-mashigo-68a1b3240)**

---

## 😄 A Bit About Me

- 🏟️ I build projects on **real sports datasets** — because tech is more fun when you care about the subject
- 🚀 I love the moment a pipeline runs green end-to-end for the first time
- 🌍 Based in **Johannesburg** (SAST, UTC+2) — working with teams locally and remotely across Africa and beyond
- 📚 I believe the best engineers are the ones who **never stop asking "why?"** — that's what ADRs are for

---

## 📊 GitHub Stats

![Masego's GitHub Stats](https://github-readme-stats.vercel.app/api?username=masegoleroux-commits&theme=dark&hide_border=false)

![GitHub Streak](https://streak-stats.demolab.com/?user=masegoleroux-commits&theme=dark&hide_border=false)

![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=masegoleroux-commits&theme=dark&hide_border=false&layout=compact)

![Activity Graph](https://github-readme-activity-graph.vercel.app/graph?username=masegoleroux-commits&theme=react-dark&hide_border=true)

---

<p align="center">
  <i>Open to Cloud Engineer · DevOps Engineer · Software Developer · AI Software Engineer roles · Johannesburg or Remote</i>
</p>
