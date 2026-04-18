# CohortIQ: Learning Analytics System

**A data-driven analysis of student retention and engagement patterns in an EdTech platform.**

---

## 📋 Project Overview

CohortIQ is a learning analytics system designed to understand **why students stay or leave** online courses. By analyzing cohort-based retention patterns, drop-off points, and engagement metrics, this project provides actionable insights into student behavior and course effectiveness.

**Real-world relevance:** This is the exact type of analysis that teams at companies like Duolingo, Coursera, and Udemy perform daily to improve their products.

---

## 🎯 Problem Statement

Most EdTech platforms struggle with these questions:

- ❓ Why do students drop off mid-course?
- ❓ Which cohorts (signup batches) are most loyal?
- ❓ Where exactly do students quit in the course progression?
- ❓ Which courses retain users best?

**Solution:** CohortIQ answers these questions using SQL-based cohort analysis, retention tracking, and visualization.

---

## 🔧 Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Database** | Oracle SQL | Store users, courses, enrollments, activity logs |
| **Data Generation** | Python (Pandas, NumPy) | Simulate realistic user behavior |
| **Analysis** | Python (Pandas, SQL queries) | Cohort retention, drop-off, engagement metrics |
| **Visualization** | Streamlit + Matplotlib | Interactive dashboard + static charts |
| **Version Control** | Git/GitHub | Project management |

---

## 📊 What This Project Analyzes

### 1. **Cohort Retention Analysis**
Tracks how many users from each signup cohort remain active over time.

```
Cohort Jan 2024: 100 users
├─ Week 1: 70 active (70% retention)
├─ Week 2: 42 active (42% retention)
├─ Week 3: 25 active (25% retention)
└─ Week 4: 15 active (15% retention)
```

**Insight:** Early drop-off suggests onboarding or engagement issues.

---

### 2. **Drop-off Analysis**
Identifies which lessons cause the largest user attrition.

```
Lesson 1: 100 users
Lesson 2: 85 users (-15%)
Lesson 3: 78 users (-7%)
Lesson 4: 72 users (-6%)
Lesson 5: 28 users (-61%) ⚠️ CRITICAL DROP-OFF
```

**Insight:** Lesson 5 needs redesign or difficulty adjustment.

---

### 3. **Course Completion Rates**
Measures which courses have high vs. low completion rates.

```
Course A: 65% completion rate ✅
Course B: 32% completion rate ⚠️
Course C: 78% completion rate ✅
```

**Insight:** Course B design needs improvement.

---

### 4. **User Engagement Metrics**
Identifies power users, inactive users, and engagement patterns.

```
Top 20% of users = 80% of total activity
Inactive users (0 activity in 30 days) = 35%
Average session length = 12 minutes
```

**Insight:** Focus retention efforts on power user behaviors.

---

## 🗂️ Project Structure

```
CohortIQ-Learning-Analytics/
│
├── README.md                          # This file
├── requirements.txt                   # Python dependencies
├── .env.example                       # Environment variables template
│
├── sql/
│   ├── 01_schema.sql                 # Database schema (CREATE TABLE)
│   ├── 02_cohort_retention.sql       # Cohort retention query
│   ├── 03_dropoff_analysis.sql       # Drop-off analysis query
│   ├── 04_completion_rate.sql        # Course completion query
│   └── 05_engagement_metrics.sql     # User engagement query
│
├── python/
│   ├── data_generator.py             # Generate realistic fake data
│   ├── oracle_connection.py          # Database connection utilities
│   ├── analysis.py                   # Run SQL queries + extract results
│   └── utils.py                      # Helper functions
│
├── streamlit/
│   └── dashboard.py                  # Interactive Streamlit dashboard
│
├── outputs/
│   ├── cohort_retention_curve.png    # Retention visualization
│   ├── dropoff_analysis.png          # Drop-off chart
│   ├── completion_rates.png          # Course completion chart
│   ├── engagement_distribution.png   # User activity distribution
│   └── analysis_results.csv          # Raw analysis data
│
└── docs/
    ├── PROJECT_REPORT.md             # Findings and insights
    └── DATA_DICTIONARY.md            # Schema documentation
```

---

##  How to Run This Project

