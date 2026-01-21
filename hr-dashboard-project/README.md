# 📊 HR Dashboard – User Story & Data Generation

This project is inspired by [Data with Baraa](https://www.youtube.com/watch?v=UcGF09Awm4Y)


---

## 🧩 User Story – HR Dashboard

**As an HR Manager**, I want a comprehensive dashboard to analyze human resources data, providing both summary views for high-level insights and detailed employee records for in-depth analysis.

---

## 📌 Dashboard Requirements

### 1️⃣ Summary View

The Summary View is divided into **three main sections**:  
**Overview**, **Demographics**, and **Income Analysis**

---

### 🔹 Overview

The Overview section provides a snapshot of overall HR metrics, including:

- Display the **total number of hired employees**
- Display the **total number of active employees**
- Display the **total number of terminated employees**
- Visualize the **total number of hired and terminated employees over the years**
- Present a breakdown of total employees by:
  - **Department**
  - **Job Title**
- Compare total employees between:
  - **Headquarters (HQ – New York)**
  - **Branches**
- Show the distribution of employees by:
  - **City**
  - **State**

---

### 🔹 Demographics

The Demographics section offers insights into workforce composition:

- Present the **gender ratio**
- Visualize the distribution of employees across:
  - **Age groups**
  - **Education levels**
- Show the total number of employees within each:
  - Age group
  - Education level
- Present the **correlation between education level and performance rating**

---

### 🔹 Income Analysis

The Income section focuses on salary-related metrics:

- Compare salaries across:
  - Education levels
  - Gender
- Identify salary discrepancies or patterns
- Present how **age correlates with salary** by department

---

## 2️⃣ Employee Records View

Provide a comprehensive employee list with the following fields:

- Employee ID  
- First Name  
- Last Name  
- Department  
- Job Title  
- Gender  
- Age  
- Education Level  
- Salary  

**Users should be able to filter by any available column.**

---

# 🧪 Data Generation – Python Script

The [Python script](generate_data.py) generates a **realistic HR dataset of 8,950 records** using controlled probabilities and business logic.

---

## 📂 Dataset Attributes

- Employee ID  
- First Name  
- Last Name  
- Gender  
- State  
- City  
- Hire Date  
- Department  
- Job Title  
- Education Level  
- Performance Rating  
- Overtime  
- Salary  
- Birth Date  
- Termination Date  
- Adjusted Salary  

---

## Project tree
hr-dashboard-project/
├── generate_data.py
├── HR Dashboard.twbx
├── HR_dashboards.pdf
├── HumanResources.csv
├── images/
└── mockups.drawio


