# 🏢 Employment Management System

A comprehensive web-based Employee Management System built with PHP, MySQL, HTML, CSS, and JavaScript. This system provides separate portals for administrators and employees to manage workforce operations efficiently.

## 📋 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [System Requirements](#system-requirements)
- [Installation Guide](#installation-guide)
- [Database Setup](#database-setup)
- [Project Structure](#project-structure)
- [Usage Guide](#usage-guide)
- [Default Credentials](#default-credentials)
- [Screenshots](#screenshots)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

### Admin Portal
- 👥 *Employee Management*: Add, edit, view, and delete employee records
- 📊 *Project Assignment*: Assign projects to employees and track progress
- 🏖️ *Leave Management*: Approve or reject employee leave requests
- 💰 *Salary Management*: Manage employee salaries and compensation
- 📈 *Dashboard*: Overview of all employees and their status

### Employee Portal
- 👤 *Profile Management*: View and update personal information
- 🎯 *Project Tracking*: View assigned projects and their status
- 📅 *Leave Application*: Apply for leave and track application status
- 💵 *Salary Information*: View salary details and payment history
- 🔐 *Password Management*: Change account password securely

## 🛠️ Tech Stack

- *Frontend*: HTML5, CSS3, JavaScript
- *Backend*: PHP 7.4+
- *Database*: MySQL 5.7+
- *Server*: Apache (XAMPP, WAMP, or LAMP)
- *Additional Libraries*: 
  - Bootstrap (included in vendor folder)
  - jQuery (included in js folder)

## 💻 System Requirements

### Minimum Requirements
- *Operating System*: Windows 7/8/10/11, macOS 10.14+, or Linux
- *Web Server*: Apache 2.4+
- *PHP Version*: 7.4 or higher (8.0+ recommended)
- *MySQL Version*: 5.7 or higher (8.0+ recommended)
- *RAM*: 2GB minimum
- *Disk Space*: 500MB free space

### Recommended Setup
- XAMPP 8.0+ (includes Apache, MySQL, PHP)
- Modern web browser (Chrome, Firefox, Edge, Safari)
- Text editor (VS Code, Sublime Text, or Notepad++)

## 📦 Installation Guide

### Step 1: Install XAMPP

1. Download XAMPP from [https://www.apachefriends.org](https://www.apachefriends.org)
2. Install XAMPP to your preferred location (e.g., C:\xampp on Windows)
3. Launch XAMPP Control Panel
4. Start *Apache* and *MySQL* services

### Step 2: Clone or Download the Project

*Option A: Using Git*
bash
cd C:\xampp\htdocs
git clone https://github.com/rutujapachange21/Employement-Management-System.git
cd Employement-Management-System


*Option B: Manual Download*
1. Download the ZIP file from GitHub
2. Extract to C:\xampp\htdocs\Employement-Management-System

### Step 3: Database Configuration

#### Create Database
1. Open your browser and go to http://localhost/phpmyadmin
2. Click on *"New"* in the left sidebar
3. Enter database name: ems_database (or your preferred name)
4. Click *"Create"*

#### Import Database Schema
1. Select your newly created database
2. Click on the *"Import"* tab
3. Click *"Choose File"* and navigate to db/ems_database.sql
4. Click *"Go"* at the bottom

*If SQL file is not included, create tables manually:*

sql
-- Create Admin Table
CREATE TABLE admin (
    admin_id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    email VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Create Employee Table
CREATE TABLE employee (
    emp_id INT PRIMARY KEY AUTO_INCREMENT,
    emp_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    password VARCHAR(255) NOT NULL,
    phone VARCHAR(15),
    address TEXT,
    designation VARCHAR(50),
    department VARCHAR(50),
    salary DECIMAL(10,2),
    joining_date DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Create Project Table
CREATE TABLE project (
    project_id INT PRIMARY KEY AUTO_INCREMENT,
    project_name VARCHAR(100) NOT NULL,
    project_desc TEXT,
    emp_id INT,
    start_date DATE,
    end_date DATE,
    status ENUM('Pending', 'In Progress', 'Completed') DEFAULT 'Pending',
    FOREIGN KEY (emp_id) REFERENCES employee(emp_id) ON DELETE CASCADE
);

-- Create Leave Table
CREATE TABLE leaves (
    leave_id INT PRIMARY KEY AUTO_INCREMENT,
    emp_id INT,
    leave_type VARCHAR(50),
    start_date DATE,
    end_date DATE,
    reason TEXT,
    status ENUM('Pending', 'Approved', 'Rejected') DEFAULT 'Pending',
    applied_on TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (emp_id) REFERENCES employee(emp_id) ON DELETE CASCADE
);

-- Insert Default Admin
INSERT INTO admin (username, password, email) 
VALUES ('admin', MD5('admin123'), 'admin@company.com');

-- Insert Sample Employee
INSERT INTO employee (emp_name, email, password, phone, designation, department, salary, joining_date) 
VALUES ('John Doe', 'john@company.com', MD5('emp123'), '1234567890', 'Developer', 'IT', 50000, '2024-01-01');


### Step 4: Configure Database Connection

1. Open db/connection.php (or process/dbh.php if that's the connection file)
2. Update the database credentials:

php
<?php
$servername = "localhost";
$username = "root";          // Default XAMPP username
$password = "";              // Default XAMPP password (empty)
$dbname = "ems_database";    // Your database name

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
?>


### Step 5: Start the Application

1. Ensure Apache and MySQL are running in XAMPP
2. Open your web browser
3. Navigate to: http://localhost/Employement-Management-System/


## 📖 Usage Guide

### For Administrators

1. *Login*
   - Go to http://localhost/Employement-Management-System/alogin.html
   - Enter admin credentials
   - Click "Login"

2. *Add New Employee*
   - Navigate to "Add Employee" from dashboard
   - Fill in all required fields
   - Set initial password for the employee
   - Click "Submit"

3. *Assign Projects*
   - Go to "Assign Project"
   - Select employee from dropdown
   - Enter project details
   - Set start and end dates
   - Click "Assign"

4. *Manage Leave Requests*
   - Go to "Leave Requests"
   - Review pending requests
   - Click "Approve" or "Reject"

5. *Manage Salaries*
   - Navigate to "Salary Management"
   - View or update employee salaries

### For Employees

1. *Login*
   - Go to http://localhost/Employement-Management-System/elogin.html
   - Enter your email and password
   - Click "Login"

2. *View Profile*
   - Click on "My Profile" from dashboard
   - View your personal and professional details

3. *Apply for Leave*
   - Navigate to "Apply Leave"
   - Select leave type and dates
   - Enter reason
   - Click "Submit"

4. *View Projects*
   - Go to "My Projects"
   - See all assigned projects and their status

5. *View Salary*
   - Navigate to "Salary Details"
   - View your salary information

## 🔑 Default Credentials

### Admin Login
- *URL*: http://localhost/Employement-Management-System/alogin.html
- *Username*: admin
- *Password*: admin123

### Employee Login
- *URL*: http://localhost/Employement-Management-System/elogin.html
- *Email*: john@company.com
- *Password*: emp123

*⚠️ Important*: Change these default passwords immediately after first login!



## 🔧 Troubleshooting

### Common Issues and Solutions

#### 1. *Cannot connect to MySQL*
*Error*: Connection failed: Access denied for user 'root'@'localhost'

*Solution*:
- Check if MySQL is running in XAMPP
- Verify database credentials in db/connection.php
- Try resetting MySQL password in phpMyAdmin

#### 2. *Page shows blank/white screen*
*Error*: White screen or no output

*Solution*:
- Enable error reporting by adding to the top of PHP files:
php
error_reporting(E_ALL);
ini_set('display_errors', 1);

- Check Apache error logs in C:\xampp\apache\logs\error.log

#### 3. *404 Not Found*
*Error*: Page not found

*Solution*:
- Verify the project is in htdocs folder
- Check URL path: http://localhost/Employement-Management-System/
- Ensure Apache is running

#### 4. *Login not working*
*Error*: Invalid credentials or redirect issues

*Solution*:
- Verify database has admin/employee records
- Check password hashing (MD5 or password_hash)
- Clear browser cache and cookies

#### 5. *CSS/Images not loading*
*Error*: Broken styling or missing images

*Solution*:
- Check file paths in HTML/PHP files
- Verify css/assets folders exist
- Use relative paths: ./css/style.css

#### 6. *Database Import Failed*
*Error*: SQL import error

*Solution*:
- Create database first, then import
- Check SQL file for syntax errors
- Import tables one by one if needed

## 🚀 Advanced Configuration

### Enable Pretty URLs (Optional)
Create .htaccess file in root directory:
apache
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php?url=$1 [QSA,L]


### Configure Email Notifications (Optional)
Install PHPMailer for sending email notifications:
bash
composer require phpmailer/phpmailer


### Backup Database Regularly
Set up automatic backups:
bash
# Linux/Mac
mysqldump -u root -p ems_database > backup_$(date +%Y%m%d).sql

# Windows (in Command Prompt)
"C:\xampp\mysql\bin\mysqldump" -u root ems_database > backup.sql


## 👤 Author

*Rutuja Pachange*
- GitHub: [@rutujapachange21](https://github.com/rutujapachange21)
