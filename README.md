# **Migration of Databse form EC2 to RDS(Iaas to Paas)**


 ## **📘 Overview**

This project demonstrates how to migrate an existing database hosted on an Amazon EC2 instance (IaaS) to Amazon RDS (PaaS).
The goal is to move from a self-managed infrastructure to a managed database service to improve scalability, reliability, and operational efficiency.

 ## **🎯 Objectives**

• Understand the difference between IaaS (EC2) and PaaS (RDS).

• Perform a database migration from EC2 to RDS securely.

• Validate the migration and ensure minimal downtime.

• Optimize performance and manage backups in RDS.

## **🧰 Prerequisites**

• AWS Account

• Existing EC2 instance with database (MySQL or PostgreSQL)

• AWS RDS instance created

• Proper Security Group configurations

• AWS CLI or AWS Management Console access

## **⚙️ Steps**

### **Step-1: Login to AWS Management Console**

1. Go to [https://aws.amazon.com/console/](https://aws.amazon.com/console/).

![alt text](<Screenshot 2025-10-27 221543-1.png>)

### **Step-2:Create RDS**

**1.click  create database.**

![alt text](<Screenshot 2025-10-27 205506.png>)

 **2. choose a database creation method.**

![alt text](<Screenshot 2025-10-27 205637.png>)

 **3. Select Database Engine.**

![alt text](<Screenshot 2025-10-27 205710.png>)

 **4. Choose engine version and Template.**

![alt text](<Screenshot 2025-10-27 210102.png>)

 **5.DB instance identifier: give your database a name** 

**6.Master username: e.g., admin**

**7.Master password: Auto Genarate Password.**

![alt text](<Screenshot 2025-10-27 210136.png>)

**8.Choose your VPC**

![alt text](<Screenshot 2025-10-27 210258.png>)

**10. Click Create database**

![alt text](<Screenshot 2025-10-27 210405.png>)

### **Step-3:lunch Ec2 Instance**

**1.Click the “Launch instance” button.**

![alt text](<Screenshot 2025-10-27 210547.png>)

**2. Name and Tags**

![alt text](<Screenshot 2025-10-27 211245.png>)

**3. Istance types.**

**4. Configure Key Pair**

![alt text](<Screenshot 2025-10-27 211321.png>)


**5. Add a Security Group rule**

![alt text](<Screenshot 2025-10-27 211349.png>)

**6. Review and Launch**

![alt text](<Screenshot 2025-10-27 211203.png>)


### **Step-4:connecting to EC2 Instance Terminal.**

![alt text](<Screenshot 2025-10-27 211437.png>)

### **Step-5: Install MariaDB Srever.**

        sudo yum update
        sudo yum install mariadb105-Server

![alt text](<Screenshot 2025-10-27 211810.png>)

**1.Start, Enable Status MariaDB Service.**

![alt text](<Screenshot 2025-10-27 212140.png>)

### **Step-6:Login to MySQL:**

     sudo mysql

**1.Set root password:**

      ALTER USER 'root'@'localhost' IDENTIFIED BY 'root';

       Exit MySQL:

![alt text](<Screenshot 2025-10-27 213453.png>)

### **Step-7: MySQL Login again with password**

**1. Login with Password**

       Sudo mysql -u root -p

 **2. Create Databse**

       Create database myntra;

       Use Myntra;     

 **3.Create table and insert data** 

       create teble user(id int, name varchar(10),Addr varchar(15)); 

       insert into user values(1,"Ram", "pune"),(2, "Sham", "Nagar");

       Select * from user;

       exit;

 ![alt text](<Screenshot 2025-10-30 200139.png>)


### **Step-8 Take a database backup**

      Mysqldump -u root -p myntra > mysql_backup.sql

(Enter password : root)

![alt text](<Screenshot 2025-10-30 200623.png>)

### **Step-9 Connect to RDS Instence**

        Sudo mysql -h <endpoint> -u admin -p

(Enter password : <rds-pass>)

![alt text](<Screenshot 2025-10-30 211635.png>)

### **Step-10 Create database and table in RDS:**

       CREATE DATABASE myntra;

       USE myntra;

       CREATE TABLE user(id int, name varchar(10), Addr varchar(15));

       Show table;

![alt text](<Screenshot 2025-10-30 211635.png>)


### **Step-11 Import the Backup into RDS:**

       mysql -h <endpoint> -u admin -p myntra < mysql_backup.sql

 (Enter password:<rds-pass>)

 ### **Step-11 Verify data in RDS:**

     sudo mysql -h <endpoint> -u admin -p

     Show databases;

     use myntr;

     Select * from user;
      
      exit

![alt text](<Screenshot 2025-10-30 214603.png>)

## **✅ Output**

All data from EC2’s local MariaDB database is now successfully migrated to Amazon RDS.


## **✅ Conclusion**

Migrating your database from EC2 to RDS simplifies management and improves reliability by leveraging AWS managed services. It’s a crucial step in moving from IaaS to PaaS architecture on AWS.