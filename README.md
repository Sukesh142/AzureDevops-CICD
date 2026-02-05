# 🚀 MuleSoft CI/CD Pipeline – Azure DevOps

This repository contains the **CI/CD pipeline configuration** for building and deploying a MuleSoft application to **CloudHub 2.0** using **Azure DevOps** and **Maven**.

The pipeline follows an **enterprise artifact promotion model**, ensuring the application is built once and safely deployed across multiple environments.

---

## 🏗 Pipeline Overview

| Branch | Deployment Flow |
|--------|------------------|
| `develop` | **Build → QA → UAT** |
| `main` | **Build → PROD** (Approval Required) |

---

## 🔄 Pipeline Stages

### 1️⃣ Build Stage
**Purpose:** Compile, package, and prepare the Mule application.

**Actions Performed:**
- Checkout source code
- Use secure `settings.xml`
- Build Mule application using Maven
- Run MUnit tests (if enabled)
- Publish build artifact for downstream deployments

---

### 2️⃣ QA Deployment
**Trigger:** Push to `develop` branch  

**Actions:**
- Download artifact produced in Build stage
- Deploy application to **QA** environment in CloudHub 2.0

---

### 3️⃣ UAT Deployment
**Trigger:** QA stage success  

**Actions:**
- Deploy the **same artifact** to **UAT** environment

---

### 4️⃣ Production Deployment
**Trigger:** Merge to `main` branch  

**Actions:**
- Requires **manual approval**
- Deploys artifact to **Production** environment

---

## 🔧 Technologies Used

- Azure DevOps Pipelines  
- Maven  
- MuleSoft Runtime  
- CloudHub 2.0  
- Anypoint Platform Connected App  

---

## 🔐 Secure Configuration

Sensitive values are managed using **Azure DevOps Variable Groups**:

| Variable Group | Purpose |
|----------------|---------|
| `mule-deploy-vars` | Common pipeline configuration |
| `mule-vars-qa` | QA environment variables |
| `mule-vars-uat` | UAT environment variables |
| `mule-vars-prod` | Production environment variables |

**Secure File Used:**
- `settings.xml` (Maven configuration)

---

## 📦 Deployment Strategy

✔ Build once  
✔ Promote the same artifact across environments  
✔ Environment-specific configuration  
✔ No rebuild between stages  
✔ Production approval gate  

This ensures **consistency**, **traceability**, and **safe releases**.

---

## ▶ How to Trigger Deployments

| Action | Result |
|--------|--------|
| Push to `develop` | Deploys to QA → UAT |
| Merge to `main` | Triggers Production deployment (approval required) |

---

## 🛠 Troubleshooting Guide

| Issue | What to Check |
|------|---------------|
| Build failure | Maven logs in Build stage |
| Deployment failure | CloudHub logs |
| Authentication errors | Connected App credentials |
| Dependency issues | `settings.xml` configuration |

---

## 📌 Best Practices Followed

- Artifact promotion model  
- Secure credential handling  
- Environment isolation  
- Approval gates for production  
- Parameterized deployment templates  

---

## 👤 Maintainer

**Integration / MuleSoft DevOps Team**
