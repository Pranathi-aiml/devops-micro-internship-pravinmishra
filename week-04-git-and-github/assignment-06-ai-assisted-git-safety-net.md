# Assignment 6 — Building an AI-Assisted Git Safety Net (PR Ready Check)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In Week 2 you built Claude Code hooks that block a dangerous action *before* it happens (`PreToolUse`), and a restricted skill that could look but not touch (`allowed-tools` without `Write`). In this assignment you will discover that Git has the exact same idea, decades older: a **pre-commit hook** that blocks a commit before it's created.

You will build both halves of a real "PR Ready" workflow:

1. A **Git hook that follows fixed rules** — scans staged changes for hardcoded secrets and oversized files and refuses the commit. No AI involved, no guessing, just a rule that gives the same answer every time.
2. A **restricted Claude Code skill** (`/pr-ready`) that reads your staged diff and drafts a Pull Request title, description, and a short list of things worth a second look — the kind of judgment a fixed rule can't make (mixed changes, missing context, unclear intent). The skill never commits, pushes, or opens the PR. You do that yourself, using its draft as a starting point.

This mirrors the Agentic Loop from Week 3's Linux triage assignment: **Gather → Analyze → Human Act → Verify**. The hook and the skill both gather and analyze; only you act.

---

# Task 0 — Confirm Your Fork and Create a Feature Branch

## Goal

Confirm you are working in your own fork, then create a dedicated branch for this assignment.

### Evidence

#### Screenshot 1 — Output of git remote -v and git branch showing the new branch

<img width="907" height="245" alt="image" src="https://github.com/user-attachments/assets/d33fc638-6c71-40d4-8cd8-7fd5d9fb57dd" />


---

### Notes

**1. Why create a dedicated branch instead of doing this work on main?**

A dedicated feature branch keeps assignment changes separate from the main branch. It allows me to develop and test the Git pre-commit safety hook and restricted Claude Code skill without affecting stable code. After testing, the changes can be reviewed and merged through a Pull Request.

---

# Task 1 — Stage a Change With Realistic Risk

## Goal

On your own fork of this repository (the one you've been submitting your DMI work in since onboarding), create a new branch and stage a change that a real reviewer should catch: a hardcoded-looking secret and a leftover debug statement.

### Evidence

#### Screenshot 1 — Output of  `git status` showing the staged file on feature/ai-pr-ready

<img width="683" height="195" alt="image" src="https://github.com/user-attachments/assets/ed54fae2-e9da-44b9-b2d8-d3d05be64ded" />


---

### Notes

**1. Why does this assignment use an obviously fake key instead of a real one?**

This assignment uses an obviously fake key to safely test the pre-commit hook without exposing real credentials. Real API keys or passwords could be stolen or misused if committed to a Git repository. A fake key allows me to verify that the safety check detects secret-like patterns without risking sensitive information.

---

# Task 2 — Write a Real Git Pre-Commit Hook

## Goal

Create a tracked, shareable pre-commit hook that blocks a commit containing secret-like patterns or files over 1MB.

### Evidence

#### Screenshot 2 — `hooks/pre-commit` open in VS Code showing the full script

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bef8960a-3544-47a1-a76e-8cb169b62bec" />


---

#### Screenshot 3 — Output of `git config core.hooksPath` confirming it points to `hooks`

<img width="817" height="216" alt="image" src="https://github.com/user-attachments/assets/9059c6e9-c535-4efe-8efc-54319e50678b" />


---

### Notes

**1. Why is `hooks/pre-commit` tracked in the repo instead of living only in `.git/hooks/`?**

hooks/pre-commit is tracked in the repository so it can be shared with other developers and version-controlled. Files inside .git/hooks/ are local to one developer's computer and are not shared when the repository is cloned. Keeping the hook in the repository makes it easier for everyone to use and maintain the same safety checks.

---

**2. Compare this to `PreToolUse` from Week 2 Assignment 6. What does each one intercept, and what do they have in common?**

A Git pre-commit hook intercepts a Git commit before it is created and can block it if staged files contain secret-like patterns or files larger than 1 MB. The PreToolUse hook intercepts a tool call made by the AI agent before the tool executes and can block unsafe actions.

---

# Task 3 — Prove the Hook Blocks the Risky Commit

## Goal

Attempt to commit the staged file from Task 1 and show the hook rejecting it.

### Evidence

#### Screenshot 4 — Terminal showing `git commit` rejected with the hook's "BLOCKED" message naming the exact file

<img width="912" height="116" alt="image" src="https://github.com/user-attachments/assets/c1e3f866-2238-4da5-8c5b-dabf3a55f3e1" />


---

### Notes

**1. Which line in `hooks/pre-commit` matched your fake key, and why did it match?**

'(API_KEY|SECRET_KEY|PASSWORD|ACCESS_TOKEN)[[:space:]]*=[[:space:]]*["'\''][^"'\'']+["'\'']'
It matched API_KEY = "FAKE_TEST_KEY_123456789" because the variable name API_KEY is in the pattern, followed by an equals sign and a non-empty value inside quotes. Therefore, the hook detected a possible secret and blocked the commit.

