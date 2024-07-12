# Essential Linux Commands Every DevOps Engineer Uses Daily

Imagine you’re a chef in a super-busy restaurant kitchen. You’ve got to make sure every dish is cooked perfectly, all ingredients are in place, and everything is on time. Well, a **DevOps engineer** is like that chef—but instead of a kitchen, they’re managing **servers, applications, and systems**!

To do this, they rely on **Linux commands** every single day. Let’s break down these commands in simple words so you can understand what makes a DevOps engineer tick—and maybe even try a few commands yourself!

---

## Introduction: Why Linux Matters in DevOps

Most of the world’s servers (where websites and apps run) use **Linux**. Unlike Windows or Mac, Linux gives DevOps engineers a **powerful toolbox** through the **command line** (also called the terminal).

👉 **Why use the command line?**

- It’s faster than clicking around.
- It’s perfect for automation.
- It’s like giving instructions directly to the computer.

Whether it’s deploying a new app, monitoring system health, or fixing problems, **Linux commands** are the bread and butter of DevOps work. Let’s explore the **essential commands** every DevOps engineer uses daily.

---

## 1️⃣ Navigating the File System

Think of your computer as a giant filing cabinet. The command line helps you find and manage files and folders.

- `pwd` — **Print Working Directory**
    - Shows you where you are.
    - 📝 Example:
        
        ```
        $ pwd
        /home/devops/project
        
        ```
        
- `ls` — **List**
    - Shows the files and folders in your current directory.
    - 📝 Example:
        
        ```
        $ ls
        app.py  logs/  config.yaml
        
        ```
        
- `cd` — **Change Directory**
    - Lets you move between folders.
    - 📝 Example:
        
        ```
        $ cd logs
        
        ```
        

---

## 2️⃣ Managing Files and Folders

DevOps engineers need to create, copy, move, and delete files quickly.

- `touch` — **Create an Empty File**
    - 📝 Example:
        
        ```
        $ touch deploy.log
        
        ```
        
- `mkdir` — **Make Directory**
    - 📝 Example:
        
        ```
        $ mkdir backups
        
        ```
        
- `cp` — **Copy Files or Folders**
    - 📝 Example:
        
        ```
        $ cp config.yaml config_backup.yaml
        
        ```
        
- `mv` — **Move or Rename**
    - 📝 Example:
        
        ```
        $ mv app.py app_old.py
        
        ```
        
- `rm` — **Remove Files or Folders**
    - ⚠️ **Be careful!** This can permanently delete files.
    - 📝 Example:
        
        ```
        $ rm app_old.py
        
        ```
        

---

## 3️⃣ Monitoring System Health

Just like a doctor checks your vital signs, DevOps engineers use commands to check a system’s health.

- `top` — **Live View of Processes**
    - Shows what’s using the CPU and memory.
    - 📝 Example:
        
        ```
        $ top
        
        ```
        
- `ps` — **List Processes**
    - Shows which programs are running.
    - 📝 Example:
        
        ```
        $ ps aux
        
        ```
        
- `df` — **Disk Space Usage**
    - Helps ensure there’s enough space for logs, backups, etc.
    - 📝 Example:
        
        ```
        $ df -h
        
        ```
        
- `free` — **Memory Usage**
    - 📝 Example:
        
        ```
        $ free -m
        
        ```
        

---

## 4️⃣ Managing Services and Logs

DevOps engineers often work with services like web servers and databases.

- `systemctl` — **Control Services**
    - Starts, stops, and checks the status of services.
    - 📝 Examples:
        
        ```
        $ systemctl status nginx
        $ systemctl start apache2
        
        ```
        
- `journalctl` — **View Logs**
    - Reads system logs to troubleshoot problems.
    - 📝 Example:
        
        ```
        $ journalctl -u nginx
        
        ```
        

---

## 5️⃣ Networking Essentials

Making sure computers can talk to each other is crucial.

- `ping` — **Test Connectivity**
    - Like asking, “Hey, are you there?”
    - 📝 Example:
        
        ```
        $ ping google.com
        
        ```
        
- `ifconfig` or `ip a` — **Check Network Info**
    - Shows IP addresses and network details.
    - 📝 Example:
        
        ```
        $ ip a
        
        ```
        
- `netstat` — **Network Connections**
    - Lists open ports and active connections.
    - 📝 Example:
        
        ```
        $ netstat -tuln
        
        ```
        

---

## 6️⃣ Package Management

DevOps engineers install and update software often.

- `apt` (Debian/Ubuntu) — **Install Packages**
    - 📝 Examples:
        
        ```
        $ sudo apt update
        $ sudo apt install nginx
        
        ```
        
- `yum` or `dnf` (Red Hat/CentOS) — **Install Packages**
    - 📝 Example:
        
        ```
        $ sudo yum install httpd
        
        ```
        

---

## Diagram Time!

Here’s a **conceptual diagram** you can draw (or ask your teacher to draw) on the board or paper:

```
+-------------------------+
|     Linux Server        |
|-------------------------|
|  Files/Folders (cd, ls) |
|  System Health (top, df)|
|  Services (systemctl)   |
|  Networking (ping, ip)  |
|  Package Mgmt (apt, yum)|
+-------------------------+

```

(Use boxes and arrows to show the different sections, or draw icons like a folder, a heart monitor, a wrench, and a globe!)

---

## Why Should DevOps Engineers Care?

Here’s why these commands matter:

✅ **Speed and Automation**: No more clicking around—type a command and boom! It’s done.

✅ **Troubleshooting**: When a website crashes, these commands help fix it fast.

✅ **Remote Work**: Most servers don’t have a graphical interface—just a terminal.

✅ **Efficiency**: Automate repetitive tasks and save time.

---

## Conclusion: Master the Toolbox!

Linux commands are like a **superpower** for DevOps engineers. They help manage servers, deploy apps, monitor health, and fix problems—all from a simple terminal window.

📌 **Try This**:

- Open a Linux terminal (or use a tool like VS Code’s integrated terminal).
- Run:
    
    ```
    pwd
    ls
    mkdir test_folder
    
    ```
    
- Explore each command and see what happens!

Remember, practice makes perfect. The more you use these commands, the more comfortable you’ll become—and you’ll soon be navigating the Linux command line like a true DevOps pro! 🚀