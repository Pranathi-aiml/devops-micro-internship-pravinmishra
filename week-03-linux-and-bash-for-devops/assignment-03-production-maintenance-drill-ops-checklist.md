# Assignment 3 — Production Maintenance Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will treat your already deployed React application (on Ubuntu VM with Nginx) as a live production system. You will perform structured operational checks covering network validation, service health, log analysis, resource monitoring, configuration verification, and incident simulation with recovery — mirroring real on-call DevOps responsibilities.

---

# Task 1 — Server Access & Networking Validation

## Goal

Verify that the deployed React application is reachable from the browser and confirm basic network connectivity of the Ubuntu VM.

### Evidence

#### Screenshot 1 — Browser showing the React app with your Full Name visible on the UI

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c6332cd2-ba8a-49b9-8620-f525b797581c" />


---

#### Screenshot 2 — Output of `ip a`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/16e85fab-8755-4d45-b203-8a175c9a8b48" />


---

#### Screenshot 3 — Output of `sudo ss -tulpen`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f1311f45-0021-4ee1-b3cf-32c6d7d5304f" />


---

#### Screenshot 4 — Output of `sudo ufw status`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c60db5d8-b36b-4034-819e-06b06ebc4b7b" />


---

### Notes

Answer the following in your own words:

**1. What proves Nginx is listening on 0.0.0.0:80?**

The sudo ss -tulpen output shows 0.0.0.0:80 in the LISTEN state, and the process is shown as nginx. This proves Nginx is listening for HTTP connections on port 80.

---

**2. What proves SSH is active on port 22?**

The sudo ss -tulpen output shows 0.0.0.0:22 in the LISTEN state, with the process shown as sshd. This proves SSH is active on port 22.

---

**3. Did you find any unexpected open ports? Explain briefly.**

No, I did not find any unexpected open ports. The main listening ports were 22 for SSH and 80 for Nginx/HTTP. The other listed ports were used by normal system services such as DNS and time synchronization.

---

# Task 2 — Service Health & Systemd Validation (Nginx)

## Goal

Verify that Nginx is properly installed, running, enabled at boot, and safely configured.

### Evidence

#### Screenshot 1 — Output of `systemctl status nginx --no-pager`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/df7428ad-4fdd-44fb-a3de-8c86656c5606" />


---

#### Screenshot 2 — Output of `sudo nginx -t`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d07d4350-12a1-45d4-8a39-f976e24d7b30" />


---

#### Screenshot 3 — Output of `sudo ss -lptn '( sport = :80 )'`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d6f97aed-0831-494d-aaca-490592898264" />


---

### Notes

Answer the following in your own words:

**1. What happens if Nginx fails to restart in production?**

If Nginx fails to restart, the website may become unavailable, and users may not be able to access the application. I would check the Nginx status and configuration errors, fix the issue, and restart Nginx safely.

---

**2. What's your basic rollback plan?**

My basic rollback plan is to restore the previous working configuration or application files, test the Nginx configuration using nginx -t, and then restart Nginx. This helps bring the website back to the last known working state.

---

# Task 3 — Logs & Request Trace

## Goal

Verify real traffic flow and analyze logs to understand system behavior and errors.

### Evidence

#### Screenshot 1 — Output of `sudo tail -n 30 /var/log/nginx/access.log`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ced0c4f9-fb5b-40b9-a7d6-b9976f6dbe42" />


---

#### Screenshot 2 — Output of `sudo tail -n 30 /var/log/nginx/error.log`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b83acc23-042a-4ea3-b4c8-15181e584d32" />


---

#### Screenshot 3 — Output of `sudo journalctl -u nginx --no-pager -n 50`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6974de20-1120-4938-a159-945de5c6e617" />


---

### Notes

Answer the following in your own words:

**1. Were there any errors in the logs?**

- If yes, mention 1–2 example error lines from the logs and explain what each one means in simple terms.
- If no, explain what it means if the error log is empty or shows no recent errors during your check.

No major errors were found during my check. The Nginx error log only showed a notice message about using inherited sockets, which is an informational message and not a failure. The Nginx service logs also showed that the service started and reloaded successfully.

---

**2. If there were no errors, what does that indicate about the system?**

It indicates that Nginx is running normally and there are no recent serious configuration or service errors. The web server appears to be functioning correctly.

---

