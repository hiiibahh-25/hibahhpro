# TaskBridge

A responsive web app that turns unclear work requests into clear, actionable plans with tasks, priorities, and tracked progress.

## 🎯 Problem

### The Context
Freelancers and early-career professionals often receive work requests without a clear breakdown of tasks, priorities, or expected deliverables.

### The Problem
People may know what they want to achieve but not how to turn it into practical steps. Without a clear plan, it is hard to organize work, set priorities, and track what is done.

### Why It Matters
A clear plan shows what is done, what is in progress, and what comes next.

## 💡 Solution

TaskBridge gives users one organized place to manage plans and tasks:

**Goal → Plan → Tasks → Priorities → Status → Progress**

What does the system do?

- Lets users sign up, log in, and log out with Supabase Auth.
- Lets users create, view, edit, and delete plans.
- Lets users add, edit, and delete tasks inside a plan.
- Supports task priority (High / Medium / Low) and status (To Do / In Progress / Done).
- Calculates progress automatically from completed tasks.
- Saves everything in a database and shows each user only their own data.

## 👤 Users

**Primary Users:** Freelancers, recent graduates, and early-career professionals (individual use only in this version).

**User Need:** Turn a vague request or goal into a structured plan and track it until it's done.

## 🧠 How I Designed the Solution

- **Data model:** `User → Plans → Tasks`. One user owns many plans, and each plan has many tasks.
- **Security at the database level:** access control is enforced with Row Level Security (RLS), not by hiding data in the UI.
- **Progress is calculated, not stored:** it is derived from current task statuses, so it can never become inconsistent with the data.
- **Small MVP scope:** no AI generation, collaboration, payments, or notifications in this version.

## ⚙️ How It Works

```
User signs up / logs in (Supabase Auth)
        ↓
Creates a plan (title, description, goal, deadline)
        ↓
Adds tasks with priority and status
        ↓
App calculates Progress = Completed ÷ Total × 100
        ↓
Data is saved in Supabase and protected by RLS
```

## 🤖 Role of AI

AI was used as a **build tool**, not as a feature inside the app.

- Lovable generated the app (UI and code) from a structured prompt: [`lovable-build-prompt.md`](lovable-build-prompt.md).
- The database design and security requirements were defined beforehand: [`database-schema.md`](database-schema.md).

### What AI Should NOT Do
- Claim a feature works or a test passed without it actually being verified.
- Use mock data as the real data source.
- Replace database-level security with frontend checks.

## 🔄 Automation

- Progress percentage is recalculated automatically when task statuses change.
- `updated_at` is updated automatically when a plan is modified.
- Deleting a plan automatically deletes its tasks (`ON DELETE CASCADE`).

## 🗂️ Data

**Input:** account credentials; plan title, description, goal, and optional deadline; tasks with priority and status.

**Output:** a personal list of plans, plan details with tasks, and a progress percentage for each plan.

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| Lovable | AI app builder used to build the application |
| Supabase Auth | User authentication |
| Supabase PostgreSQL | Storing plans and tasks |
| Supabase RLS | Per-user data access control |
| GitHub | Project documentation and versioning |

## 🔑 Key Design Decisions

### Decision 1
**Decision:** Enforce data isolation with Row Level Security.

**Why:** Hiding data in the frontend is not real protection. The database must enforce access even for direct requests.

### Decision 2
**Decision:** Link tasks to plans with a composite foreign key `(plan_id, user_id)`.

**Why:** It guarantees a task's owner always matches its plan's owner.

### Decision 3
**Decision:** Calculate progress from task statuses instead of storing it.

**Why:** A stored value could become out of sync with the real data.

## 🧪 Testing

### Test 1: Account creation with email confirmation
**Input:** Sign up with an email and password.

**Expected Result:** The app asks the user to confirm their email before signing in.

**Actual Result:** The message "Check your email to confirm your account, then sign in" appeared, and a confirmation email was received.

**Status:** ✅

