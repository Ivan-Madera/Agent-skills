---
name: git-smart-commit-push
description: Analyze modified files, generate a structured commit message using Commitizen standard, create a commit, and push to the current branch safely if permissions allow.
---

# 🚀 Git Smart Commit & Push GOD `v2.0`

> [!IMPORTANT]
> This workflow is designed for **Atomic, Standardized Git History**. It prioritizes **Meaningful Context** over speed. Never commit broken code or push without verification.

---

## 🎯 Executive Summary

Automate the full Git lifecycle with elite engineering standards. No more generic messages, no more messy history, and **Zero Friction** deployments.

- **Deep Analysis:** Understands intent before drafting messages.
- **Commitizen Compliant:** Enforces industry-standard naming conventions.
- **Pre-Flight Validation:** Ensures the build is stable before committing.
- **Safe Deployment:** Automated push flow with strict permission checks.

---

## 🧠 Core Engineering Principles

| Principle                | Description                                                                  |
| :----------------------- | :--------------------------------------------------------------------------- |
| **Atomic Commits**       | One logical change per commit. Keep the history readable and reversible.     |
| **Standardized Format**  | Always follow the `type(scope): description` pattern. No exceptions.         |
| **Validation First**     | Never commit code that breaks the build or fails basic sanity checks.       |
| **No "Lazy" Messages**   | Descriptions must be specific. "Fixed stuff" is forbidden.                   |
| **Safe Networking**      | Never use force push unless explicitly requested by a human for a specific reason. |

---

## ⚙️ The Workflow (MANDATORY ORDER)

### 🧹 Phase 1: State Detection

Before acting, you must understand the current delta.

1.  **Status Scan:** Run `git status` to identify modified, new, and deleted files.
2.  **Diff Intelligence:** Run `git diff` (and `git diff --cached`) to analyze the actual logic changes.
3.  **Intent Detection:** Determine if the changes are a feature, a fix, a refactor, or just documentation.

---

### 📝 Phase 2: Standardized Drafting

Construct the commit message using the **Commitizen (Conventional Commits)** standard.

#### 🏗️ Commit Classification

| Type       | Use Case                                                                 |
| :--------- | :----------------------------------------------------------------------- |
| **feat**   | A new feature or functionality.                                          |
| **fix**    | A bug fix.                                                               |
| **refactor** | Code change that neither fixes a bug nor adds a feature.                |
| **perf**   | A code change that improves performance.                                 |
| **docs**   | Documentation only changes.                                              |
| **style**  | Changes that do not affect the meaning of the code (white-space, etc).   |
| **test**   | Adding missing tests or correcting existing tests.                        |
| **chore**  | Changes to the build process or auxiliary tools and libraries.            |

#### ✍️ Message Structure
- **Format:** `type(scope): short description`
- **Scope Examples:** `auth`, `api`, `config`, `ui`, `db`, `deps`.
- **Rules:** Use lowercase, max 72 characters, and be specific.

> [!TIP]
> If you detect a breaking change, add `BREAKING CHANGE:` in the footer of the commit message.

---

### 🧪 Phase 3: Pre-Commit Validation

**Safety Check:** You MUST verify the code state before finalizing the commit.

1.  **Stage Files:** Run `git add .` (or target specific files).
2.  **Build Verification:** If applicable, run a quick build or lint check (e.g., `npm run build` or `lint`).
3.  **Gatekeeping:** If the build is broken or there are obvious errors, **STOP**. Suggest a fix instead of committing.

---

### 💾 Phase 4: Persistence & Push

1.  **Commit:** Run `git commit -m "<generated_message>"`.
2.  **Branch Detection:** Identify the current branch using `git branch --show-current`.
3.  **Safe Push:** Run `git push origin <branch>`.

- **Requirement:** If permissions are denied or a conflict is detected, stop and report the manual command to the USER.

---

## 📋 Reporting Format (STRICT)

For every commit lifecycle completed, provide the following summary:

| Field                | Details                               |
| :------------------- | :------------------------------------ |
| **📂 Files**         | List of modified/added files          |
| **🧠 Type**          | `feat` / `fix` / `refactor` / etc.    |
| **📝 Message**       | `type(scope): description`            |
| **🚀 Result**        | Committed & Pushed / Local Only       |

---

## 🚫 Forbidden Actions (The "Never" List)

- **NO** `--force` push (Ever).
- **NO** Empty commits.
- **NO** Vague messages (e.g., "update", "fixes").
- **NO** Committing code with obvious syntax errors or "TODO" markers.

---

## ⚡ Activation Triggers

- _"commit my changes"_
- _"haz commit y push"_
- _"git smart flow"_
- _"generate commit message"_
- _"push to current branch"_
- _"sube mis cambios"_

---