# Assignment 5 — Bash Script Automation Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will practice Bash scripting by building a series of small automation scripts covering environment setup, variables, arrays, loops, file conditionals, if-else logic, and functions. These scripts form the foundation of real-world Linux automation used in DevOps, cloud, and production support environments.

---

# Task 1 — Bash Environment & Workspace Setup

## Goal

Verify that Bash is available on your system and create a clean workspace for this assignment.

### Evidence

#### Screenshot 1 — Output of `echo $SHELL` and `bash --version`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/611b0d1f-9c3e-4655-974b-f601c485d200" />


---

#### Screenshot 2 — Output of `pwd` and `ls -lah` showing the scripts directory

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f9867d37-9a0f-447d-ab57-9812e2ea2f71" />


---

### Notes

Answer the following in your own words:

**1. What is Bash?**

Bash stands for Bourne Again Shell. It is a command-line interpreter that allows us to interact with the operating system by typing commands. It can also execute scripts to automate repetitive tasks.

---

**2. What is the difference between shell and Bash?**

A shell is a general program that accepts commands from users and communicates with the operating system. Bash is one specific type of shell. Other examples of shells include Zsh, Fish, and Dash.

---

**3. Why is it important to confirm the Bash version before writing scripts?**

Checking the Bash version helps us confirm that the required features and commands are supported. Different versions may support different features, so checking the version helps avoid compatibility problems and script errors.

---

# Task 2 — Your First Bash Script

## Goal

Create your first Bash script, make it executable, and run it from the terminal.

### Evidence

#### Screenshot 1 — Content of `first-script.sh`

<img width="1110" height="452" alt="image" src="https://github.com/user-attachments/assets/ff586a00-fe73-42d7-b9cc-50873c228c0f" />


---

#### Screenshot 2 — Output of `./first-script.sh`

<img width="1026" height="167" alt="image" src="https://github.com/user-attachments/assets/aa442758-ea58-41e8-aea9-da10310e375e" />


---

#### Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission

<img width="1042" height="66" alt="image" src="https://github.com/user-attachments/assets/78afa329-9403-4150-b036-ef9f645dd347" />


---

### Notes

Answer the following in your own words:

**1. What is the purpose of `#!/bin/bash`?**

#!/bin/bash is called a shebang. It tells the operating system to use the Bash interpreter to execute the script.

---

**2. Why do we use `chmod +x` before running a script?**

We use chmod +x to give a file executable permission. This allows us to run the script directly using ./script.sh.

---

**3. What is the difference between running a script using `./script.sh` and `bash script.sh`?**

./script.sh runs the script directly and requires executable permission.

bash script.sh runs the script through Bash and does not require executable permission, as long as the file can be read.

---

# Task 3 — Variables: User Information Script

## Goal

Use variables to store and display user-related information.

### Evidence

#### Screenshot 1 — Content of `user-info.sh`

<img width="572" height="453" alt="image" src="https://github.com/user-attachments/assets/f509400f-1a0c-4eaf-ae5b-d9ce969a3a9f" />


---

#### Screenshot 2 — Output of `./user-info.sh`

<img width="872" height="198" alt="image" src="https://github.com/user-attachments/assets/1a05d7ca-d074-4f37-a1fa-f6aa22a5e867" />


---

### Notes

Answer the following in your own words:

**1. What is a variable in Bash?**

A variable in Bash is a named storage location used to store data such as text, numbers, or other values. For example, name="Pranathi" stores the text Pranathi in the variable name.

---

**2. Why should we avoid spaces around the `=` sign when creating variables?**

Bash does not allow spaces around the = sign when assigning a value to a variable. For example, name="Pranathi" is correct, but name = "Pranathi" is incorrect because Bash treats the parts as separate commands or arguments.

---

**3. How do you access the value stored inside a Bash variable?**

We use the $ symbol followed by the variable name to access its value. For example, if we write name="Pranathi", then echo "$name" displays Pranathi.

---

# Task 4 — Arrays & Loops: Tools Checklist Script

## Goal

