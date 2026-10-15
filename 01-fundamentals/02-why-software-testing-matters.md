# Lesson 02 — Why Software Testing Matters

**Status:** Completed

## 1. Testing က ဘာကြောင့် အရေးကြီးသလဲ?
Local Machine မှာ Application Run လို့ရရုံနဲ့ Production မှာ မှန်ကန်မယ်လို့ မဆိုနိုင်ပါ။ Different Users, Data, Environments နဲ့ Workloads တွေကြောင့် Bugs တွေ ပေါ်လာနိုင်တယ်။

Testing ရဲ့ ရည်ရွယ်ချက်က **Quality အကြောင်း Evidence ပေးပြီး Risk ကို လျှော့ချရန်** ဖြစ်တယ်။

## 2. Key Benefits
1. **Early Defect Detection** — Bug တွေကို စောစောရှာနိုင်လို့ Rework လျော့နိုင်တယ်။
2. **Risk Reduction** — Unauthorized Access, Data Loss, Incorrect Results စတာတွေကို ရှာဖွေကာကွယ်နိုင်တယ်။
3. **Requirement Verification** — Software က Specifications ကို လိုက်နာသလား စစ်နိုင်တယ်။
4. **User Satisfaction** — ယုံကြည်စိတ်ချရတဲ့ Workflow ကို ပေးနိုင်တယ်။
5. **Regression Detection** — Feature အသစ်ကြောင့် Existing Functionality ပျက်သွားတာကို ဖမ်းနိုင်တယ်။
6. **Release Confidence** — Deployment Decision အတွက် Test Evidence ရရှိတယ်။

## 3. Cost of Defects
Development မှာ Bug တွေ့ရင် Code နဲ့ Tests ပြင်ရုံနဲ့ ပြီးနိုင်ပေမဲ့ Production မှာ တွေ့ရင် Incident Investigation, Data Cleanup, User Support, Rollback/Deployment Coordination တွေ လိုလာနိုင်တယ်။ **Bug တိုင်းရဲ့ Cost က Stage အပေါ် တစ်ပုံစံတည်း မတက်ပါ** — Impact နဲ့ Context ပေါ် မူတည်တယ်။

### Shift-left Testing
Testing Activities ကို Requirements/Design Stage ကတည်းက စတင်ခြင်း။ ဥပမာ Requirements Review, Test Scenario Design, Code Review, Unit Tests စတာတွေကို Early Development မှာ လုပ်တယ်။

## 4. Full Stack Examples
### Project infoSphere — Authorization
**Requirement:** Only assigned supervisors can approve proposals.
- UI မှာ Approve Button Hide လုပ်ရုံ မလုံလောက်ဘူး။
- Backend API က Unauthorized Requests ကို Reject လုပ်ရမယ်။
- Rejected Request ကြောင့် Database Proposal Status မပြောင်းရဘူး။

### Exam Timetable Generator — Correctness
Timetable Generate ဖြစ်တာနဲ့ မှန်တယ်လို့ မဆိုနိုင်ဘူး။ Student Exam Conflicts, Room Capacity, Lecturer Conflicts နဲ့ No-solution Handling ကို စစ်ရမယ်။

### AI Documentation Assistant — Reliability
Empty Prompt, API Timeout, Rate Limit, Unauthorized Access, Sensitive API Key Exposure စတာတွေကို Test လုပ်ရမယ်။ AI Output ကို Exact Text Equality နဲ့ပဲ စစ်ဖို့ မသင့်တော်နိုင်ဘူး။

## 5. Risk-based Testing
Testing Effort ကို Risk အလိုက် ဦးစားပေးတာဖြစ်တယ်။
- **Likelihood:** Problem ဖြစ်နိုင်ခြေ
- **Impact:** ဖြစ်သွားရင် ထိခိုက်မှု

| Issue | Learner's Priority | Review |
|---|---|---|
| A — Unauthorized Proposal Approval | High | သင့်တော်; Security/Business Rule Impact မြင့်နိုင်တယ် |
| B — Dashboard Spacing | Low | Minor Cosmetic Issue ဆိုရင် သင့်တော် |
| C — Duplicate Project Submission | Medium | လက်ခံနိုင်; Data Integrity Impact မြင့်ရင် High ဖြစ်နိုင် |
| D — Slow Report Loading (12s) | Medium | လက်ခံနိုင်; Critical Workflow ဆိုရင် High ဖြစ်နိုင် |

**Learner's reasoning:** Issue A ကို အရင်စစ်မယ်၊ Authorization နဲ့ Approval Flow ကို Verify လုပ်ရမယ်။

**Improvement:** Backend Authorization, Role/Assignment Rules နဲ့ Rejected Request ကြောင့် Database State မပြောင်းတာကို Verify လုပ်ပါ။

## 6. Severity vs. Priority (Preview)
- **Severity:** Defect က System ကို ဘယ်လောက်ထိခိုက်သလဲ?
- **Priority:** Defect ကို ဘယ်လောက်မြန်မြန် Fix လုပ်သင့်သလဲ?

## Key Takeaway
**A successful HTTP response does not always mean a successful business operation.**

[Risk-based Testing Exercise](exercises/risk-based-testing.md)
