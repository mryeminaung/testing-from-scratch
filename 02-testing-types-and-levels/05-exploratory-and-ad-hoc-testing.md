# Testing from Scratch — Module 02, Lesson 05

# Exploratory Testing vs. Ad-hoc Testing

> **Language:** မြန်မာ + English Technical Terms  
> **Level:** Beginner → Intermediate  
> **Estimated Study Time:** 40–50 minutes  
> **Projects:** Project infoSphere (React + Laravel + PostgreSQL), ESP32 Smart Agriculture (React + Express + MongoDB)

## Learning Objectives

ဒီ Lesson ပြီးသွားရင် —

1. **Exploratory Testing** နဲ့ **Ad-hoc Testing** ကို ခွဲခြားနိုင်မယ်။
2. **Scripted Testing** နဲ့ Exploratory Testing တို့ရဲ့ Strengths ကို နားလည်မယ်။
3. **Session-based Exploratory Testing Charter** တစ်ခု ရေးနိုင်မယ်။
4. Findings တွေကို **Evidence** နဲ့ **Bug Report** အဖြစ် Document လုပ်နိုင်မယ်။
5. Full Stack Project တစ်ခုမှာ Risk-based Test Ideas တွေ စဉ်းစားနိုင်မယ်။

---

## 1. Why Do We Need Exploratory and Ad-hoc Testing?

Project infoSphere ရဲ့ **Proposal Submission Feature** မှာ အောက်ပါ Scripted Tests တွေ Pass ဖြစ်ထားတယ်ဆိုပါစို့။

- Valid Proposal Submit → Success
- Empty Title → Validation Error
- Unauthorized User → Access Denied
- Duplicate Proposal → Rejected (**ဒီ Business Rule ကို Requirement မှာ သတ်မှတ်ထားမှသာ**)

ဒါပေမဲ့ User က Form ဖွင့်ထားစဉ် **Session Expire** ဖြစ်သွားပြီး Submit လုပ်လိုက်တဲ့အခါ Unexpected Behavior ဖြစ်နိုင်တယ်။ အဲဒီ Scenario ကို Test Cases ထဲမှာ ကြိုမရေးထားရင် လွတ်သွားနိုင်တယ်။

**Key Idea:** Scripted Testing က Known Requirements တွေကို Consistently Verify လုပ်နိုင်တယ်။ Exploratory Testing က Unexpected Behaviors နဲ့ Unknown Risks တွေကို စူးစမ်းရှာဖွေရာမှာ ကူညီတယ်။

---

## 2. Exploratory Testing ဆိုတာ ဘာလဲ?

**Exploratory Testing** ဆိုတာ Software ကို **Learning**, **Test Design**, **Test Execution** တို့ကို တစ်ပြိုင်နက်တည်း လုပ်ဆောင်တဲ့ Testing Approach ဖြစ်တယ်။

**Mental Model:**

```text
Explore → Learn → Design → Test → Observe → Adapt
                  ↑__________________________|
```

Tester က Test Result တွေကို Observe လုပ်ပြီး နောက်ထပ် ဘာစမ်းမလဲဆိုတာ ဆုံးဖြတ်တယ်။ **Random Clicking သက်သက် မဟုတ်ဘူး**။ Mission, Focus, Notes နဲ့ Evidence တွေ ရှိနိုင်တယ်။

### 2.1 Project infoSphere Example

Proposal Submission Form ကို စမ်းမယ်။

1. **Normal Submit** — Valid Data နဲ့ Submit လုပ်တယ်။
2. **Double Submit** — Submit Button ကို အမြန် နှစ်ခါနှိပ်ကြည့်တယ်။
3. **Refresh** — Request Pending ဖြစ်နေချိန် Refresh လုပ်ကြည့်တယ်။
4. **Session Expiry** — Session Expire ဖြစ်ပြီး Submit လုပ်ကြည့်တယ်။
5. **Network Interruption** — Network Disconnect / Reconnect ဖြစ်တဲ့အခါ UI Behavior ကို စစ်တယ်။