### **Prerequisites**
- Oracle Database (11g or higher) installed locally or accessible
- Python 3.8+
- Git

### **Step 1: Clone Repository**
```bash
git clone https://github.com/your-username/CohortIQ-Learning-Analytics.git
cd CohortIQ-Learning-Analytics
```

### **Step 2: Setup Environment Variables**
Create a `.env` file in the root directory:

```bash
cp .env.example .env
```

Edit `.env` with your Oracle credentials:
```
ORACLE_USER=your_oracle_user
ORACLE_PASSWORD=your_oracle_password
ORACLE_DSN=localhost:1521/XE
```

⚠️ **Never commit `.env` to GitHub** (it's in `.gitignore`)

### **Step 3: Install Python Dependencies**
```bash
pip install -r requirements.txt
```

### **Step 4: Create Database Schema**
Connect to Oracle and run:

```bash
sqlplus your_user/your_password@localhost:1521/XE < sql/01_schema.sql
```

Or manually execute `sql/01_schema.sql` in Oracle SQL Developer.

### **Step 5: Generate Realistic Data**
```bash
python python/data_generator.py
```

This will:
- Create 500+ realistic users
- Generate course enrollments
- Simulate activity logs with realistic drop-off patterns
- Insert everything into Oracle

**Expected output:**
```
✅ Generated 500 users
✅ Generated 25 courses
✅ Generated 2,500 enrollments
✅ Generated 15,000 activity logs
✅ Data inserted successfully
```

### **Step 6: Run Analysis Queries**
```bash
python python/analysis.py
```

This will:
- Execute all SQL analysis queries
- Generate visualizations (PNG files)
- Export results to CSV

**Output location:** `outputs/`

### **Step 7: Launch Interactive Dashboard**
```bash
streamlit run streamlit/dashboard.py
```

Open browser → `http://localhost:8501`

You'll see:
- 📈 Cohort retention curves
- 📉 Drop-off analysis charts
- 📊 Course completion rates
- 👥 User engagement metrics

---

## 📈 Key Findings (Example Results)

When you run the analysis, you'll get insights like:

### Retention Patterns
- **January 2024 Cohort:** 70% retention after week 1, drops to 35% by week 4
- **Earlier cohorts:** Show better long-term retention (product improvement over time?)

### Critical Drop-off Points
- **Lesson 5:** 60% users drop off (needs UX redesign)
- **Quiz assessments:** 40% drop-off rate (reduce difficulty or add more guidance)

### Course Performance
- **Top performers:** Data Science 101 (75% completion)
- **Bottom performers:** Advanced SQL (28% completion, needs redesign)

### User Segments
- **Power users (top 10%):** Engage 3+ times/week, complete 85% of lessons
- **Casual learners (middle 40%):** 1 engagement/week, 45% completion
- **Inactive (bottom 50%):** <1 activity/month, 15% completion

---

## 🔍 SQL Analysis Examples

### Cohort Retention Query
```sql
SELECT 
    TRUNC(u.signup_date, 'MM') AS cohort_month,
    TRUNC(a.timestamp, 'MM') AS activity_month,
    COUNT(DISTINCT u.user_id) AS active_users,
    ROUND(100.0 * COUNT(DISTINCT u.user_id) / 
        (SELECT COUNT(*) FROM users u2 
         WHERE TRUNC(u2.signup_date, 'MM') = TRUNC(u.signup_date, 'MM')), 2) AS retention_pct
FROM users u
JOIN activity_logs a ON u.user_id = a.user_id
GROUP BY TRUNC(u.signup_date, 'MM'), TRUNC(a.timestamp, 'MM')
ORDER BY cohort_month, activity_month;
```

### Drop-off Analysis Query
```sql
SELECT 
    l.lesson_id,
    l.lesson_name,
    COUNT(DISTINCT a.user_id) AS users_reached,
    LAG(COUNT(DISTINCT a.user_id)) OVER (ORDER BY l.lesson_id) AS prev_lesson_users,
    ROUND(100.0 * COUNT(DISTINCT a.user_id) / 
        LAG(COUNT(DISTINCT a.user_id)) OVER (ORDER BY l.lesson_id), 2) AS retention_pct
FROM lessons l
LEFT JOIN activity_logs a ON l.lesson_id = a.lesson_id
GROUP BY l.lesson_id, l.lesson_name
ORDER BY l.lesson_id;
```

---

## 📊 Data Schema

### **users**
| Column | Type | Purpose |
|--------|------|---------|
| user_id | NUMBER (PK) | Unique user identifier |
| signup_date | DATE | When user joined |
| country | VARCHAR2(50) | Geographic data (optional) |

### **courses**
| Column | Type | Purpose |
|--------|------|---------|
| course_id | NUMBER (PK) | Unique course identifier |
| course_name | VARCHAR2(100) | Course title |
| difficulty_level | VARCHAR2(20) | Beginner/Intermediate/Advanced |

### **enrollments**
| Column | Type | Purpose |
|--------|------|---------|
| enrollment_id | NUMBER (PK) | Unique enrollment record |
| user_id | NUMBER (FK) | Links to users |
| course_id | NUMBER (FK) | Links to courses |
| enroll_date | DATE | When user enrolled |
| completion_status | VARCHAR2(20) | Completed/In Progress/Dropped |

### **lessons**
| Column | Type | Purpose |
|--------|------|---------|
| lesson_id | NUMBER (PK) | Unique lesson identifier |
| course_id | NUMBER (FK) | Links to courses |
| lesson_name | VARCHAR2(100) | Lesson title |
| lesson_order | NUMBER | Sequence in course |

### **activity_logs**
| Column | Type | Purpose |
|--------|------|---------|
| log_id | NUMBER (PK) | Unique log entry |
| user_id | NUMBER (FK) | Links to users |
| lesson_id | NUMBER (FK) | Links to lessons |
| timestamp | DATE | When activity occurred |
| action | VARCHAR2(50) | View/Complete/Quiz/Comment |
| duration_minutes | NUMBER | Time spent (optional) |

---
users,enrolments,lessons,activiy logs
## 💡 Key Insights You Can Extract

1. **Onboarding effectiveness:** Do users complete lesson 1? (predictor of retention)
2. **Difficulty curve:** Where do struggles spike? (lesson 5? quiz assessments?)
3. **Course quality:** Which courses have highest completion rates?
4. **User segments:** Who are power users vs. casual learners vs. inactive?
5. **Seasonal patterns:** Do certain cohorts perform better? (Jan cohort vs. July cohort?)

---

## 🎓 Learning Outcomes

By building this project, you'll understand:

✅ **Database design** - Schema with relationships and constraints
✅ **Data generation** - Simulate realistic user behavior
✅ **SQL analytics** - Window functions, CTEs, aggregations
✅ **Python-DB integration** - Connect and query programmatically
✅ **Data visualization** - Tell stories with charts
✅ **Full-stack thinking** - Data pipeline from DB → insights → UI

---

## 🚀 Future Enhancements

### Phase 2 (Optional upgrades)
- [ ] Predictive modeling: Predict which users will drop off
- [ ] ML clustering: Segment users by behavior patterns
- [ ] Real-time alerts: Flag cohorts with unusual drop-off
- [ ] A/B testing framework: Test course variations
- [ ] Recommendation engine: Suggest courses based on user history

### Phase 3 (Advanced)
- [ ] Deploy to cloud (AWS RDS + EC2 Streamlit)
- [ ] Add user authentication
- [ ] Export reports to PDF
- [ ] Integrate with Slack alerts

---

## 📚 Resources

- [Oracle SQL Tutorial](https://docs.oracle.com/en/database/)
- [Pandas Documentation](https://pandas.pydata.org/)
- [Streamlit Documentation](https://docs.streamlit.io/)
- [Cohort Analysis Guide](https://www.optimizesmart.com/cohort-analysis/)
- [SQL Window Functions](https://mode.com/sql-tutorial/sql-window-functions/)

---

## 🤝 Contributing

This is a personal project, but feel free to fork and adapt for your own learning!

---

## 📝 License

This project is open source under the MIT License.

---

## ✍️ Author

**Bhaskar**  
*Data Analytics & Machine Learning Enthusiast*

---

## 📧 Questions?

Have questions or found issues? Open an issue on GitHub or reach out.

---

**Last Updated:** April 2026  
**Status:** Active Development
phase 1 
phase 2