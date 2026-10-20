# Assignment 3 — CodeTrack: Branching Workflow (Add & Verify a Contact Page)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will add a new Contact page to CodeTrack using a clean feature-branch workflow. You will keep each change in a separate commit, prove that your default branch remains unchanged before the merge, and validate the result after merging.

---

# Task 1 — Confirm Repository State and Default Branch

## Goal

Start from a clean default branch (`main` or `master`) and confirm the repository status.

### Evidence

#### Screenshot 1 — Output of `git status` and `git branch` showing a clean status and the default branch checked out

<img width="773" height="155" alt="image" src="https://github.com/user-attachments/assets/f1a3c3cb-f7f5-4d1b-b15a-fdca1534dee2" />



---

# Task 2 — Create and Switch to a Feature Branch

## Goal

Create a branch named exactly `feature/contact-page` and switch to it.

### Evidence

#### Screenshot 2 — Output of `git checkout -b feature/contact-page` and `git branch` showing `* feature/contact-page`

<img width="785" height="155" alt="image" src="https://github.com/user-attachments/assets/2444b6c6-bf03-4336-a213-83056bfd256f" />


---

# Task 3 — Add contact.html on the Feature Branch

## Goal

Create `contact.html` with the provided content and commit it alone using the message `feat(contact): add Contact page`.

### Evidence

#### Screenshot 3 — Output of `ls` showing `contact.html`

<img width="777" height="290" alt="image" src="https://github.com/user-attachments/assets/f617ed45-b6ab-41aa-b427-851e617e88fe" />


---

#### Screenshot 4 — Output of `git commit`

<img width="827" height="171" alt="image" src="https://github.com/user-attachments/assets/4ec582b5-d39a-4caf-85cf-a34f7ea0966d" />


---

#### Screenshot 5 — Output of `git log --oneline -3` showing the new commit

<img width="826" height="152" alt="image" src="https://github.com/user-attachments/assets/831a2e92-4be5-4b82-af69-49eada27c81b" />


---

# Task 4 — Add the Contact Link to index.html

## Goal

Add the provided Contact Page link to `index.html` and commit it separately using the message `feat(nav): add Contact Page link`.

### Evidence

#### Screenshot 6 — Output of `git status` showing `index.html` as modified before staging

<img width="762" height="215" alt="image" src="https://github.com/user-attachments/assets/913e9ac4-2a11-431e-9da0-eb7cd0d17f0d" />


---

#### Screenshot 7 — Output of `git commit`

<img width="820" height="155" alt="image" src="https://github.com/user-attachments/assets/d221f523-48fa-4644-aca9-29ad25da6e0d" />


---

#### Screenshot 8 — Browser showing the Contact Page link on the homepage while on `feature/contact-page`

<img width="1378" height="852" alt="image" src="https://github.com/user-attachments/assets/c097f729-2880-4bde-a6bf-2acb3e632736" />



---

# Task 5 — Verify Isolation (Prove the Default Branch Is Unchanged)

## Goal

Switch back to the default branch and confirm that `contact.html` and the Contact Page link do not exist there yet.

### Evidence

#### Screenshot 9 — Terminal showing the checkout and `ls` output, proving `contact.html` is absent

<img width="830" height="292" alt="image" src="https://github.com/user-attachments/assets/715cb7e9-bd57-4a8c-b9f2-bf8109206294" />


---

#### Screenshot 10 — Browser showing the homepage on the default branch with no Contact Page link

<img width="1220" height="755" alt="image" src="https://github.com/user-attachments/assets/7b2b7c39-0e9c-47f5-8528-45cd732a4dd7" />


---

# Task 6 — Merge the Feature Branch into the Default Branch

## Goal

Merge `feature/contact-page` into your default branch and confirm the Contact page works.

### Evidence

#### Screenshot 11 — Output of `git merge feature/contact-page`

<img width="817" height="203" alt="image" src="https://github.com/user-attachments/assets/9f8d361a-0af3-4d5c-af8d-a1ee68c2d141" />


---

#### Screenshot 12 — Output of `ls` showing `contact.html` after the merge


<img width="788" height="275" alt="Screenshot 2026-10-20 140524" src="https://github.com/user-attachments/assets/fdf75621-ad9f-4ed8-92c5-c805219161bd" />


---

#### Screenshot 13 — Browser showing the Contact page opened from the homepage link on the default branch



<img width="1047" height="587" alt="image" src="https://github.com/user-attachments/assets/26351f7a-6b21-4853-98f2-dfe59302f336" />



---

# Task 7 — Inspect History (Graph View)

## Goal

Display the repository history as a graph and locate both feature commits.

### Evidence

#### Screenshot 14 — Full output of `git log --oneline --graph --decorate --all`


<img width="822" height="297" alt="image" src="https://github.com/user-attachments/assets/73984c6a-b3f5-4af7-9a1f-0e2d89de260e" />


---

# Task 8 — Optional Cleanup (Delete the Feature Branch)

## Goal

Delete the merged `feature/contact-page` branch to keep your branch list clean.

### Evidence

#### Screenshot 15 (Optional) — Output showing `feature/contact-page` deleted and no longer listed


<img width="822" height="153" alt="image" src="https://github.com/user-attachments/assets/15bd9aa7-4c00-4062-acd7-37e9b3129101" />


---

# Submission Instructions

- Tasks 1–7 are required; Task 8 is optional
- Add all required screenshots in your submission
- Evidence must show `contact.html` and the homepage link were absent before merging, and working after merging
- Do not expose passwords, access tokens, or private keys

---

# Completion Checklist

- [ ] Repository confirmed clean on the default branch (Screenshot 1)
- [ ] `feature/contact-page` created and checked out (Screenshot 2)
- [ ] `contact.html` added in its own commit (Screenshots 3–5)
- [ ] Homepage Contact link added in a separate commit (Screenshots 6–8)
- [ ] Default branch proven unchanged before merge (Screenshots 9–10)
- [ ] Feature branch merged and Contact page verified (Screenshots 11–13)
- [ ] Graph history reviewed (Screenshot 14)
- [ ] Optional cleanup completed (Screenshot 15)
- [ ] No sensitive data exposed

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