**အရေးကြီး:** ဒီ Steps တွေက **Test Ideas** ဖြစ်ပြီး Bugs တကယ်ရှိတယ်ဆိုတဲ့ Evidence မဟုတ်ဘူး။ Actual Result ကို စမ်းသပ်ပြီးမှ မှတ်တမ်းတင်ရမယ်။

### 2.2 Main Characteristics

| Characteristic | Explanation |
|---|---|
| Learning + Testing | Software ကို စမ်းရင်း Behavior အသစ်တွေ သိလာတယ် |
| Adaptive | Observation အပေါ်မူတည်ပြီး Next Test ပြောင်းတယ် |
| Goal-oriented | Mission / Charter သတ်မှတ်နိုင်တယ် |
| Evidence-based | Notes, Screenshots, Logs, Network Responses သိမ်းနိုင်တယ် |
| Human Reasoning | Critical Thinking နဲ့ Curiosity အရေးကြီးတယ် |

---

## 3. Session-Based Exploratory Testing (SBTM)

**Session-Based Test Management** က Exploratory Testing ကို ပိုပြီး Trackable ဖြစ်အောင် **Charter**, **Time-box** နဲ့ **Session Notes** သုံးတယ်။

### 3.1 Example Testing Charter

| Field | Value |
|---|---|
| Charter Title | Proposal Submission Reliability |
| Mission | Unexpected User Actions, Session Expiry နဲ့ Duplicate Requests တွေကြောင့် ဖြစ်နိုင်တဲ့ Issues ရှာဖွေရန် |
| Scope | React Form, Laravel API, PostgreSQL Persistence |
| Time-box | 30 Minutes |
| User Role | Student |
| Test Ideas | Double Submit, Refresh, Session Expiry, Network Interruption, Browser Back |
| Deliverables | Session Notes, Evidence, Bug Reports, Follow-up Ideas |

### 3.2 Example Time-box Plan

| Time | Activity | What to Record |
|---|---|---|
| 00–05 min | Normal Submission | Baseline Behavior |
| 05–10 min | Double Submit | Request Count, DB Records |
| 10–15 min | Refresh During Submit | Form State, Duplicate/Retry Behavior |
| 15–20 min | Session Expiry | API Status, UI Error Handling |
| 20–25 min | Network Interruption | Recovery, Error Message |
| 25–30 min | Review Findings | Reproduction Steps, Evidence, Follow-ups |

### 3.3 Session Notes Template

```markdown
## Exploratory Session Notes

- Session ID: ET-001
- Charter: Proposal Submission Reliability
- Tester:
- Date / Time:
- Build / Commit:
- Environment / Browser:
- User Role:
- Test Data:

### Actions & Observations
1. Action:
   Expected / Oracle:
   Actual:
   Evidence:

### Defects
- Bug ID:
- Severity / Priority (provisional):
- Reproduction Steps:

### Follow-up Ideas
- ...
```

**Test Oracle** ဆိုတာ Result မှန်/မမှန် ဆုံးဖြတ်ဖို့ အသုံးပြုတဲ့ Reference ဖြစ်တယ်။ Requirements, Business Rules, Stakeholder Expectations စတာတွေ ဖြစ်နိုင်တယ်။

---

## 4. Ad-hoc Testing ဆိုတာ ဘာလဲ?

**Ad-hoc Testing** ဆိုတာ Formal Test Plan သို့မဟုတ် Predefined Test Cases မရှိဘဲ **Informal** နည်းနဲ့ Software ကို စမ်းသပ်တာဖြစ်တယ်။

ဥပမာ Developer က Form Feature ပြင်ပြီးနောက် —

- Button ကို နှစ်ခါနှိပ်ကြည့်တယ်။
- Empty Input ပို့ကြည့်တယ်။
- Browser Refresh လုပ်ကြည့်တယ်။
- Unexpected Characters ထည့်ကြည့်တယ်။

### Advantages

- Quick Checks လုပ်လို့ရတယ်။
- Unexpected Defects တွေကို ရှာတွေ့နိုင်တယ်။
- Setup နဲ့ Formal Documentation အများကြီး မလိုနိုင်ဘူး။

### Limitations