Use arrays and loops to print a checklist of tools used in Bash scripting.

### Evidence

#### Screenshot 1 — Content of `tools-checklist.sh`

<img width="602" height="477" alt="image" src="https://github.com/user-attachments/assets/a1d31ed8-fcdd-4ab3-8df2-da9bddd22684" />


---

#### Screenshot 2 — Output of `./tools-checklist.sh`

<img width="952" height="235" alt="image" src="https://github.com/user-attachments/assets/4d2c4506-984c-4eee-9c27-063074d577dd" />


---

### Notes

Answer the following in your own words:

**1. What is an array in Bash?**

An array in Bash is a variable that can store multiple values under a single name. For example, tools=("Bash" "Git" "Docker") stores three tool names in one array.

---

**2. Why are arrays useful in scripts?**

Arrays are useful because they let us store and manage multiple values together. We can use loops to process each value, which reduces repeated code and makes scripts easier to maintain.

---

**3. What does `"${tools[@]}"` mean?**

"${tools[@]}" is used to access all the elements in the tools array. It allows a loop to process each tool name separately, including values that contain spaces.

---

**4. What is the purpose of the `for` loop in this script?**

The for loop is used to go through each element in the tools array one by one and print each tool as a checklist item. It avoids writing a separate echo command for every tool.

---

# Task 5 — Loops: Number Counter Script

## Goal

Use loops to repeat a task multiple times.

### Evidence

#### Screenshot 1 — Content of `counter.sh`

<img width="442" height="352" alt="image" src="https://github.com/user-attachments/assets/28b5926f-0312-4943-aab6-361023d77b77" />


---

#### Screenshot 2 — Output of `./counter.sh`

<img width="815" height="337" alt="image" src="https://github.com/user-attachments/assets/e85fbc8f-65dc-409d-aaa5-2fe0879907b7" />


---

### Notes

Answer the following in your own words:

**1. What is a loop?**

A loop is a programming structure that repeats a set of instructions multiple times until a condition is met or the loop finishes.

---

**2. Why do we use loops in Bash scripting?**

We use loops to repeat tasks automatically without writing the same commands again and again. This makes scripts shorter, easier to read, and more efficient.

---

**3. How many times did the loop run in your script?**

The loop ran 10 times, counting from 1 to 10.

---

**4. What would you change if you wanted the loop to run 10 times?**

In my script, the loop already runs 10 times because the condition is i<=10. If I wanted to change the number of repetitions, I would modify the loop condition.

---

# Task 6 — Files & Conditionals: File Validation Script

## Goal

Use file checks and conditionals to verify whether files and directories exist.

### Evidence

#### Screenshot 1 — Output of `ls -lah ../test-folder`

<img width="861" height="157" alt="image" src="https://github.com/user-attachments/assets/46758790-39fd-4313-bec2-575eaa38628b" />


---

#### Screenshot 2 — Content of `file-check.sh`

<img width="685" height="491" alt="image" src="https://github.com/user-attachments/assets/4130754a-168d-4f01-b0ff-7553b01f66be" />


---

#### Screenshot 3 — Output of `./file-check.sh`

<img width="912" height="157" alt="image" src="https://github.com/user-attachments/assets/5416fb8b-3bef-48ac-8314-22a173d6c385" />


---

### Notes

Answer the following in your own words:

**1. What does `-d` check in Bash?**

-d checks whether a directory exists at the given path.


**2. What does `-f` check in Bash?**

-f checks whether a regular file exists at the given path.


**3. Why should file and directory paths be stored in variables?**

Storing paths in variables makes the script easier to read, update, and reuse.


**4. What happens if the file does not exist?**

If the file does not exist, the -f condition returns false, and the script executes the else block if one is provided.

# Task 7 — Conditionals: Pass or Retry Script

## Goal

Use if-else conditionals to make decisions based on a variable value.

### Evidence

#### Screenshot 1 — Content of `score-check.sh` with `score=85`