**3. Based on the access logs, were your curl requests visible in the log entries? What does that prove about traffic flow?**

Yes, the HTTP requests were visible in the Nginx access log. The log showed requests such as GET / and requests for the JavaScript and CSS files, with successful 200 or 304 responses. This proves that traffic is reaching the EC2 server and Nginx is receiving and processing the requests.

---

# Task 4 — System Resource Health Check (Capacity Red Flags)

## Goal

Assess server capacity and detect potential performance or failure risks.

### Evidence

#### Screenshot 1 — Output of `uptime`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/dfc035cb-7116-47d2-9752-4f10e33d222c" />


---

#### Screenshot 2 — Output of `free -h`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/16fbaf03-4d9e-4d84-9d08-edfa68cbd811" />


---

#### Screenshot 3 — Output of `df -h`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e07a5d0d-df01-46d7-8c84-6d5362b88d35" />


---

#### Screenshot 4 — Output of `sudo du -sh /var/* | sort -h`

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. Which resource looks most critical right now? (CPU/load, memory, or disk) Explain why.**

Write your answer here.

---

**2. What happens if disk becomes 100% full in a production server?**

Write your answer here.

---

# Task 5 — Configuration & Deployment Verification

## Goal

Ensure the correct React build is deployed and Nginx is serving it properly.

### Evidence

#### Screenshot 1 — Output of `ls -lah /var/www/html | head -n 20`

Add your screenshot here.

---

#### Screenshot 2 — Output of `grep -R "Deployed by" -n /var/www/html 2>/dev/null | head`

Add your screenshot here.

---

#### Screenshot 3 — Output of `grep -n "try_files" /etc/nginx/sites-available/default`

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. How do you confirm that the correct version of the application is deployed?**

Write your answer here.

---

# Task 6 — Nginx Configuration Failure Simulation

## Goal

Simulate a real-world Nginx misconfiguration and recover the service safely.

### Evidence

#### Screenshot 1 — Output of `sudo nginx -t` showing the syntax error (broken config)

Add your screenshot here.

---

#### Screenshot 2 — Output of `sudo nginx -t` showing syntax ok (fixed config)

Add your screenshot here.

---

#### Screenshot 3 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What caused the configuration failure?**

Write your answer here.

---

**2. How did you fix the issue?**

Write your answer here.

---

**3. How can you avoid this kind of issue in real production systems?**

Write your answer here.

---

# Task 7 — Web Application Failure Simulation

## Goal

Simulate missing deployment content and recover the application safely.

### Evidence

#### Screenshot 1 — Output of `curl -I http://<public-ip>` showing failure (non-200 response)

Add your screenshot here.

---

#### Screenshot 2 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What caused the application to break in this scenario?**

Write your answer here

---

**2. How did you fix the issue and restore the application?**

Write your answer here.

---

**3. What steps would you take to prevent this kind of issue in real production systems?**

Write your answer here.

---

# Task 8 — Security & Reliability Review

## Goal

Review and reflect on the security and reliability practices applied during this assignment.

### Security & Reliability Notes

Answer the following in your own words:

**1. Why is SSH key-based authentication more secure than sharing passwords?**

Write your answer here.

---

**2. Why should only required ports be open on a production server?**

Write your answer here.

---

**3. Why is it important for Nginx to be enabled on boot?**

Write your answer here.

---

**4. What are the risks of sharing secrets, keys, or credentials publicly?**

Write your answer here.

---

**5. Why should cloud resources be stopped or terminated when they are no longer needed?**

Write your answer here.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot — Published LinkedIn post

Add your screenshot here.

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Task 1: Screenshots (browser, ip a, ss -tulpen, ufw status) + Notes answered
- [ ] Task 2: Screenshots (nginx status, nginx -t, ss port 80) + Notes answered
- [ ] Task 3: Screenshots (access log, error log, journalctl) + Notes answered
- [ ] Task 4: Screenshots (uptime, free -h, df -h, du -sh) + Notes answered
- [ ] Task 5: Screenshots (ls html, grep deployed by, grep try_files) + Notes answered
- [ ] Task 6: Screenshots (nginx -t fail, nginx -t pass, curl recovery) + Notes answered
- [ ] Task 7: Screenshots (curl failure, curl recovery) + Notes answered
- [ ] Task 8: Security & Reliability Notes answered
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots
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
