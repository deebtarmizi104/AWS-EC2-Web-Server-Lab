# 🌐 AWS EC2 Web Server Lab

This repository contains my work for the **Parallel and Distributed Computing** course for **Master of Data Science (MDS)**.  
It demonstrates how to deploy a **static HTML webpage** (a personal CV-style page) on an **AWS EC2 instance** using the **Apache2 web server**.

The project highlights essential cloud-based deployment concepts from the Parallel and Distributed Computing syllabus, focusing on distributed resource utilization and server configuration.

---

## 🎯 Project Objectives

- Launch and configure an **AWS EC2 instance** running **Ubuntu Server**.  
- Install and manage the **Apache2 web server**.  
- Replace the default Apache page with a **custom HTML/CSS webpage**.  
- Understand the basics of **distributed web hosting** and **remote access**.  
- Integrate **GitHub** and **VS Code** for continuous deployment and version control.

---

## 🏗️ Project Overview

This project showcases:
- A **dark-themed CV page** featuring interactive accordion sections (Experience, Education, Certifications, and Skills).  
- Use of **Font Awesome icons** for design enhancement.  
- Deployment and testing of a custom webpage on an **AWS EC2 public IP**.  
- Hands-on configuration of the Apache2 service and Linux file management.  
- A reproducible development-to-deployment workflow using **VS Code → GitHub → EC2**.

---

## 🛠️ Technologies & Tools

| Category | Tools / Technologies |
|-----------|----------------------|
| Cloud Platform | AWS EC2 |
| Operating System | Ubuntu 22.04 LTS |
| Web Server | Apache 2 |
| Frontend | HTML 5, CSS 3, JavaScript |
| Development Environment | Visual Studio Code |
| Version Control | Git + GitHub |
| Libraries | Font Awesome 6 |
| Terminal Utilities | Nano, SCP, SSH |

---

## 📁 Repository Structure

```text
AWS-EC2-Web-Server-Testing/
│
├── index.html              # Main webpage (dark-themed CV)
├── assets/
│   ├── style.css           # (Optional) Stylesheet file
│   └── script.js           # (Optional) Accordion functionality
└── README.md               # Documentation file
```

> The same `index.html` file is deployed to `/var/www/html/` on the EC2 instance.

---

## 🚀 Step-by-Step Deployment Guide

### 1️⃣ Launch EC2 Instance
1. Log in to **AWS Academy / AWS Console**.  
2. Navigate to **EC2 → Launch instances**.  
3. Choose **Ubuntu Server 22.04 LTS** AMI.  
4. Instance type: `t3.micro` (free tier eligible).  
5. Configure **Security Group** rules:
   - SSH (22) → My IP  
   - HTTP (80) → 0.0.0.0/0  
6. Launch instance and note the **Public IPv4 address**.

---

### 2️⃣ Connect to EC2
**Browser-based method:**  
EC2 Dashboard → Instance → Connect → **EC2 Instance Connect**

**OR via SSH (local terminal):**
```bash
ssh -i "your-key.pem" ubuntu@<your-public-ip>
```

---

### 3️⃣ Install Apache2
```bash
sudo apt update
sudo apt install apache2 -y
```
Check status:
```bash
sudo systemctl status apache2
```
You should see `active (running)`.

Visit:
```
http://<your-public-ip>
```
to confirm the default Apache page.

---

### 4️⃣ Replace the Default Page
Navigate to the web root:
```bash
cd /var/www/html
```

Back up the original page:
```bash
sudo mv index.html index_backup.html
```

Create a new one:
```bash
sudo nano index.html
```

Paste your **custom HTML** (for example, the CV page).  
Save → `Ctrl + O`, Enter → Exit → `Ctrl + X`.

Restart Apache (optional):
```bash
sudo systemctl restart apache2
```

Test again:
```
http://<your-public-ip>
```

---

### 5️⃣ Update Workflow (Local → GitHub → EC2)

1. Edit and preview HTML locally using **VS Code Live Server**.  
2. Push updates to GitHub:
   ```bash
   git add .
   git commit -m "Update CV page"
   git push
   ```
3. Copy the latest file to EC2 using SCP:
   ```bash
   scp -i your-key.pem index.html ubuntu@<your-public-ip>:/tmp/index.html
   ```
4. On EC2:
   ```bash
   sudo mv /tmp/index.html /var/www/html/index.html
   sudo systemctl restart apache2
   ```

---

## 🧩 Example HTML Features

- **Header Section:** Name, contact details, and GitHub link.  
- **Accordion Sections:**  
  - 💼 Experience  
  - 🎓 Education  
  - 🏅 Certifications  
  - 💻 Technical Skills  
  - 💬 Soft Skills  
- **Color Scheme:** Dark background with light text for readability.  
- **Responsive Design:** Works on desktop and mobile browsers.

---

## 🧠 Reflection / Learning Outcomes

Through this project, I learned to:
- Launch and manage **virtual instances** in AWS EC2.  
- Configure **security groups** to enable public web access.  
- Understand how **Apache2** serves static web content.  
- Edit and manage files within a remote **Linux environment** using nano.  
- Apply **version control and deployment workflows**.  
- Relate cloud-based web hosting to **distributed computing principles** (resource distribution, concurrency, and scalability).

---

## 🌍 Optional : Host via GitHub Pages

You can also make this repository live on GitHub Pages:

1. Go to **Settings → Pages**  
2. Choose **Source → Deploy from a branch**  
3. Select branch `main`, folder `/root`  
4. Save  

GitHub will provide a link such as  
`https://deebtarmizi104.github.io/AWS-EC2-Web-Server-Testing/`

---

## 👩‍💻 Author

Wan Nurul Adibah  

---

## 📜 License

This repository was created for **academic and self-learning purposes**.

---