- Test Coverage ကို Systematically မသိနိုင်ဘူး။
- Reproduction ခက်နိုင်တယ်။
- Tester Experience ပေါ် အများကြီးမူတည်တယ်။
- Formal Tests ကို အစားမထိုးသင့်ဘူး။

---

## 5. Exploratory vs. Ad-hoc Testing

| Aspect | Exploratory Testing | Ad-hoc Testing |
|---|---|---|
| Main Idea | Learn + Design + Execute Together | Informal Testing |
| Planning | Charter / Mission ရှိနိုင် | Formal Plan မရှိတတ် |
| Structure | Structured ဖြစ်နိုင် | ပို Informal ဖြစ်တတ် |
| Documentation | Session Notes, Findings, Evidence | Minimal ဖြစ်တတ် |
| Adaptability | High | High |
| Strength | Unknown Risks ကို Systematically Explore | Quick Defect Discovery |
| Limitation | Skill နဲ့ Focus လိုတယ် | Coverage / Reproducibility အားနည်းနိုင် |

**Nuance:** Approaches နှစ်ခုဟာ လုံးဝသီးခြား မဖြစ်နိုင်ဘူး။ Informal Exploration တစ်ခုမှာ နှစ်မျိုးလုံးရဲ့ Characteristics ပါနိုင်တယ်။ Exploratory Testing ရဲ့ ထူးခြားချက်က **Conscious Learning နဲ့ Adaptive Test Design** ပဲ။

---

## 6. Scripted Testing vs. Exploratory Testing

**Scripted Testing** — Test Cases, Steps, Expected Results တွေကို ကြိုတင်ရေးထားပြီး Execute လုပ်တယ်။

**Exploratory Testing** — Tester က စမ်းသပ်နေစဉ် Findings အပေါ်မူတည်ပြီး Next Test ကို Design လုပ်တယ်။

| Scripted Test | Exploratory Test Idea |
|---|---|
| Empty Title → Validation Error | Title ကို Unicode, Whitespace, Long Text နဲ့ Explore |
| Valid Proposal → Success | Double Submit / Refresh / Network Interruption |
| Unauthorized User → Rejected | Session Expiry / Role Changes During Session |

**Best Practice:** Known Requirements တွေအတွက် Scripted Tests; Unknown Risks တွေအတွက် Exploratory Testing ကို **Complementary Approaches** အဖြစ် ပေါင်းသုံးပါ။

---

## 7. ESP32 Smart Agriculture — Practical Examples

Illustrative Architecture:

```text
ESP32 Sensors → Express API → MongoDB → React Dashboard
```

### Scripted Test

Valid Sensor Reading ကို API က လက်ခံပြီး Database မှာ Save လုပ်သလား စစ်မယ်။

### Exploratory Test Ideas

1. Sensor Reading တစ်ခုကို နှစ်ခါပို့ရင် ဘယ်လို Handle လုပ်မလဲ?
2. Network Disconnect → Reconnect ဖြစ်တဲ့အခါ Data Handling ဘယ်လိုရှိမလဲ?
3. Sensor Value က Unexpected Range ဖြစ်ရင် ဘယ်လို Response ပြန်မလဲ?
4. Dashboard ကို Browser Tabs နှစ်ခုနဲ့ ဖွင့်ထားရင် Update Behavior ဘယ်လိုရှိမလဲ?
5. Server Restart ဖြစ်တဲ့အခါ Client Recovery ဘယ်လိုရှိမလဲ?

**Note:** Duplicate Data ကို Reject/Accept လုပ်သင့်မသင့်၊ Sensor Range ဘယ်လောက်ဖြစ်သင့်သလဲဆိုတာ **Actual Requirements** ပေါ်မူတည်တယ်။ Requirement မသတ်မှတ်ထားရင် Stakeholders နဲ့ Clarify လုပ်ရမယ်။

---

## 8. Bug Reporting During Exploratory Testing

Exploratory Testing မှာ Test Case ကြိုမရှိလည်း **Reproducible Bug Report** ရေးနိုင်တယ်။

### Example Bug Report (Hypothetical)