---

**2. Could this hook have caught a poorly-named variable that stores a secret without the `AKIA` prefix? What does that tell you about the limits of a fixed rule like this?**

No, not necessarily. The hook checks only for specific variable names such as API_KEY, SECRET_KEY, PASSWORD, and ACCESS_TOKEN. A secret stored in a poorly named variable might bypass this rule, even if it does not have the AKIA prefix. This shows that fixed rules have limitations and cannot detect every secret. More advanced secret-scanning tools and code reviews can help catch additional cases.

---

# Task 4 — Build the `/pr-ready` Skill

## Goal

Create a manually invoked Claude Code skill that reads your staged changes and produces a PR-readiness report and a draft PR description — without writing, committing, or pushing anything itself.

### Evidence

#### Screenshot 5 — `SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no `Write`) and `disable-model-invocation: true`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/15008012-52fb-4eda-94d1-f66b5abac8fe" />


---

#### Screenshot 6 — `/pr-ready` output while the risky file is still staged, showing it flagged the secret and/or debug statement

<img width="1405" height="436" alt="image" src="https://github.com/user-attachments/assets/73aa89df-6244-4b5b-b14b-8272e4fb9fb6" />


---

### Notes

**1. Why does `/pr-ready` have `Bash` and `Read` but not `Write`?**

Bash allows /pr-ready to run read-only Git commands, such as git status and git diff --cached, to inspect staged changes. Read allows it to read files, and Grep helps search for suspicious patterns. Write is excluded because the skill should only review changes and generate a report and draft PR description. It must not modify files, ensuring the review is safe and read-only.

---

**2. The pre-commit hook and `/pr-ready` both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?**

Both were designed to detect the fake API key and debug statement in README.md. The pre-commit hook successfully detected the possible secret and blocked the commit. The /pr-ready skill was intended to provide a broader review, including debug statements, potential bugs, whitespace issues, and PR readiness. However, because Claude Code returned an API error, /pr-ready did not complete its review, so I could not confirm which additional issues it would have caught.

---

# Task 5 — Fix the Issues and Re-Verify

## Goal

Remove the secret and debug statement, then prove both gates now pass clean.

### Evidence

#### Screenshot 7 — `git commit` succeeding after the fix (no BLOCKED message)

<img width="891" height="195" alt="Screenshot 2026-10-22 090131" src="https://github.com/user-attachments/assets/f5009b06-5b2e-492f-9ce4-3aa34c22a8ac" />


---

#### Screenshot 8 — Second `/pr-ready` run showing a clean risk report and a drafted PR title + description

<img width="1363" height="880" alt="download (1)2" src="https://github.com/user-attachments/assets/5494bded-c240-4c7a-8d2f-d3e4e4637d76" />


---

### Notes

**1. What exactly did you change to satisfy the pre-commit hook?**

I removed the fake API key (API_KEY = "FAKE_TEST_KEY_123456789"), the temporary debug statement (print("DEBUG: temporary diagnostic output")), and the temporary safety-hook test comment from README.md. Then I staged the cleaned file again and retried the commit. The pre-commit hook passed, and the commit was successful.

---

# Task 6 — Push and Open a Pull Request Using the AI Draft

## Goal

Push your branch and open a real Pull Request, using `/pr-ready`'s drafted title and description as your starting point — read it critically and edit before you use it.

**Important:** Open this Pull Request with base repository set to **your own fork** — not the shared upstream `pravinmishraaws/devops-micro-internship-pravinmishra` repository. This assignment's hook and skill files are your own practice work, not a change meant for the shared class repo.

### Evidence

#### Screenshot 9 — Your Pull Request showing the base repository is your own fork, plus the title and description, with the `/pr-ready` draft visible for comparison (paste it in the PR conversation or your notes below)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/45777dd4-d9c7-4849-87c8-f98ad2ca8910" />


---

#### PR Link

https://github.com/Pranathi-aiml/devops-micro-internship-interviews/pull/1

