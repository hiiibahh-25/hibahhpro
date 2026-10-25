# SkillBridge Lite
A responsive web app that compares a user's professional profile with a selected career opportunity and returns actionable feedback: relevant skills, potential gaps, and next steps.

---

## 🎯 Problem

### The Context
Students, recent graduates, and early-career professionals often have skills, projects, and experience, and want to apply for an internship or entry-level role (for example, in AI Automation).

### The Problem
They struggle to connect what they already have to what an opportunity requires. It is unclear which skills are relevant, how past projects support the requirements, which requirements need more learning, and what to do next.

### Why It Matters
Without that clarity, it is hard to make good decisions about professional development or to prepare effectively for an opportunity.

---

## 💡 Solution

SkillBridge Lite lets a user keep a professional profile, browse three sample opportunities, pick one, and request an analysis of how the profile relates to it. The result is never presented as a guarantee of acceptance or a final judgment of ability.

**What does the system do?**

- Lets the user view and edit their profile (name, headline, about, skills, projects, experience).
- Shows three sample opportunities with details, required skills, and responsibilities.
- Compares the saved profile with the selected opportunity when the user clicks **Analyze My Fit**.
- Displays results in three sections: **Relevant Skills**, **Potential Gaps**, **Recommended Next Steps**.
- Shows clear states for loading, insufficient data, AI unavailable, and errors.

---

## 👤 Users

**Primary Users:**
Student / Recent Graduate / Early-Career Professional (single-user prototype).

**User Need:**
Understand how their current skills, background, and projects relate to a specific opportunity, identify potential gaps, and know what to do next.

---

## 🧠 How I Designed the Solution

The project followed five design layers, where each layer's output feeds the next:

| Layer | Focus | Output |
|---|---|---|
| 01 — Understand the User | User, goal, need, pain points, facts vs. assumptions | User Understanding Brief |
| 02 — Define the Solution | Scope, features, user stories, requirements, acceptance criteria | Solution Definition |
| 03 — Design the Experience | User journey and screen flow | UX Flow |
| 04 — Design the System | System capabilities and data flow | System Design |
| 05–06 — Specify & Build with AI | Prompts and implementation guide for Lovable | Working prototype |

Main thinking: build the smallest useful solution that solves the right problem, compare against **one** opportunity at a time, and keep AI as one function inside the product rather than the product itself.

---

## ⚙️ How It Works

```
Professional Profile + Selected Opportunity
  ↓
Analysis request (Analyze My Fit)
  ↓
AI / Logic: compare documented evidence with requirements
  ↓
Structured result (validated)
  ↓
Relevant Skills · Potential Gaps · Recommended Next Steps
```

**User flow:** Home → My Profile → Opportunities → Opportunity Details → Analyze My Fit → AI Fit Analysis

---

## 🤖 Role of AI

**What does AI do in this solution?**

- Analyzes how documented skills, projects, and experience relate to the selected opportunity.
- Returns structured data with `relevantSkills` (item, evidence, relevance), `potentialGaps` (requirement, reason), and `recommendedNextSteps` (action, reason).
- Suggests practical, opportunity-specific next steps.

**What AI Should NOT Do**

- Invent skills, qualifications, projects, or experience that are not in the profile.
- Treat missing information as proof that a skill is missing.
- Guarantee acceptance or predict hiring outcomes.
- Be presented as real when only a sample result is shown (sample results must be clearly labeled as demonstrations).

---

## 🔄 Automation

- Analysis is triggered by one click (**Analyze My Fit**) using the latest saved profile and the selected opportunity.
- Results are organized automatically into the three result sections.
- Output validation runs before a result is shown as successful.
- The saved profile is kept in the browser (`localStorage`), so it persists after a refresh on the same device.

---

## 🗂️ Data

**Input**
- Profile: `name`, `headline`, `about`, `skills`, `projects`, `experience`
- Opportunity: `title`, `company`, `description`, `requiredSkills`, `responsibilities`

**Sample opportunities (fixed data)**
1. AI Automation Intern, TechFlow: Python, AI, Automation, APIs
2. Junior Frontend Developer, PixelWorks: HTML, CSS, JavaScript, React
3. IoT Solutions Engineer, Connected Systems Lab: IoT, Python, ESP32, APIs

**Output**
A structured analysis with Relevant Skills, Potential Gaps, and Recommended Next Steps, or a clear state message (loading, insufficient data, AI unavailable, error).

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Lovable | Building the responsive web app from natural-language specs |
| Application state + `localStorage` | Holding profile edits and keeping them after a refresh (same browser and device) |
| AI service | Generating the AI Fit Analysis, with secrets kept out of client-side code |
| GitHub | Hosting the project documentation and repository |

---

## 🔑 Key Design Decisions

### Decision 1
**Decision:** Compare the profile against a single opportunity per analysis.

**Why:** It keeps the scope small and the results clear, and it matches the MVP goal.

### Decision 2
**Decision:** Distinguish "potential gap" from "insufficient information."

**Why:** A skill not being mentioned does not prove it is missing, and the analysis must not claim more than the evidence supports.

### Decision 3
**Decision:** Never show sample results as real AI output.

**Why:** A UI that displays a result does not mean a real analysis happened. If AI is not configured, the app says so clearly.