```markdown
# BUG-ET-001 — Duplicate Proposals Created on Double Submit

## Environment
- App: Project infoSphere
- Build: [version/commit]
- Browser: [browser/version]
- Role: Student

## Preconditions
- Student is authenticated.
- Proposal submission form is open.

## Steps to Reproduce
1. Enter valid proposal data.
2. Double-click the Submit button quickly.
3. Inspect the proposal list and database records.

## Expected Result
If the business rule requires one submission per action,
only one proposal record should be created.

## Actual Result
[Record actual observed behavior after testing.]

## Evidence
- Browser Network log
- Screenshot / Screen recording
- Database query result (with sensitive data removed)

## Severity / Priority
- To be assessed based on impact and business requirements.
```

**Don't invent actual results:** Hypothetical Bug ကို Demo အဖြစ်ရေးနိုင်ပေမဲ့ Testing မလုပ်ရသေးတဲ့ Result ကို Observed Fact လို့ မဖော်ပြရဘူး။

---

## 9. Common Mistakes

1. **Exploratory = Random Clicking** လို့ ထင်တာ → Learning, Observation, Test Design ပါဝင်တယ်။
2. **Exploratory မှာ Documentation မလို** လို့ ထင်တာ → Evidence နဲ့ Notes က Reproducibility အတွက် အရေးကြီးတယ်။
3. **Ad-hoc က Formal Tests ကို အစားထိုးနိုင်တယ်** လို့ ထင်တာ → Systematic Coverage မသေချာနိုင်ဘူး။
4. **Predefined Test Case မရှိရင် Bug Report မရေးနိုင်ဘူး** လို့ ထင်တာ → Reproduction Steps နဲ့ Expected/Actual ကို Document လုပ်နိုင်တယ်။
5. **Exploratory Testing က Manual Only** လို့ ထင်တာ → Tester က Tools, Scripts နဲ့ Automation ကို Investigation အတွက် အသုံးချနိုင်တယ်။

---

## 10. Knowledge Check — Quiz

**Q1.** Charter နဲ့ Time-box သတ်မှတ်ပြီး Findings အပေါ်မူတည်ကာ Next Tests Design လုပ်တာ ဘယ် Approach လဲ?

A. Exploratory Testing  
B. Ad-hoc Testing  
C. Regression Testing

**Q2.** Formal Test Cases မရှိဘဲ Developer က UI ကို Informally စမ်းကြည့်တာ ဘယ် Approach လဲ?

A. Acceptance Testing  
B. Ad-hoc Testing  
C. Unit Testing

**Q3.** Exploratory Testing မှာ Documentation မလိုအပ်ဘူးဆိုတာ မှန်သလား?

A. Yes  
B. No

**Q4.** Scripted Testing ကို Exploratory Testing နဲ့ အပြည့်အဝ အစားထိုးသင့်သလား?

A. Yes  
B. No

**Q5.** Session Expiry Error ကိုတွေ့ပြီး Network Interruption ကို ဆက်စမ်းတာ ဘာကို ပြသလဲ?

A. Adaptive Test Design  
B. Only Retesting  
C. Only Unit Testing

### Quiz Answer Key

1. **A** — Charter နဲ့ Adaptive Learning ပါတယ်။
2. **B** — Informal Testing ဖြစ်တယ်။
3. **B** — Notes နဲ့ Evidence တွေက အရေးကြီးတယ်။
4. **B** — နှစ်မျိုးလုံးက Complementary ဖြစ်တယ်။
5. **A** — Observation အပေါ်မူတည်ပြီး Next Test ကို ပြောင်းတယ်။

---

## 11. Hands-on Mini Challenge

**Scenario:** Project infoSphere မှာ Proposal Submission Feature ကို **30 Minutes** Test လုပ်ရမယ်။

1. **Exploratory Testing Charter** တစ်ခုရေးပါ။ Mission, Scope, Time-box ပါရမယ်။
2. **Exploratory Test Ideas 5 ခု** ရေးပါ။
3. Exploratory Testing နဲ့ Ad-hoc Testing ရဲ့ Main Difference ကို ရှင်းပြပါ။
4. Duplicate Proposal Bug တွေ့ခဲ့ရင် ဘယ်လို Document လုပ်မလဲ?