<img width="495" height="375" alt="image" src="https://github.com/user-attachments/assets/4ed9c0a3-7885-443c-b938-1bc41ae731a1" />


---

#### Screenshot 2 — Output showing `Result: Pass`

<img width="897" height="252" alt="image" src="https://github.com/user-attachments/assets/3c2f6825-1945-46f6-98e3-09f7eda2b863" />


---

#### Screenshot 3 — Content of `score-check.sh` with `score=55`

<img width="503" height="392" alt="image" src="https://github.com/user-attachments/assets/f8da7511-4759-46d6-b81a-2594e3a44e3d" />


---

#### Screenshot 4 — Output showing `Result: Retry`

<img width="801" height="247" alt="image" src="https://github.com/user-attachments/assets/c61dff18-acc7-4410-9822-0728ede488fb" />


---

### Notes

Answer the following in your own words:

**1. What is the purpose of if-else in Bash?**

The if-else statement helps a script make decisions based on whether a condition is true or false.

---

**2. What does `-ge` mean?**

-ge means “greater than or equal to.” For example, [ "$score" -ge 60 ] checks whether the score is at least 60.

---

**3. Why should conditions be tested with different values?**

Testing different values helps us check whether the script produces the correct result in different situations.

---

**4. How can conditionals help in automation scripts?**

Conditionals help automation scripts make decisions automatically, such as checking files, validating scores, and deciding whether to continue or stop a task.

---

# Task 8 — Functions: Final Bash Automation Script

## Goal

Create a final Bash script using functions to organize reusable code.

### Evidence

#### Screenshot 1 — Content of `final-automation.sh`

<img width="718" height="621" alt="image" src="https://github.com/user-attachments/assets/2e2186b3-b20e-4d58-b57b-a3a1dad23873" />

---

#### Screenshot 2 — Output of `./final-automation.sh`

<img width="927" height="505" alt="image" src="https://github.com/user-attachments/assets/1e6ecdbd-ccb4-4ab5-83ee-cac59b94a714" />


---

#### Screenshot 3 — Output of `ls -lah` showing all created scripts


<img width="791" height="273" alt="image" src="https://github.com/user-attachments/assets/b5424e38-918e-4bfe-9bca-45537c2f5a00" />


---

### Notes

Answer the following in your own words:

**1. What is a function in Bash?**

A function in Bash is a block of code that performs a specific task and can be called whenever needed.

---

**2. Why are functions useful in scripts?**

Functions help organize code, avoid repeating the same code, and make scripts easier to read, reuse, and maintain.

---

**3. Which functions did you create in this script?**

I created four functions: show_info(), show_tools(), check_files(), and check_score(). I also created a main() function to call these functions in order.

---

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

The script uses variables to store information, an array to store DevOps tool names, a loop to display the tools, conditionals to check files and validate a score, and functions to organize the different tasks into reusable blocks of code.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

https://www.linkedin.com/posts/pranathi-kummari-213641425_devops-bashscripting-linux-share-7516810220694798336--2t2/?utm_source=share&utm_medium=member_desktop&rcm=ACoAAGvFY-8BHygXK5EkHCp2QWk-eDvXi6Zgzt0

---

#### Screenshot — Published LinkedIn post


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7ac2099c-ed71-466d-adea-ef660839f78c" />


---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- All script files must be created and run successfully
- Required notes must be answered clearly for every task
- Do not expose sensitive information (keys, passwords, credentials)

---

# Completion Checklist

- [ ] Task 1: Environment setup verified, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: First script created, executed, permissions verified (Screenshots 1–3, Notes answered)
- [ ] Task 3: Variables script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 4: Arrays and loops script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 5: Counter loop script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 6: File validation script created and run (Screenshots 1–3, Notes answered)
- [ ] Task 7: Pass/Retry conditional script tested with both values (Screenshots 1–4, Notes answered)
- [ ] Task 8: Final automation script created and run (Screenshots 1–3, Notes answered)
- [ ] All scripts run without errors
- [ ] Full Name visible in all required screenshots
- [ ] LinkedIn post published and URL submitted
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