### Decision 4
**Decision:** Exclude authentication, database, admin dashboard, saved opportunities, and similar features.

**Why:** They do not serve the core flow and would consume time and credits.

---

## 🧪 Testing

### Test 1: Profile editing and saving
**Input:** Fill in all profile fields (name, headline, about, skills, projects, experience) and save.

**Expected Result:** The "Profile in use" panel switches from the fictional sample profile to the user's own data, and the analysis uses it.

**Actual Result:** After saving, the panel showed the entered profile with no "Sample profile" badge. The analysis pages then showed "Profile: HIBA" instead of "Sample Student (fictional)".

**Status:** ✅

### Test 2: Persistence after page refresh
**Input:** Save the profile, then refresh the page.

**Expected Result:** After adding `localStorage` persistence, the saved profile is still there after a refresh.

**Actual Result:** Before `localStorage` was added (and while the published site was not yet updated), the profile reverted to the fictional sample profile. After adding `localStorage` and clicking Publish → Update, the saved profile stayed after a page refresh.

**Status:** ✅

### Test 3: Opportunity selection
**Input:** Open the opportunities list and view details for Junior Frontend Developer.

**Expected Result:** Each opportunity shows its own title, company, description, required skills, and responsibilities.

**Actual Result:** The list showed all three sample opportunities with their skills. The Frontend details page showed its required skills (HTML, CSS, JavaScript, React), four responsibilities, and an **Analyze My Fit** button.

**Status:** ✅

### Test 4: Analysis changes with the opportunity
**Input:** Run Analyze My Fit on the same profile for three different opportunities.

**Expected Result:** Results differ by opportunity, with all three sections shown.

**Actual Result:** Results differed for each opportunity. For IoT Solutions Engineer: ESP32 and automation workflows. For Junior Frontend Developer: the portfolio website and a general technical background. For AI Automation Intern: AI knowledge and automation workflow development. Wording also varied between two runs on the same input, which indicates generated output rather than fixed text.

**Status:** ✅

### Test 5: Analysis uses the latest saved profile
**Input:** Add ESP32 to the skills, save, and run the analysis on IoT Solutions Engineer (before the edit, ESP32 was listed as a gap).

**Expected Result:** ESP32 appears under Relevant Skills.

**Actual Result:** ESP32 appeared first under Relevant Skills, with the note that no ESP32 project or sensor integration is documented.

**Status:** ✅ (ESP32 was added only for this test and removed afterward)

### Test 6: Honesty of the analysis
**Input:** Review the Potential Gaps and Recommended Next Steps for IoT with the sample profile.

**Expected Result:** Missing information is not presented as a confirmed lack of skill, and no hiring outcome is promised.

**Actual Result:** The gaps were phrased as "undocumented experience, not a confirmed lack of ability," and the next steps were practical (build an ESP32 prototype, extend Python practice, document tests in Git). No hiring outcome was promised.

**Status:** ✅

### Test 7: AI unavailable or error state
**Input:** Run the analysis with no AI service configured or with a forced failure.

**Expected Result:** A clear message appears, and no static result is shown as real AI output.

**Actual Result:** Not tested.

**Status:** ⏳ Not tested

---

## 📸 Evidence

### Final Result
![Final Result](path/to/final-result.png)

### Workflow
![Workflow](path/to/workflow.png)

---

## ⚠️ Challenges & Failures

**What didn't work as expected?**

- The profile was kept only for the current session at first, and reverted to the sample profile.
- After sending the `localStorage` prompt to Lovable, the public link still behaved the same, because I had not published the update yet.
- Skills must be separated with commas. When I typed `Automation Workflows ESP32` without a comma, the two could be read as a single skill.
- Typing in the form is not enough: until **Save Profile** is clicked, the app keeps using the fictional sample profile.

**How did I solve it?**

- Sent Lovable a focused prompt to add `localStorage` persistence for the profile only, then clicked Publish → Update so the public link used the new version. After that, the saved profile stayed after a refresh.
- Corrected the skills field to use commas and saved again before re-running the analysis.
- Checked the "Profile in use" panel after every save to confirm which profile the analysis would use.

---

## 📚 What I Learned

### Technical Lesson
Where the data lives matters: state held only in the app is lost on refresh, so persistence (for example `localStorage`) has to be an explicit decision. Also, changes made in Lovable only reach the public link after publishing the update, so I test the published version, not just the preview.

### Problem-Solving Lesson
Building an AI solution starts with understanding the problem and the user, not with writing a prompt.

### AI Lesson
A UI that shows a result is not proof of real AI analysis. I verified it by changing the opportunity and the profile and checking that the output changed accordingly, and by checking that gaps were phrased as missing evidence rather than confirmed lack of skill.

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- Test and document the AI unavailable and error states.
- Improve mobile responsiveness and visual polish.

---

## 🔗 Project Links

**Live Demo:** [https://screenshot-faithful-layout-lab.lovable.app](https://screenshot-faithful-layout-lab.lovable.app)

**Workflow:** [Link]

**Repository:** [Link]

---

## 👩‍💻 Author

**Hibatullah Hijazy (هبة حجازي)**

[LinkedIn](https://www.linkedin.com/in/hiba-hijazy-57b7a642a) · [GitHub](https://github.com/hiiibahh-25)
