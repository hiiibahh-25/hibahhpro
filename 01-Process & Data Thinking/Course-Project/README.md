# 🤖 AI Client Intake & Request Routing System

An intelligent system that receives client requests from a Google Forms submission, analyzes them with AI to extract the key information, and automatically routes each request to the right team.

---

## 🎯 Problem

### Context
Companies receive many requests from new clients through different forms, and the information that comes in is often unstructured or incomplete.

### The Problem
- **Slow manual processing:** The team spends time reading and formatting requests by hand.
- **Missing information:** Project requirements (service, budget, timeline) are often unclear.
- **Wrong routing:** A request may end up with the wrong department.
- **Lost requests:** There is no systematic follow-up on new requests.

### Why It Matters
It saves time and resources, and ensures every request reaches the right person with the right information.

---

## 💡 Solution

The system automates the whole intake process: automatic reception from the form, smart analysis of the data, and instant routing based on the request's status.

### What does the system do?
- ✅ Automatically receives form responses
- ✅ Extracts key data (service, budget, timeline)
- ✅ Checks that the information is complete
- ✅ Routes the request to the team or to manual review
- ✅ Documents every step in an organized way

---

## 👤 Users

**Primary users:**
- **Sales team:** receives organized, ready-to-use requests.
- **Development team:** receives only complete requests.
- **Project manager:** reviews incomplete requests.

**User needs:**
Save their time so they can focus on actual work instead of managing data.

---

## 🧠 How I Designed the Solution

The core idea:
- Make the AI act as a **smart receptionist** that understands the client's requirements.
- Apply **strict rules** in the analysis (no assumptions).
- Route automatically based on **how complete** the data is.

---

## ⚙️ How It Works

```
Google Forms Response
        ↓
[Step 1: New Form Response]
        ↓
AI Analysis Engine
        ↓
[Step 2: Extract Data & Validate]
        ↓
Decision Logic
        ↓
[Step 3: Parallel Paths Routing]
        ↓
Output: Web Team  OR  Human Review
```

---

## 🤖 Role of AI

### What does AI do in this solution?
- ✅ **Data extraction:** pulls out the service type, budget, and timeline.
- ✅ **Completeness check:** makes sure the essential information is present.
- ✅ **Request summary:** writes a clear summary of what the client asked for.
- ✅ **Status classification:** marks the request as ready to work on or needing follow-up.

### What AI should NOT do
- ❌ Do not assume or guess information.
- ❌ Do not add information the client did not mention.
- ❌ Do not decide default prices or timelines.
- ❌ Do not ignore the rules defined in advance.

---

## 🔄 Automation

### Which parts of the process are automated?
- ✅ Receiving requests in real time
- ✅ Analyzing the data without delay
- ✅ Routing the request instantly based on its status
- ✅ Documenting every step for review

---

## 🗂️ Data

### Input
- Client name
- Requested service type
- Available budget
- Delivery timeline
- Additional requirement details

### Output
| Field | Description |
|---|---|
| Service Type | Type of service (website, app, design, etc.) |
| Timeline | The stated timeline |
| Budget | The stated budget |
| Request Summary | A complete summary of the request |
| Missing Information | Missing data, if any |
| Request Status | `VALID` or `NEEDS_REVIEW` |
| Routing | Responsible destination (`web_team` or `human_review`) |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Google Forms | Receiving client requests |
| AI by Zapier | Analyzing and classifying the data |
| Zapier Paths | Conditional routing of requests |
| Zapier (Automation) | Automating the entire process |

---

## 🔑 Key Design Decisions

### Decision 1: AI extracts data only (no assumptions)
**Decision:**
Use a strict rule: "Extract only the information explicitly stated by the client."

**Why:**
To avoid errors and ambiguity. If a client says "soon", it counts as missing data, not a defined timeline.

### Decision 2: Route based on completeness
**Decision:**
Complete request → development team directly | Incomplete request → manual review.

**Why:**
It saves the technical team's time and gives clients a professional experience from the start.

---

## 🧪 Testing

### Test 1: Complete request
**Input:**
> "I need an e-commerce website, the budget is $5000, and I need it done in one month."

**Expected result:**
- Service Type: `website`
- Timeline: `within one month`
- Budget: `$5000`
- Status: `VALID`
- Routing: `web_team`

**Status:** ✅

### Test 2: Incomplete request
**Input:**
> "I need a new website, but very quickly."

**Expected result:**
- Service Type: `website`
- Timeline: `null` (vague expression)
- Budget: `null` (not provided)
- Status: `NEEDS_REVIEW`
- Routing: `human_review`

**Status:** ✅

---

## 📸 Evidence

### Workflow
[View the project on Zapier](https://zapier.com/editor/383094940/)

<!-- Add screenshots here, for example:
![Workflow](screenshots/workflow.png)
![Final result](screenshots/final-result.png)
-->

---

## ⚠️ Challenges & Failures

### What didn't work as expected?
- ❌ **Handling vague expressions:** words like "soon" or "quickly".
- ❌ **Missing data:** some clients do not mention a budget.
- ❌ **Different input styles:** every client writes differently.

### How did I solve it?
- ✅ Defined a clear list of vague expressions that are treated as `null`.
- ✅ Gave the AI very explicit instructions covering different input styles.

---

## 📚 What I Learned

### Technical lesson
- Using Parallel Paths in Zapier to route data efficiently.
- The importance of strict rules in AI prompts.

### Problem-solving lesson
- Not assuming is the best path to accuracy.
- Good documentation saves time later.

### AI lesson
- AI works best when it has very clear instructions.
- Defined limits (`null` values) are essential.

---

## 🔮 Future Improvements

If I continue developing this project, I will:

- Use clear email templates for each path, so the team gets consistent notifications.
- Add routing paths for other services such as digital marketing and app development.
- Send an automatic follow-up email to clients when budget or timeline is missing.
- Log technical failures and send an alert when a workflow step fails.
- Add a request tracking status (new, under review, followed up) after routing.
- Measure processing time, extraction accuracy, and routing accuracy.

---

## 🔗 Project Links

- **Workflow:** https://zapier.com/editor/383094940/
- **Repository:** [add your GitHub repository link here]

---

## 👩‍💻 Author

**Hiba Hijazy**

[LinkedIn](https://www.linkedin.com/in/hiba-hijazy-57b7a642a) · [GitHub](https://github.com/hiiibahh-25)
