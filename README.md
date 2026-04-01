# 🚀 CLUBY Platform – Team Guide

> **Purpose**: This README explains how the CLUBY platform is organized, how the team collaborates using Git, and how to get a local environment running. It is intended for all developers joining or contributing to the project.

---

## 🏗️ Organization Structure

> **Annotation**: CLUBY uses a **decoupled architecture**. Each repository has a single responsibility, which allows teams to work independently while sharing contracts and infrastructure.

* **cluby-infra**
  *Infrastructure & shared services*

  * Docker Compose
  * PostgreSQL
  * Redis
  * Keycloak (realm configuration in `cluby/infrast/realms/`)

* **cluby-backend**
  *.NET 8 API following Clean Architecture*

  * Domain-driven structure
  * Authentication via Keycloak
  * RESTful endpoints consumed by Web & Mobile

* **cluby-web**
  *React Web Dashboard*

  * Feature-based folder structure
  * Used by admins and club managers

* **cluby-mobile**
  *React Native Mobile Application*

  * End-user focused
  * Shares API contracts with the backend

---

## 🌿 Development Workflow (Feature Branch Workflow)

> **Annotation**: To protect stability and code quality, **direct pushes to `main` are strictly forbidden**. Every change must go through a Pull Request.

### 🔒 Golden Rule

* ❌ Never push directly to `main`
* ✅ Always work in a branch and open a PR

---

## 1️⃣ Starting a New Feature

> **Annotation**: Always branch from the latest `main` to avoid conflicts and outdated code.

```bash
git checkout main
git pull origin main
git checkout -b feature/your-feature-name
```

**Branch naming conventions**:

* `feature/your-feature-name`
* `fix/bug-description`
* `refactor/module-or-concept`

---

## 2️⃣ Committing Your Work

> **Annotation**: Small, logical commits make reviews easier and help track changes clearly.

```bash
git add .
git commit -m "feat: add member attendance validation logic"
```

**Commit message tips**:

* Use present tense (`add`, `fix`, `refactor`)
* Be concise but descriptive

---

## 3️⃣ Syncing With `main` (Rebasing)

> **Annotation**: Rebasing keeps the Git history clean and avoids unnecessary merge commits.

```bash
git fetch origin
git rebase origin/main
```

If conflicts occur:

* Resolve them carefully
* Continue rebase with `git rebase --continue`

---

## 4️⃣ Pushing & Opening a Pull Request

> **Annotation**: Pull Requests are mandatory and ensure shared code ownership.

```bash
git push -u origin feature/your-feature-name
```

**Pull Request rules**:

* At least **one team member review** is required
* CI must pass before merging
* Use clear PR descriptions (what & why)

**After merge**:

* Delete the remote branch
* Delete your local branch

---

## ⚙️ Infrastructure & Keycloak Configuration

> **Annotation**: Keycloak is a shared dependency. Any change to roles or clients affects the entire system.

If your feature introduces **new roles, clients, or permissions**:

1. Modify Keycloak locally

   * Access: `http://localhost:8080`

2. Export the updated configuration:

```bash
docker exec <container_name> \
  /opt/keycloak/bin/kc.sh export \
  --file /opt/keycloak/data/import/infos.json
```

3. Commit the updated `infos.json` **in a new branch** of `cluby-infra`

4. Notify the team in your Backend/Web PR:

   * Mention that a new Infra branch must be pulled

---

## 📥 Getting Started (New Team Members)

> **Annotation**: Infrastructure always comes first. Applications depend on shared services.

### 1. Clone Infrastructure

```bash
git clone https://github.com/clubyy/cluby_infra.git
```

### 2. Environment Setup

```bash
cp .env.example .env
```

Update values if needed (ports, secrets, etc.).

### 3. Launch Infrastructure

```bash
docker-compose up -d
```

Verify that:

* PostgreSQL is running
* Redis is running
* Keycloak is accessible

### 4. Clone Applications

```bash
git clone https://github.com/clubyy/cluby-backend.git
git clone https://github.com/clubyy/cluby-web.git
```
## ☁️ Azure Setup (Required)

# Azure is used for deployments and infrastructure operations.

## 1. Install Azure CLI

# Check if installed:
``` bash 

az --version
```

# If not installed:
https://learn.microsoft.com/cli/azure/install-azure-cli
``` bash 
2. Login to Azure
az login
```
This opens a browser for authentication.

# 3. Select Subscription
``` bash 
az account list --output table
az account set --subscription "<SUBSCRIPTION_ID>"
az account show
```

Ensure:

Correct subscription
Correct tenant
Active session
Follow each repository’s README for run instructions.

---

## ✅ Final Notes

* Keep branches short-lived
* Communicate infra changes early
* Prefer clarity over cleverness in code

Welcome to the team — happy building! 🚀
