# CareerFlow

A web app that helps job seekers track their job applications, interview dates, and results in one organized dashboard.

---

## 🎯 Problem

### The Context
Job seekers usually apply to many companies at the same time, through different websites, emails, and platforms.

### The Problem
Application details (company, job title, application date, interview date, notes) end up scattered across notes, emails, and browser tabs. It becomes easy to forget where you applied, what stage each application is at, and when an interview is scheduled.

### Why It Matters
Missing an interview or forgetting to follow up can cost a real opportunity. Having one clear view of all applications reduces stress and helps people stay organized and prepared.

---

## 💡 Solution

CareerFlow is a personal dashboard where each user signs in and manages their own job applications from one place.

### What does the system do?

- Lets users sign up, log in, and log out securely.
- Lets users add, edit, and delete job applications (company, job title, status, application date, interview date, job link, notes).
- Shows live statistics: total applications, interview stage, offers received, and rejected.
- Lets users search by company or job title and filter by status.
- Keeps each user's data private, so one user cannot see another user's applications.

---

## 👤 Users

### Primary Users
Job seekers, fresh graduates, and students applying to multiple jobs or internships.

### User Need
Track every application and its stage, remember interview dates, and keep notes and job links in one place.

---

## 🧠 How I Designed the Solution

- **Simple dashboard first:** the main screen shows the numbers that matter most (total, interviews, offers, rejected) before the details.
- **Four clear statuses:** Applied, Interview, Offer, Rejected, matching the real stages of a job search.
- **One form for everything:** a single "Add Application" form keeps data entry fast, with only Company Name and Job Title required.
- **Per-user data:** every application belongs to the logged-in user, so the app is safe to use with real personal information.

---

## ⚙️ How It Works

```
User signs up / logs in
  ↓
Opens the Dashboard
  ↓
Adds or edits an application (form with validation)
  ↓
Data is saved to the database, linked to the user
  ↓
Dashboard refreshes: table + statistics update
  ↓
User searches / filters / updates status over time
```

---

## 🔄 Automation

- Statistics cards (Total, Interview, Offers, Rejected) update automatically whenever an application is added, edited, or deleted.
- Search and status filtering update the table instantly with the result count.
- Applications are automatically linked to the logged-in user and loaded only for that user.

---

## 🗂️ Data

### Input
Company name, job title, status, application date, interview date, job link, and notes, entered by the user.

### Output
A personal dashboard with a searchable and filterable list of applications, plus summary statistics.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| Lovable | Building the web app and user interface |
| Supabase | Database, authentication, and user data management |
| Supabase Row Level Security (RLS) | Making sure each user only accesses their own data |
| GitHub | Source code repository |

---

## 🔑 Key Design Decisions

### Decision 1
**Decision:** Use Supabase Authentication with per-user data.

**Why:** Job application data is personal. Each user must only see their own applications.

### Decision 2
**Decision:** Require only Company Name and Job Title; all other fields are optional.

**Why:** Users should be able to save an application quickly and add details later, such as the interview date.

### Decision 3
**Decision:** Show summary statistics at the top of the dashboard.

**Why:** Users get an instant overview of their progress without scanning the full table.

---

## 🧪 Testing

### Test 1: Positive Test
**Input:** Log in, click "Add Application", and fill in all fields with valid data (company, job title, status, dates, link, notes).

**Expected Result:** The application is saved, appears in the table, and the statistics cards update.

**Actual Result:** [Fill in after testing]

**Status:** ⬜ ✅ / ❌

### Test 2: Negative Test
**Input:** Try to save an application with an empty Company Name and/or Job Title. Also try an invalid job link (for example `abc`).

**Expected Result:** The app shows a validation error and does not save the incomplete or invalid data.

**Actual Result:** [Fill in after testing]

**Status:** ⬜ ✅ / ❌

### Test 3: Edge Case
**Input:** Set the Interview Date earlier than the Application Date, or enter very long notes (including Arabic text), or delete the last remaining application.

**Expected Result:** The app handles it without crashing (for example, validation message, text displayed correctly, empty state shown).

**Actual Result:** [Fill in after testing]

**Status:** ⬜ ✅ / ❌

### Test 4: Data / Access Test
**Input:** Create two accounts (User A and User B). Add an application as User A, then log in as User B.

**Expected Result:** User B cannot see or modify User A's applications.

**Actual Result:** [Fill in after testing]

**Status:** ⬜ ✅ / ❌

---

## 📸 Evidence

### Final Result
![Dashboard](screenshots/dashboard.png)

### Add Application Form
![Add Application](screenshots/add-application.png)

### Test Evidence
- Positive test: ![Positive](screenshots/test-positive.png)
- Negative test: ![Negative](screenshots/test-negative.png)
- Edge case: ![Edge](screenshots/test-edge.png)
- Data / access test (two accounts): ![Access](screenshots/test-access.png)
- Database result in Supabase: ![Database](screenshots/supabase-table.png)
- Bug fix before / after: ![Fix](screenshots/bug-fix.png)

---

## ⚠️ Challenges & Failures

### What didn't work as expected?

- [Describe the bug(s) you found during testing. Example: the date field displayed in a confusing format in the form.]
- [Add any other issue, such as validation not blocking invalid data.]

### How did I solve it?

- [Explain what you changed in Lovable or Supabase, and how you re-tested to confirm the fix.]

---

## 📚 What I Learned

### Technical Lesson
[Example: How authentication and Row Level Security keep user data separate in Supabase.]

### Problem-Solving Lesson
[Example: Testing with real scenarios and two accounts reveals problems that normal use does not show.]

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- Add a Kanban board view with drag and drop between statuses.
- Add follow-up reminders and upcoming-interview alerts.
- Add charts for application progress over time.
- Add Arabic / English language switch with full RTL support.

---

## 🔗 Project Links

**Live Demo:** https://role-hunt-haven.lovable.app

**Repository:** [Add your GitHub repository link]

---

## 👩‍💻 Author

**Hibatullah Hijazy**

[LinkedIn](https://www.linkedin.com/in/hiba-hijazy-57b7a642a) · [GitHub](https://github.com/hiiibahh-25)
