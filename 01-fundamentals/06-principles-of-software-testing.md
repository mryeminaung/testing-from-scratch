# Lesson 06 — Seven Principles of Software Testing

> **Testing from Scratch · Module 01: Software Testing Fundamentals**  
> Language: မြန်မာ (English Technical Terms မပြောင်းထားပါ)

## Learning Objectives

Software Testing Principles 7 ခုကို နားလည်ပြီး Full Stack Projects တွေမှာ Test Design, Risk-based Prioritization နဲ့ Test Maintenance အတွက် အသုံးချနိုင်ဖို့ ဖြစ်တယ်။

## 1. Testing Shows the Presence of Defects, Not Their Absence

Testing က Defects ရှိနေကြောင်း ပြသနိုင်တယ်။ ဒါပေမဲ့ Defects လုံးဝမရှိဘူးဆိုတာ သက်သေမပြနိုင်ဘူး။

**Example — Project infoSphere:** Proposal Submission Tests 50 ခု Pass ဖြစ်ပေမဲ့ Concurrent Submission, Expired Session, Network Failure စတဲ့ မစမ်းသပ်ရသေးတဲ့ Cases တွေမှာ Bugs ရှိနိုင်သေးတယ်။

**Remember:** `All Tests Passed` ≠ `Bug-free Software`။

## 2. Exhaustive Testing Is Impossible

Inputs, Conditions, Browser/Device Combinations နဲ့ Execution Paths အားလုံးကို လက်တွေ့မှာ Test လုပ်ဖို့ မဖြစ်နိုင်သလောက် ဖြစ်တယ်။ ဒါကြောင့် **Risk-based Testing**, **Boundary Value Analysis (BVA)** နဲ့ **Equivalence Partitioning** စတဲ့ Techniques တွေကို သုံးရတယ်။

**Example:** Password Minimum Length = 8 ဆိုရင် 7, 8, 9 Characters ကို Boundary Values အဖြစ် စမ်းနိုင်တယ်။

| Password Length | Expected Result |
|---|---|
| 7 | Reject |
| 8 | Accept (အခြား Rules တွေ ပြည့်မီရင်) |
| 9 | Accept (အခြား Rules တွေ ပြည့်မီရင်) |

## 3. Early Testing Saves Time and Money

Defects တွေကို Requirements/Design အစောပိုင်းကတည်းက Detect လုပ်နိုင်ရင် နောက်ပိုင်း Rework နဲ့ Fixing Effort ကို လျှော့ချနိုင်တယ်။ **Shift-left Testing** နဲ့ ဆက်စပ်တယ်။

**Example:** “Only assigned supervisors can approve proposals” ဆိုတဲ့ Requirement ကို Review လုပ်စဉ် Substitute Supervisor အတွက် Rule လိုသလား ကြိုမေးနိုင်တယ်။ Production ရောက်မှ Workflow ပြင်ရတာထက် ပိုထိရောက်နိုင်တယ်။

## 4. Defects Cluster Together

Defects တွေဟာ Modules အားလုံးမှာ ညီမျှစွာ မပြန့်နှံ့ဘဲ တချို့ Modules တွေမှာ ပိုစုစည်းနေတတ်တယ်။

**Hypothetical Project infoSphere Data:**

| Module | Defects Found |
|---|---:|
| Authentication | 12 |
| Proposal Approval | 9 |
| Dashboard | 2 |

Authentication နဲ့ Proposal Approval မှာ Defects ပိုများနေတာကြောင့် Root Cause နဲ့ Risk ကို ပိုစစ်ဆေးသင့်တယ်။ Defect Count တစ်ခုတည်းက Severity ကို မသတ်မှတ်ပေးနိုင်ဘူး။

## 5. Tests Wear Out (Pesticide Paradox)

Existing Tests တွေကိုပဲ ထပ်ခါတလဲလဲ Run လုပ်နေရင် New Defects တွေကို Detect လုပ်နိုင်မှု လျော့နည်းလာနိုင်တယ်။ Features, Requirements နဲ့ Risks ပြောင်းလာတဲ့အခါ Test Cases တွေကို **Review, Update, Expand** လုပ်ရမယ်။

