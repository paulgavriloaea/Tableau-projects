# 📊 HR Dashboard – User Story & Data Generation

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

The following Python script generates a **realistic HR dataset of 8,950 records** using controlled probabilities and business logic.

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

## 🐍 Python Script – HR Dataset Generator

```python
import random
import pandas as pd
from datetime import datetime, timedelta
import numpy as np

# -------------------------------
# Configuration
# -------------------------------
NUM_RECORDS = 8950
random.seed(42)
np.random.seed(42)

# -------------------------------
# Reference Data
# -------------------------------
GENDERS = ["Female", "Male"]
GENDER_PROBS = [0.46, 0.54]

STATES_CITIES = {
    "New York": ["New York"],
    "California": ["Los Angeles", "San Francisco", "San Diego"],
    "Texas": ["Dallas", "Austin", "Houston"],
    "Illinois": ["Chicago"],
    "Florida": ["Miami", "Orlando"],
    "Washington": ["Seattle"],
}

DEPARTMENTS = {
    "HR": 0.10,
    "Finance": 0.12,
    "IT": 0.22,
    "Sales": 0.20,
    "Marketing": 0.14,
    "Operations": 0.22,
}

JOB_TITLES = {
    "HR": {"HR Assistant": 0.4, "HR Manager": 0.6},
    "Finance": {"Accountant": 0.5, "Finance Manager": 0.5},
    "IT": {"Developer": 0.5, "Data Analyst": 0.3, "IT Manager": 0.2},
    "Sales": {"Sales Rep": 0.6, "Sales Manager": 0.4},
    "Marketing": {"Marketing Specialist": 0.6, "Marketing Manager": 0.4},
    "Operations": {"Operations Analyst": 0.5, "Operations Manager": 0.5},
}

EDUCATION_BY_JOB = {
    "HR Assistant": ["Bachelor"],
    "HR Manager": ["Bachelor", "Master"],
    "Accountant": ["Bachelor", "Master"],
    "Finance Manager": ["Master"],
    "Developer": ["Bachelor", "Master"],
    "Data Analyst": ["Bachelor", "Master"],
    "IT Manager": ["Master"],
    "Sales Rep": ["Bachelor"],
    "Sales Manager": ["Bachelor", "Master"],
    "Marketing Specialist": ["Bachelor"],
    "Marketing Manager": ["Master"],
    "Operations Analyst": ["Bachelor"],
    "Operations Manager": ["Bachelor", "Master"],
}

PERFORMANCE_RATINGS = ["Excellent", "Good", "Satisfactory", "Needs Improvement"]
PERFORMANCE_PROBS = [0.25, 0.40, 0.25, 0.10]

SALARY_RANGES = {
    "HR Assistant": (45000, 60000),
    "HR Manager": (75000, 95000),
    "Accountant": (60000, 80000),
    "Finance Manager": (90000, 120000),
    "Developer": (70000, 110000),
    "Data Analyst": (65000, 95000),
    "IT Manager": (100000, 140000),
    "Sales Rep": (50000, 80000),
    "Sales Manager": (85000, 120000),
    "Marketing Specialist": (55000, 80000),
    "Marketing Manager": (85000, 115000),
    "Operations Analyst": (60000, 85000),
    "Operations Manager": (90000, 120000),
}

HIRE_YEAR_PROBS = {
    year: prob for year, prob in zip(
        range(2015, 2025),
        [0.05, 0.06, 0.07, 0.08, 0.10, 0.12, 0.14, 0.14, 0.12, 0.12]
    )
}

TERMINATION_RATE = 0.112

# -------------------------------
# Helper Functions
# -------------------------------
def random_date(year):
    start = datetime(year, 1, 1)
    end = datetime(year, 12, 31)
    return start + timedelta(days=random.randint(0, (end - start).days))

def generate_birth_date(hire_date, min_age=22, max_age=60):
    age = random.randint(min_age, max_age)
    return hire_date - timedelta(days=age * 365)

def adjusted_salary(base_salary, gender, education, age):
    salary = base_salary

    if gender == "Male":
        salary *= 1.02

    if education == "Master":
        salary *= 1.08

    if age > 45:
        salary += 3000

    return round(salary, 2)

# -------------------------------
# Data Generation
# -------------------------------
records = []

for i in range(NUM_RECORDS):
    gender = random.choices(GENDERS, GENDER_PROBS)[0]

    state = random.choice(list(STATES_CITIES.keys()))
    city = random.choice(STATES_CITIES[state])

    department = random.choices(
        list(DEPARTMENTS.keys()),
        list(DEPARTMENTS.values())
    )[0]

    job_title = random.choices(
        list(JOB_TITLES[department].keys()),
        list(JOB_TITLES[department].values())
    )[0]

    education = random.choice(EDUCATION_BY_JOB[job_title])

    hire_year = random.choices(
        list(HIRE_YEAR_PROBS.keys()),
        list(HIRE_YEAR_PROBS.values())
    )[0]

    hire_date = random_date(hire_year)
    birth_date = generate_birth_date(hire_date)

    base_salary = random.randint(*SALARY_RANGES[job_title])
    age = (hire_date - birth_date).days // 365

    salary = adjusted_salary(
        base_salary,
        gender,
        education,
        age
    )

    termination_date = None
    if random.random() < TERMINATION_RATE:
        termination_date = hire_date + timedelta(days=random.randint(180, 2000))

    records.append({
        "Employee ID": f"EMP{i+1:05d}",
        "Gender": gender,
        "State": state,
        "City": city,
        "Department": department,
        "Job Title": job_title,
        "Education Level": education,
        "Hire Date": hire_date,
        "Birth Date": birth_date,
        "Age": age,
        "Salary": base_salary,
        "Adjusted Salary": salary,
        "Performance Rating": random.choices(PERFORMANCE_RATINGS, PERFORMANCE_PROBS)[0],
        "Overtime": random.choices(["Yes", "No"], [0.3, 0.7])[0],
        "Termination Date": termination_date
    })

# -------------------------------
# Create DataFrame
# -------------------------------
df = pd.DataFrame(records)
df.to_csv("hr_dataset.csv", index=False)

print("HR dataset generated successfully!")

