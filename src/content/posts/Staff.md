---
title: Staff
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Footprinting
draft: false
---

### **Staff and Social Media Recon**

#### **Why Focus on Employees?**
Employees often *unknowingly expose valuable intel* through:
- Social media posts (especially LinkedIn)
- Public GitHub repos
- Résumés/CVs
- Job listings

---

### **What Can Job Posts Reveal?**

Let’s look at some gold nuggets from the example:

| Tech Area               | Examples from Job Listing                                    |
|------------------------|-------------------------------------------------------------|
| **Languages**          | Java, C#, C++, Python, Ruby, PHP, Perl                      |
| **Databases**          | PostgreSQL, MySQL, SQL Server, Oracle                       |
| **Frameworks**         | Flask, Django, Spring, ASP.NET MVC                          |
| **Version Control**    | Git, SVN, Mercurial, Perforce                               |
| **CI/CD & Agile**      | Agile methodologies, CI tools                               |
| **Security**           | TS/SCI clearance, Security+, Software Security              |
| **DevOps**             | Docker, Kubernetes                                          |
| **Tools**              | Atlassian suite (Jira, Confluence, Bitbucket), Redis, NumPy |

> **Insight**: This gives clues not only about the current stack, but also **future plans**, security expectations, and team composition.

---

### **LinkedIn & Employee Profiling**

LinkedIn profiles can help you:
- Identify who works on **backend/frontend/security**.
- See **tech preferences** (e.g., Python/Django vs. Java/Spring).
- Understand **certifications** and **open-source contributions**.
- Find potential **weak points** like:
  - Outdated libraries mentioned in posts.
  - GitHub projects with sensitive info (e.g., exposed keys or emails).

#### **Example of Misconfiguration Found**
- Hardcoded **JWT token** in a public GitHub repo.
- Public email linked with a real production role.
- This can lead to **token replay attacks**, impersonation, or further pivoting.

---

### **Strategy for Recon via LinkedIn & Job Boards**

1. **Search Filters:**
   - Use LinkedIn filters (Title: “Developer”, “Security Analyst”, “DevOps Engineer”, etc.)
   - Filter by company name and tech keywords.

2. **Look for These Details:**
   - Tech stack mentioned (e.g., “Experienced with Django and Flask”).
   - Repos linked in profile (check for `.env`, `config.py`, or credentials).
   - Certifications (Security+, AWS Certified, etc.)
   - Posts/articles written by the person.

3. **Cross-Reference Job Ads:**
   - Use job listings to **match employees** and tech stack.
   - Helps verify which technologies are really in use.

4. **Check Public Repos:**
   - Look for exposed secrets, misconfigured environments, etc.
   - Examples: GitHub, GitLab, Bitbucket (public repos).

---

### **OSINT Tool Tips**
- **theHarvester** – Email and employee name harvesting.
- **LinkedIn Dorking** – `site:linkedin.com/in "CompanyName" AND "developer"`
- **Hunter.io** – Find corporate email formats.
- **Shodan/Censys** – Match user tech preferences with exposed services.

---

### **Real-World Risks of Oversharing**
- **Security Clearance info** can hint at government contracts (a big target).
- **Hardcoded keys** or **tokens in GitHub** can lead to full breaches.
- **Flask/Django** security misconfigs are **commonly abused** when default settings are left enabled.

---

### Summary

| Area | Insight |
|------|---------|
| Employees | Reveal tools, skills, and even configuration habits. |
| Job Listings | Uncover stack, version control systems, and infrastructure direction. |
| GitHub | Often leaks sensitive information. |
| LinkedIn | A treasure trove for mapping org charts and skills. |
| Passive Recon | Can identify security gaps before even touching the target. |