---

### Notes

**1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?**

I edited the AI's draft to make the summary, validation steps, and notes match my actual changes. I included the pre-commit safety hook and the pr-ready skill, and clarified that the automated /pr-ready report was not successfully generated, so the description was reviewed manually. This keeps the PR description accurate and honest.

---

**2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?**

The AI might include incorrect claims, miss security risks, or describe changes that were not actually made or tested. This could mislead reviewers and reduce trust in the project. Therefore, I reviewed the title and description before creating the Pull Request.

---

**3. Why does this PR need to target your own fork instead of the shared upstream repository?**

This PR contains my personal practice work for the DevOps Micro Internship, including the pre-commit hook and the pr-ready skill. Targeting my own fork keeps these changes separate from the shared class repository and avoids submitting practice changes directly to the upstream project without permission.

---

# Task 7 — Map the Workflow to the Agentic Loop

## Goal

Explain this assignment's workflow using the same Gather → Analyze → Human Act → Verify structure from Week 3.

### Notes

**1. Which step(s) represent Gather?**

Gather is the step where I collect information about the repository and staged changes using commands such as git status --short and git diff --cached. The pre-commit hook also gathers staged file content to check for possible secrets and files larger than 1 MB.

---

**2. Which step(s) represent Analyze?**

Analyze happens when the pre-commit hook checks staged files against fixed rules and when the pr-ready AI skill reviews the changes for possible secrets, bugs, missing tests, and other risks. The AI skill then produces a readiness verdict and drafts the PR title and description.

---

**3. Which step is Human Act, and why must a human — not Claude — run `git commit`, `git push`, and open the PR?**

Human Act is the step where I review the AI's findings, edit the PR description, run git commit and git push, and open the Pull Request. A human must control these actions because they can change repository history, publish code, and create a real review request. Human approval helps prevent unintended or unsafe changes.

---

**4. Which step is Verify?**

Verify is the step where I check whether the pre-commit hook blocks suspicious content, confirm that the hook passes after removing the test content, run git diff --cached --check, and inspect the GitHub Pull Request to confirm the correct repository, branches, title, and description.

---

**5. In one or two sentences: why do you need *both* the fixed-rule pre-commit hook and the AI skill? Isn't one enough?**

The pre-commit hook enforces specific rules consistently, such as detecting secret-like patterns and files larger than 1 MB, while the AI skill can reason about broader issues such as bugs, incomplete changes, and missing tests. Both are needed because fixed rules are predictable but limited, whereas AI review is flexible but can miss issues or make mistakes.

---

# Task 8 — LinkedIn Post

## Goal

Publish a LinkedIn post summarizing what you built and what you learned about combining fixed-rule safety checks with AI-assisted review.

### Evidence

#### LinkedIn Post URL

Add your LinkedIn post URL here...

---

## Key Learnings

Add 3-5 bullet points on what you learned this week.

-
-
-

---

# Submission Instructions

- Ensure `hooks/pre-commit` and `.claude/skills/pr-ready/SKILL.md` are committed to your GitHub repository
- Add all required screenshots to your submission
- All written answers must be in your own words
- Do not use a real secret or credential anywhere in your submission — the fake key in Task 1 is intentional and must stay clearly fake
- Open your Pull Request against your own fork, not the shared upstream repository
- Push your final changes to your forked repository
- Include your PR link and LinkedIn post URL

---

## GitHub Repository URL

Paste your forked repository URL here:

`Add your URL here`

---

# Completion Checklist

- [ ] Branch `feature/ai-pr-ready` created with a staged file containing a fake secret and a debug statement
- [ ] `hooks/pre-commit` created and tracked in the repo (not only in `.git/hooks/`)
- [ ] `core.hooksPath` configured to point at `hooks/`
- [ ] Pre-commit hook shown blocking the risky commit
- [ ] `.claude/skills/pr-ready/SKILL.md` created with correct `allowed-tools` (no `Write`) and `disable-model-invocation: true`
- [ ] `/pr-ready` run against the risky diff and shown flagging issues
- [ ] Risky file fixed; `git commit` succeeds cleanly
- [ ] `/pr-ready` re-run showing a clean report and drafted PR title/description
- [ ] Pull Request opened using the AI draft as a starting point, with your own fork as the base repository (not upstream), PR link included
- [ ] Agentic Loop mapping (Task 7) completed in your own words
- [ ] LinkedIn post published and URL submitted
- [ ] All required screenshots added
- [ ] GitHub repository URL provided

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
