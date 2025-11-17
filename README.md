# 💾 MYSQL-TO-RDS-MIGRATION-USING-EC2

**Author:** Prasad  
**Project Type:** AWS Cloud | Database Migration  
**Version:** 1.0  
**License:** MIT  

---

## 🌐 Project Overview

This project demonstrates how to migrate a **MySQL database from an EC2 instance to Amazon RDS (MySQL engine)**.  
It covers everything from RDS setup, security configuration, export/import commands, and real-world best practices.

🔹 **Goal:** Move data securely and efficiently to AWS RDS  
🔹 **Tools Used:** EC2, RDS, MySQL, AWS Console, CLI  

---

## 🧩 Architecture

+--------------------+ +---------------------------+

| EC2 Instance | ---> | Amazon RDS (MySQL) |

| MySQL Installed | | Managed Database Service |

+--------------------+ +---------------------------+

---

## ⚙️ Tech Stack

| Component | Description |
|------------|-------------|
| ☁️ **AWS EC2** | Compute instance hosting MySQL |
| 🗄️ **AWS RDS** | Managed MySQL database service |
| 🐬 **MySQL** | Database engine used for data migration |
| 🔐 **Security Groups** | Network control for EC2 ↔ RDS access |

---

## 🚀 Step-by-Step Setup

## **Step 1 — Launch EC2 Instance**


**Update packages**
~~~
sudo apt update -y
~~~
**Install MySQL server**
~~~
sudo apt install mysql-server -y
~~~
**# Start service**
~~~
sudo systemctl start mysql
sudo systemctl enable mysql
~~~
**Create a sample database:**
~~~
sudo mysql
CREATE DATABASE studentdb;
USE studentdb;

CREATE TABLE students (
  roll_no INT PRIMARY KEY,
  name VARCHAR(100),
  contact VARCHAR(15),
  address VARCHAR(255)
);

INSERT INTO students VALUES;
EXIT;
~~~

## **Step 2 — Export the Local MySQL Database**
~~~

sudo mysqldump -u root -p studentdb > mydb.sql

🧾 This command exports your database into a .sql file for migration.
~~~
## **Step 3 — Create an RDS Database**

◆ Go to AWS Console → RDS → Create database
◆ Choose Standard Create
◆ Engine: MySQL
◆ Template: Free Tier
◆ DB Identifier: myrdsdb
◆ Master username: admin
◆ Master password: (create a secure password)
◆ Instance class: db.t3.micro
◆ Public access: ✅ Yes (for demo)
◆ Port: 3306
◆ Click Create Database and wait until status is Available ✅

## **Step 4 — Configure RDS Security Group**

◆ Go to EC2 → Security Groups
◆ Find the RDS security group
◆ Edit Inbound Rules → Add Rule:
◆ Type: MySQL/Aurora
◆ Port: 3306
◆ Source: Your EC2’s security group (recommended)

## **Step 5 — Connect EC2 to RDS**
Install MySQL client on EC2 (if not already installed):
~~~
sudo apt update
sudo apt install mysql-client -y
~~~
**Test connection:**
~~~
mysql -h <rds-endpoint> -u admin -p
Example:
mysql -h myrdsdb.cno4usiwkkw0.ap-south-1.rds.amazonaws.com -u admin -p
~~~
## **Step 6 — Create Target Database in RDS**
~~~
Once connected to RDS MySQL:
CREATE DATABASE studentdb;
EXIT;
~~~
## **step 7 — Import SQL File from EC2 to RDS**
~~~
mysql -h <rds-endpoint> -u admin -p studentdb < mydb.sql
~~~
## **Step 8 — Verify Data Migration**
~~~
mysql -h <rds-endpoint> -u admin -p
USE studentdb;
SELECT * FROM students;
~~~

✅ You should now see your table and data successfully migrated from EC2 to RDS!

## 🧠 Common Issues & Fixes

❌ Access denied	Wrong username/password	Use correct RDS admin credentials
🔒 Timeout	Security group not allowing port 3306	Edit inbound rules to allow EC2 SG
⚙️ Import error	Database doesn’t exist	Create database before import

## 📁 Folder Structure

MYSQL-TO-RDS-MIGRATION-USING-EC2/
│
├── mydb.sql               # Exported database file
├── README.md              # Project documentation
└── Images/           # (Optional) Add setup screenshots

## 📸 Recommended Screenshot Ideas

📍 RDS creation page

📍 Security group inbound rules

📍 EC2 MySQL connection success

📍 SELECT * FROM students; output

## 🧾 Summary

✅ Created MySQL DB on EC2

✅ Exported local database using mysqldump

✅ Created RDS MySQL instance

✅ Configured security for EC2 ↔ RDS communication

✅ Imported SQL file to RDS successfully

## 💡 Key Learning

◆ Understanding AWS RDS connectivity.

◆ Using mysqldump for database migration.

◆ Setting up secure VPC communication between EC2 and RDS.
 ```
## 🌐 Connect with Me

👨‍💻 **Prasad**  
💼 Cloud & DevOps Enthusiast  

- 🔗 [LinkedIn](http://linkedin.com/in/prasad-bhoite-a38a64223)  
- 🔗 [GitHub](https://github.com/Prasad-bhoite19)  
- 🔗 [Portfolio](https://prasad-bhoite19.github.io/prasad-portfolio/)