**Example:** Login Tests မှာ Valid Login, Invalid Password, Logout ပဲ ရှိတယ်ဆိုပါစို့။ Password Reset Feature အသစ်ထည့်ရင် Expired Token, Reused Token, Valid Reset စတဲ့ New Tests လိုလာနိုင်တယ်။

> Existing Regression Tests တွေကို ဖျက်ပစ်ရမယ်လို့ မဆိုလိုဘူး။ Relevant Coverage ကို ထိန်းသိမ်းပြီး New Risks အတွက် Tests ထပ်ထည့်ရမယ်။

## 6. Testing Is Context Dependent

Testing Approach က Software Type, Business Requirements, User Needs နဲ့ Risk Profile အပေါ် မူတည်တယ်။

| Project | Testing Focus |
|---|---|
| Project infoSphere | RBAC, Authorization, Proposal Approval, Data Integrity |
| Exam Timetable Generator | Scheduling Conflicts, Algorithm Correctness |
| AI Documentation Assistant | API Failures, Input Handling, Output Evaluation |
| ESP32 Smart Agriculture | Sensor Data, Connectivity, Data Consistency |

**Remember:** One Testing Strategy Does Not Fit Every Project။

## 7. Absence-of-Errors Fallacy

Defects နည်းတာ၊ Tests Pass ဖြစ်တာက User ရဲ့ တကယ့်လိုအပ်ချက်ကို ဖြည့်ဆည်းနိုင်တယ်လို့ မဆိုလိုဘူး။ **Verification vs Validation** နဲ့ ဆက်စပ်တယ်။

**Example:** Exam Timetable Generator မှာ No Exam Conflicts, No Room Capacity Violations စတဲ့ Tests အားလုံး Pass ဖြစ်တယ်။ ဒါပေမဲ့ University Exam Office က Timetable ကို Manual Adjust လုပ်ဖို့ လိုပြီး System မှာ Feature မရှိဘူးဆိုရင် Actual User Needs ကို မဖြည့်ဆည်းနိုင်သေးဘူး။

**Remember:** `Absence of Defects` ≠ `Fitness for Purpose`။

## 8. Seven Principles — Quick Reference

| Principle | Main Lesson |
|---|---|
| Testing Shows Presence of Defects | Passing Tests ≠ Bug-free |
| Exhaustive Testing Is Impossible | Risk-based Test Selection လုပ် |
| Early Testing Saves Time and Money | Defects ကို စောစော Detect လုပ် |
| Defects Cluster Together | Risky Modules တွေကို အာရုံစိုက် |
| Tests Wear Out | Tests တွေ Review/Update လုပ် |
| Testing Is Context Dependent | Project Context အလိုက် Test |
| Absence-of-Errors Fallacy | Actual User Needs ကို Verify/Validate လုပ် |

## 9. Hands-on Exercise — Project infoSphere

**Scenario (Hypothetical):** Authentication = 12 Defects, Proposal Approval = 9 Defects, Dashboard = 2 Defects။

### Q1. Which Principle?

**Learner Answer:** Defects Cluster Together  
**Review:** Correct! Defects တွေက Authentication နဲ့ Proposal Approval Modules တွေမှာ ပိုစုစည်းနေတယ်။

### Q2. Which Modules Should Be Prioritized?

**Learner Answer:** Proposal and Dashboard, because Authentication has 12 defects and may take more time.  
**Review:** Time Constraint ကို စဉ်းစားထားတာ ကောင်းပေမဲ့ **Risk-based Prioritization** အရ Authentication နဲ့ Proposal Approval ကို အရင်စစ်သင့်တယ် (Defect Details မသိသေးတဲ့အခြေအနေမှာ Reasonable Initial Priority)။

- **Authentication:** Login, Sessions, Access Control နဲ့ Security Risks ရှိနိုင်တယ်။
- **Proposal Approval:** Authorization, Academic Workflow, Data Integrity ကို ထိခိုက်နိုင်တယ်။
- **Dashboard:** Cosmetic Issues ပဲဆိုရင် Lower Priority; Sensitive Data Leakage လို Issue ဖြစ်ရင် Priority မြင့်နိုင်တယ်။

