🚀 CLUBY Platform - Team Guide

Welcome to the CLUBY development team. This project uses a decoupled architecture to manage a club activity ecosystem. To maintain code quality, we follow a strict Feature Branch Workflow.
🏗️ Organization Structure

    cluby-infra: Docker Compose, PostgreSQL, Redis, and Keycloak (realms/infos.json).

    cluby-backend: .NET 8 Clean Architecture API.

    cluby-web: React Feature-based Web Dashboard.

    cluby-mobile: React Native Mobile Application.

🌿 The Development Workflow (Branches)

Strict Rule: No one pushes directly to the main branch. All changes must go through a Pull Request.
1. Starting a New Feature

Always start by pulling the latest changes to ensure your base is up to date.
Bash

git checkout main
git pull origin main
git checkout -b feature/your-feature-name

Use naming conventions like feature/, fix/, or refactor/.
2. Committing Work

Break your work into small, logical commits.
Bash

git add .
git commit -m "feat: add member attendance validation logic"

3. Syncing with Main (Rebasing)

If your colleagues merged work into main while you were working, rebase your branch to avoid messy merge commits.
Bash

git fetch origin
git rebase origin/main

4. Pushing and Pull Requests

Push your branch to GitHub and open a Pull Request (PR).
Bash

git push -u origin feature/your-feature-name

    Review: At least one other team member must review the code before merging.

    Cleanup: Delete your local and remote branch after the PR is merged.

⚙️ Infrastructure & Keycloak

Since Keycloak configuration is shared via cluby-infra/realms/infos.json, follow this if your feature adds new roles or clients:

    Modify Keycloak in your local browser (localhost:8080).

    Export the new config:
    docker exec <container_name> /opt/keycloak/bin/kc.sh export --file /opt/keycloak/data/import/infos.json

    Commit the updated infos.json to a branch in cluby-infra.

    Notify the team in your Backend/Frontend PR that they need to pull the new Infra branch.

📥 Getting Started for New Members

    Clone the Infrastructure: git clone https://github.com/clubyy/cluby_infra.git

    Setup Env: Copy .env.example to .env.

    Launch: docker-compose up -d

    Clone Apps: Proceed to clone cluby-backend and cluby-web.