### Sample Model Answers (Student Submission မဟုတ်ပါ)

**1. Charter**

- **Mission:** Proposal Submission မှာ Unexpected User Actions နဲ့ Session/Network Issues တွေကြောင့် ဖြစ်နိုင်တဲ့ Defects ရှာရန်။
- **Scope:** Student Proposal Form, Submission API, Database Persistence.
- **Time-box:** 30 Minutes.
- **Deliverables:** Session Notes, Reproduction Steps, Evidence, Follow-up Test Ideas.

**2. Five Exploratory Test Ideas**

1. Submit Button ကို နှစ်ခါနှိပ်ကြည့်မယ်။
2. Request Pending ဖြစ်နေချိန် Browser Refresh လုပ်မယ်။
3. Session Expire ဖြစ်ပြီး Submit လုပ်မယ်။
4. Network Disconnect / Reconnect လုပ်မယ်။
5. Long Text / Whitespace / Unicode Inputs နဲ့ Form Behavior စစ်မယ်။

**3. Difference**

Exploratory Testing က **Learning, Test Design, Execution** တို့ကို တစ်ပြိုင်နက်တည်း လုပ်ပြီး Charter နဲ့ Session Notes ပါဝင်နိုင်တယ်။ Ad-hoc Testing က Formal Plan မရှိတဲ့ Informal Testing ဖြစ်တယ်။

**4. Bug Documentation**

Bug Title, Environment, Preconditions, Steps to Reproduce, Expected Result, Actual Result, Evidence, Severity/Priority ကို Record လုပ်မယ်။ Duplicate Submission ဟာ Bug ဟုတ်မဟုတ် Business Rules နဲ့ Confirm လုပ်မယ်။

### Professional English Model Answers

**Q1 — Exploratory Testing Charter**

> My mission is to explore the reliability of the proposal submission workflow under unexpected user actions, expired sessions, and network interruptions. The scope includes the student-facing form, submission API, and database persistence. I will conduct a 30-minute exploratory testing session and document observations, evidence, defects, and follow-up test ideas.

**Q2 — Five Test Ideas**

> I would test rapid double submission, page refresh during submission, submission after session expiry, network interruption and recovery, and unusual input values such as long text or whitespace.

**Q3 — Difference**

> Exploratory testing combines learning, test design, and test execution, often guided by a testing charter. Ad-hoc testing is generally more informal and may be performed without a formal plan or predefined test cases. Both approaches can overlap, but exploratory testing emphasizes deliberate learning and adaptation.

**Q4 — Bug Documentation**

> I would create a bug report containing the environment, preconditions, steps to reproduce, expected and actual results, and supporting evidence such as network logs and database records. I would confirm the intended business rule before classifying duplicate submissions as a defect.

---

## 12. Lesson Summary / Quick Revision

- **Exploratory Testing:** Learning + Test Design + Execution ကို တစ်ပြိုင်နက်တည်း လုပ်တဲ့ Adaptive Testing Approach.
- **Ad-hoc Testing:** Formal Plan မရှိဘဲ Informal Testing လုပ်တာ.
- **Session-Based Testing:** Charter + Time-box + Session Notes နဲ့ Exploration ကို Manage လုပ်တာ.
- **Scripted + Exploratory:** Known Requirements နဲ့ Unknown Risks နှစ်မျိုးလုံးအတွက် Complementary ဖြစ်တယ်.
- **Bug Reporting:** Reproduction Steps, Expected vs. Actual, Evidence ကို Record လုပ်ရမယ်.

### Course Progress

- Module 02 Lesson 01 — Software Testing Levels: Covered
- Module 02 Lesson 02 — Functional vs. Non-functional Testing: Covered
- Module 02 Lesson 03 — Smoke, Sanity & Regression Testing: Covered
- Module 02 Lesson 04 — Black-box, White-box & Grey-box Testing: Covered
- **Module 02 Lesson 05 — Exploratory & Ad-hoc Testing: Notes Prepared; Exercise Pending**

**Next Module:** Module 03 — Test Case Design Techniques.

---

*GitHub Notes Path: `02-testing-types-and-levels/05-exploratory-and-ad-hoc-testing.md`*
