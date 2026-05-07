---
name: snyk-workflow-god
description: Execute a professional-grade Snyk vulnerability resolution workflow. Focuses on clean installs, extension-based scanning, safe upgrades, and surgical overrides while maintaining build integrity and zero-residue cleanup.
---

# Snyk Workflow GOD

Automate a real-world vulnerability fixing workflow used by elite engineering teams. No generic fixes, no broken builds, and **Zero Residual Footprint**.

> [!IMPORTANT]
> This workflow is designed for **Production-Grade Dependency Management**. It prioritizes **Build Stability** over blind security compliance. Follow the steps in the exact order specified.

## Core Engineering Principles

| Principle                | Description                                                                  |
| :----------------------- | :--------------------------------------------------------------------------- |
| **Stability > Purity**   | A secure app that doesn't build is useless. Always verify runtime integrity. |
| **Clean Slate**          | Never debug or fix on top of "dirty" `node_modules`.                         |
| **Minimal Intervention** | Change the least amount of code possible. If Snyk is clean, stop.            |
| **Snyk > npm audit**     | Priority is Snyk compliance. Do NOT fix npm audit if Snyk is green.          |
| **No "Legacy" Crutches** | `--legacy-peer-deps` is forbidden. Fix the tree, don't ignore it.            |

## Key Capabilities

- **Clean State:** Always start from a neutral dependency tree.
- **Extension-First:** Leverage the IDE extension or Snyk CLI for contextual intelligence.
- **AI-Ready:** Automated authentication flow for autonomous agents.
- **Surgical Precision:** Apply upgrades first, overrides only as a last resort.
- **Zero Waste:** Automated cleanup of all temporary artifacts.

## Upgrade Priority Order

1. **Patch** (`x.x.Z`) — _Safe & Recommended_ ✅
2. **Minor** (`x.Y.x`) — _Usually Safe_ ✅
3. **Major** (`X.x.x`) — _Caution: Check for Breaking Changes_ ⚠️

## Override Implementation Pattern

Apply surgical overrides **ONLY** if:

- The vulnerability is transitive and no parent upgrade exists.
- A direct upgrade breaks the project's core functionality.

```json
"overrides": {
  "parent-pkg": {
    "vulnerable-transitive-pkg": "fixed.version"
  }
}
```

_Target the specific path to avoid side effects across the entire tree._

## Reporting Format

For every fix applied, provide the following summary:

| Field                | Details                               |
| :------------------- | :------------------------------------ |
| **🧩 Vulnerability** | `pkg-name` (Severity)                 |
| **🛠 Action**        | Upgrade / Override                    |
| **💻 Change**        | `version` -> `fixed_version`          |
| **⚠️ Risk**          | Impact on build / compatibility notes |

---

## When to use this skill

- Use this when you need to fix vulnerabilities in your project dependencies
- This is helpful for securing Node.js projects while maintaining build stability
- Use this to perform professional-grade vulnerability scanning and remediation
- This is ideal for teams that need to maintain security compliance without breaking builds

## How to use it

### Phase 1: The Great Reset

Before scanning, purge the current state to ensure the dependency tree is honest:

1. **Delete Artifacts:**
   - `node_modules/`
   - `package-lock.json`
2. **Purge `package.json`:**
   - Remove existing `"overrides"` or `"resolutions"`.
   - Remove any previous manual "forced" fixes.

> [!TIP]
> Starting from a neutral tree ensures that Snyk identifies the _actual_ root causes, not side effects of previous fix attempts.

### Phase 2: Fresh Foundation & Tooling

Initialize the project and ensure the Snyk CLI is ready:

1. **Validate Snyk CLI:** Check if `snyk` is installed (`snyk --version`).
2. **Auto-Setup:** If not found, install via `npm install -g snyk` or use `npx snyk` as the primary execution method.
3. **Project Install:** Run `npm install` to build the dependency tree.

- **Strict Rule:** **DO NOT** use `--force` or `--legacy-peer-deps`.
- **Requirement:** The installation **must** complete without errors before proceeding.

### Phase 3: Snyk Intelligence (Scan)

Prioritize the **Snyk IDE Extension** or the **Snyk CLI** to extract deep context.

#### AI-Agent Authentication Flow

If scanning as an agent and authentication fails:

1. **Generate URL:** Run `npx snyk auth`.
2. **Provide Link:** Deliver the generated OAuth/Login URL to the USER immediately.
3. **Wait for Confirmation:** Once the USER authenticates in their browser, proceed to scan.

#### Analysis

Analyze the findings and extract the following metadata for each threat:

- **Package:** The specific vulnerable library.
- **Severity:** (Critical, High, Medium, Low).
- **Path:** How it gets into your project (Direct vs. Transitive).
- **Fixed In:** The version that resolves the issue.

> [!TIP]
> Use `npx snyk test --dev` to catch vulnerabilities in build tools (like `jest` or `webpack`) that `npm audit` might miss.

### Phase 4: Surgical Upgrades (Priority 1)

Always try to upgrade before you override:

1. Apply the version change in `package.json`.
2. Run `npm install`.
3. Verify the fix via Snyk Extension.

### Phase 5: Targeted Overrides (The Last Resort)

Apply overrides only when upgrades are not viable.

### Phase 6: Validation & Cleanup

Once the scan returns clean (or acceptable risk):

1. **Final Install:** Run `npm install` one last time.
2. **Final Scan:** Confirm fixes in the Snyk Extension/CLI.
3. **Snyk vs Audit Note:** If `npm audit` still shows warnings but Snyk is 100% clean, the task is considered **SUCCESSFUL**. Do not add more overrides.
4. **Purge:** Delete any `.snyk`, `snyk-test.json`, or temporary logs.

## Forbidden Actions

- **NO** `--legacy-peer-deps` (Ever).
- **NO** `npm audit fix --force` (Destructive).
- **NO** Global overrides (Unless absolutely necessary).
- **NO** Leaving `npm-debug.log` or temp files behind.

## Activation Triggers

- _"fix snyk workflow"_
- _"clean and fix vulnerabilities"_
- _"run secure install flow"_
- _"no rompas el build"_
- _"apply snyk fixes safely"_
