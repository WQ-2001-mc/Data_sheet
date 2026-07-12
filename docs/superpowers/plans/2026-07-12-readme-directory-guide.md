# Data_sheet README Directory Guide Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a concise Chinese repository guide and preserve every current local manual-category directory on GitHub.

**Architecture:** A root `README.md` is the single human-readable index for the repository. Empty category directories are represented by `.gitkeep` files because Git does not track directories by themselves.

**Tech Stack:** Markdown, Git

## Global Constraints

- Do not modify `相机手册/结构光/gemini深度相机规格书.pdf`.
- Do not include files from the parent `/Users/hanxiaobo/Desktop/codex` repository.
- Keep the README concise and written in Chinese.
- Push the final result directly to `main` and verify the remote commit SHA.

---

### Task 1: Add the repository directory guide

**Files:**
- Create: `README.md`
- Create: `FPGA开发板手册/.gitkeep`
- Create: `红外散斑投影器/.gitkeep`
- Create: `相机手册/IR相机/.gitkeep`
- Verify existing: `芯片手册/.gitkeep`
- Verify existing: `相机手册/tof/.gitkeep`
- Verify existing: `相机手册/结构光/gemini深度相机规格书.pdf`

**Interfaces:**
- Consumes: the directory layout approved in `docs/superpowers/specs/2026-07-12-readme-directory-guide-design.md`
- Produces: a GitHub-rendered repository overview whose paths match the committed Git tree

- [ ] **Step 1: Create the README and empty-directory markers**

Create `README.md` with this exact content:

```markdown
# Data_sheet

本仓库用于分类整理和保存硬件设备的数据手册、规格书及相关技术资料，便于统一查找和持续维护。

## 目录结构

\`\`\`text
.
├── FPGA开发板手册/
├── 红外散斑投影器/
├── 芯片手册/
└── 相机手册/
    ├── IR相机/
    ├── tof/
    └── 结构光/
        └── gemini深度相机规格书.pdf
\`\`\`

## 目录说明

- `FPGA开发板手册/`：存放 FPGA 开发板的用户手册、硬件说明和规格资料。
- `红外散斑投影器/`：存放红外散斑投影器的规格书及相关技术资料。
- `芯片手册/`：存放各类芯片的数据手册和参考资料。
- `相机手册/`：按相机类型分类保存设备资料。
  - `IR相机/`：红外相机相关资料。
  - `tof/`：ToF（飞行时间）深度相机相关资料。
  - `结构光/`：结构光深度相机相关资料，目前收录 Gemini 深度相机规格书。

## 当前资料

- [`相机手册/结构光/gemini深度相机规格书.pdf`](相机手册/结构光/gemini深度相机规格书.pdf)

## 维护说明

新增资料时，请放入对应分类目录；若增加新的设备类别，请同步更新本 README 中的目录结构和说明。
```

Create empty files at:

```text
FPGA开发板手册/.gitkeep
红外散斑投影器/.gitkeep
相机手册/IR相机/.gitkeep
```

- [ ] **Step 2: Verify content and scope before committing**

Run:

```bash
git diff --check
git status --short
test -f README.md
test -f FPGA开发板手册/.gitkeep
test -f 红外散斑投影器/.gitkeep
test -f 相机手册/IR相机/.gitkeep
test -f 相机手册/结构光/gemini深度相机规格书.pdf
```

Expected: `git diff --check` returns no output; `git status --short` lists only the plan, README, and three intended `.gitkeep` files; every `test` exits with status 0.

- [ ] **Step 3: Commit the implementation**

Run:

```bash
git add README.md FPGA开发板手册/.gitkeep 红外散斑投影器/.gitkeep 相机手册/IR相机/.gitkeep docs/superpowers/plans/2026-07-12-readme-directory-guide.md
git diff --cached --check
git diff --cached --stat
git commit -m "添加资料目录说明"
```

Expected: the cached diff has no whitespace errors and the commit contains the README, three new directory markers, and this implementation plan.

- [ ] **Step 4: Push and verify the remote branch**

Run:

```bash
git push origin main
git rev-parse HEAD
git ls-remote origin refs/heads/main
git status -sb
```

Expected: local `HEAD` and remote `refs/heads/main` print the same 40-character SHA; status reports `main...origin/main` with no uncommitted changes.
