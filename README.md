# 🚀 CI/CD Pipeline with GitHub Actions

## Overview

This project demonstrates a multi-stage CI/CD pipeline built using **GitHub Actions** for a Node.js application.

The workflow simulates a real-world delivery process including:

- Automated testing  
- Dependency caching  
- Artifact handling  
- Reusable deployment workflows  
- Conditional execution  
- Failure reporting  

The goal of this project is to showcase structured pipeline design, job orchestration, and failure handling in a production-like CI/CD setup.

---

## 🏗 Workflow Architecture

The pipeline consists of the following jobs:

```
test → build → deploy → deployment-result
↘
report (on failure)
```

### 1️⃣ Test Job
- Checks out repository  
- Caches dependencies  
- Installs dependencies if cache miss  
- Runs test suite  
- Uploads test artifacts on failure  

### 2️⃣ Build Job
- Runs only if tests pass (`needs: test`)  
- Reinstalls dependencies (fresh runner)  
- Builds the application  
- Uploads build artifacts for deployment  

### 3️⃣ Deploy Job (Reusable Workflow)
- Triggered via `workflow_call`  
- Downloads build artifacts  
- Simulates deployment  
- Exposes deployment result via workflow outputs  

### 4️⃣ Deployment Result Job
- Reads output from deploy workflow  
- Prints final deployment status  

### 5️⃣ Failure Report Job
- Runs only if any upstream job fails  
- Demonstrates failure handling using `if: failure()`  
- Outputs contextual workflow information  

---

## 🔑 Key Concepts Demonstrated

- Job dependency control using `needs`  
- Conditional execution using `if`  
- Caching using `actions/cache`  
- Artifact upload and download  
- Reusable workflows using `workflow_call`  
- Output passing between jobs  
- Failure simulation and reporting  
- Pull request validation  

---

## ⚙️ Triggers

The workflow runs on:

- Push to `main`  
- Pull requests targeting `main`  

This ensures both direct commits and proposed changes are validated before merge.

---

## 🧪 Failure Simulation

To validate pipeline behavior, test failures were intentionally introduced to observe:

- Downstream job skipping  
- Conditional artifact uploads  
- Failure-triggered report job execution  

This ensures correct failure propagation and workflow control.

---

## 📦 Reusable Deployment Workflow

The deployment logic is separated into a reusable workflow (`deploy.yml`) using:
```
workflow_call
```

This demonstrates modular pipeline design and output passing between workflows.

---

## 🛠 Technologies Used

- GitHub Actions  
- Node.js  
- YAML  
- CI/CD Concepts  

---

## 📌 Purpose of This Project

This project was built to:

- Strengthen understanding of CI/CD internals  
- Demonstrate pipeline orchestration skills  
- Showcase structured DevOps thinking  
- Simulate real-world deployment flow  