**Key Learning:** `Prioritize by Risk, Not Just by Time or Convenience.`

### Q3. Should New Tests Be Added?

**Learner Answer:** If necessary, write new test cases.  
**Review:** Direction မှန်တယ်။ Principle Name ကို ဖြည့်ရမယ် — **Tests Wear Out**။ Features အသစ်၊ Requirements ပြောင်းလဲမှု၊ Emerging Risks တွေရှိရင် Existing Tests ကို Update လုပ်ပြီး New Cases ထပ်ထည့်ရမယ်။

### Professional English Answer

> **1. Defects Cluster Together:** Most of the reported defects are concentrated in the Authentication and Proposal Approval modules. These modules may need additional investigation and testing.  
> **2. Risk-based Prioritization:** I would prioritize Authentication and Proposal Approval because they involve security-sensitive functionality and critical business workflows. Even if Authentication requires more effort, I would test high-risk scenarios first rather than delay it solely because of its defect count. I would test Dashboard later, assuming its defects are less critical.  
> **3. Tests Wear Out:** Even when existing tests pass, new defects may remain undetected. I would review and update the test suite and add new test cases when features, requirements, or risks change.

## 10. Mini Challenge — Risk-based Testing

**Scenario:** Testing Time = 2 Hours။

- **Issue A:** Student က Admin-only API ကို Access လုပ်နိုင်နေတယ်။
- **Issue B:** Dashboard Card Spacing မညီဘူး။
- **Issue C:** Proposal Approval Page Loading Time = 8 Seconds။

**Recommended Priority:** Issue A ကို အရင်စစ်ပါ။ Unauthorized Admin API Access က Security နဲ့ RBAC ကို ထိခိုက်စေနိုင်လို့ High-risk ဖြစ်တယ်။ Issue C ရဲ့ Actual Impact ကို ဆက်စစ်ပြီး Issue B ကို Cosmetic Issue ဆိုရင် နောက်ထားနိုင်တယ်။

## 11. Self-check Quiz

1. All Tests Pass ဖြစ်တာ Bug-free ဖြစ်ကြောင်း သက်သေပြနိုင်သလား?
2. Inputs အားလုံး Test မလုပ်နိုင်တာ ဘယ် Principle လဲ?
3. Requirement Review မှာ Bug စောစောတွေ့တာ ဘယ် Principle လဲ?
4. Authentication မှာ Bugs ပိုများတာ ဘယ် Principle လဲ?
5. New Feature အတွက် Tests အသစ်ထည့်ရတာ ဘယ် Principle လဲ?
6. IoT နဲ့ Academic App Testing Strategies မတူတာ ဘယ် Principle လဲ?
7. Technical Tests Pass ဖြစ်ပေမဲ့ User Needs မပြည့်တာ ဘယ် Principle လဲ?

<details><summary>Answers</summary>

1. No — Testing Shows Presence of Defects, Not Their Absence
2. Exhaustive Testing Is Impossible
3. Early Testing Saves Time and Money
4. Defects Cluster Together
5. Tests Wear Out
6. Testing Is Context Dependent
7. Absence-of-Errors Fallacy

</details>

## Key Takeaways

- Tests Pass ဖြစ်တာနဲ့ Bug-free မဟုတ်ဘူး။
- Test Everything မလုပ်နိုင်လို့ Risk-based Approach သုံးရမယ်။
- Defects တွေကို Early Detect လုပ်တာ ပိုထိရောက်တယ်။
- High-risk Modules တွေကို Priority ပေးရမယ်။
- Tests တွေကို Changes အလိုက် Update လုပ်ရမယ်။
- Testing Strategy က Project Context အပေါ် မူတည်တယ်။
- User Needs ပြည့်မီမှုကို မမေ့ရဘူး။

**Lesson Status:** Exercise reviewed; Risk-based Prioritization နဲ့ Tests Wear Out ကို ပြန်လေ့ကျင့်ရန်။