### Test 2: Create a plan
**Input:** Fill in title, description, goal, and deadline, then create the plan.

**Expected Result:** The plan appears in My Plans.

**Actual Result:** The plan appeared in My Plans with its goal, deadline, and progress bar.

**Status:** ✅

### Test 3: Progress calculation
**Input:** A plan with 6 tasks, 1 marked Done.

**Expected Result:** 1 ÷ 6 ≈ 17%.

**Actual Result:** "1 of 6 done · 17%" is shown in My Plans and Plan Details.

**Status:** ✅

### Test 4: User data isolation
**Input:** Create a plan with account A, then log in with a different account B.

**Expected Result:** Account B cannot see account A's plans.

**Actual Result:** Account B saw only its own data ("No plans yet") and none of account A's plans.

**Status:** ✅

### Test 5: Edit a plan
**Input:** Open an existing plan and change its details.

**Expected Result:** The changes are saved and shown.

**Actual Result:** The plan was updated as expected.

**Status:** ✅

### Test 6: Add, edit, and delete tasks
**Input:** Add a task to a plan, edit it, then delete it.

**Expected Result:** Each action is saved and the task list updates.

**Actual Result:** All three operations worked as expected.

**Status:** ✅

### Test 7: Change task priority and status
**Input:** Change a task's priority (High / Medium / Low) and status (To Do / In Progress / Done).

**Expected Result:** The new values are saved and the progress percentage updates.

**Actual Result:** Changes were saved and progress was recalculated correctly.

**Status:** ✅

### Test 8: Delete a plan
**Input:** Delete a plan and confirm.

**Expected Result:** The plan and its tasks are removed.

**Actual Result:** The plan was deleted as expected.

**Status:** ✅

### Test 9: Data persistence
**Input:** Refresh the page, and log out then log in again.

**Expected Result:** Plans and tasks are still there.

**Actual Result:** All data was preserved.

**Status:** ✅

## 📸 Evidence

### Landing Page
![Landing Page](screenshots/landing.png)

### Sign Up
![Sign Up](screenshots/signup.png)

### Email Confirmation
![Email Confirmation](screenshots/email-confirmation.png)

### Create Plan
![Create Plan](screenshots/create-plan.png)

### My Plans
![My Plans](screenshots/my-plans.png)

### Plan Details
![Plan Details](screenshots/plan-details.png)

### Data Isolation (second account)
![Empty state for second account](screenshots/isolation-empty-state.png)

## ⚠️ Challenges & Failures

**What didn't work as expected?**

The only issue I faced was the limited credits in Lovable.

## 📚 What I Learned

### Technical Lesson
A working interface is not the same as a working system. I learned how a relational design (`User → Plans → Tasks`), constraints, and a composite foreign key keep data consistent, and how Row Level Security enforces access at the database level instead of relying on the frontend. I also learned the difference between authentication (who you are) and authorization (what you're allowed to access).

### Problem-Solving Lesson
Features should be verified by testing, not assumed. Testing with two different accounts showed that data isolation actually worked. I also learned that a small, well-defined MVP scope is easier to build and verify than a large one.

### AI Lesson
AI builders like Lovable speed up building, but the responsibility for understanding, directing, and evaluating the result stays with the engineer. A clear, structured prompt with explicit rules and verification steps leads to better results, and AI claims should be checked against the real implementation.

## 🔮 Future Improvements

If I continued developing this project, I would add:

- AI plan generation from a natural-language goal
- AI evaluation of generated plans (clarity, completeness, realism)
- Integration with external automation platforms
- A Progressive Web App (PWA) experience

## 🔗 Project Links

Live Demo: [https://clearpath-workplans.lovable.app](https://clearpath-workplans.lovable.app)

Repository: [Add your GitHub repository link]

Database design: [`database-schema.md`](database-schema.md)

Build prompt: [`lovable-build-prompt.md`](lovable-build-prompt.md)

## 👩‍💻 Author

[Your Name]

[LinkedIn] · [GitHub]
