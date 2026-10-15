# Lesson 03 — QA vs. QC vs. Testing

**Status:** Completed

## 1. Quality Assurance (QA)
**QA** က Software Quality ကောင်းဖို့ **Development Process ကို တိုးတက်အောင်လုပ်ပြီး Defects ဖြစ်နိုင်ခြေ လျှော့ချခြင်း** ကို အဓိကထားတယ်။ **Process-oriented** ဖြစ်တယ်။

ဥပမာ Coding Standards, Requirements Review Guidelines, Pull Request Review Process, Definition of Done, Database Constraints Checklist သတ်မှတ်ခြင်း။

**Question:** Are we using the right processes to build quality software?

## 2. Quality Control (QC)
**QC** က Software Product က သတ်မှတ်ထားတဲ့ Quality Criteria တွေကို ပြည့်မီသလား **Product-oriented Evaluation** လုပ်တာဖြစ်တယ်။

ဥပမာ Completed Feature ကို Acceptance Criteria နဲ့ နှိုင်းယှဉ်ခြင်း၊ Release Quality Review လုပ်ခြင်း။

**Question:** Does the product meet the required quality standards?

## 3. Software Testing
**Testing** က Test Cases Design/Execute/Analyze လုပ်ပြီး Software Behavior ကို စစ်ဆေးတာဖြစ်တယ်။ QC မှာ အသုံးပြုတဲ့ အရေးကြီး Activity တစ်ခု ဖြစ်နိုင်တယ်။

ဥပမာ Duplicate Email Registration Request ပို့ပြီး Validation Error, API Response နဲ့ Database Record မပြောင်းတာ စစ်ခြင်း။

## 4. Comparison
| Aspect | QA | QC | Testing |
|---|---|---|---|
| Focus | Process | Product | Software Behavior |
| Main Aim | Defect Prevention | Quality Evaluation | Defect Detection and Evaluation |
| Example | Review Checklist | Release Quality Review | API Test |
| When | Throughout SDLC | During Product Evaluation | Throughout SDLC |

> QA, QC, Testing တို့ရဲ့ Scope နဲ့ Organizational Responsibilities က Company အလိုက် ကွဲပြားနိုင်ပါတယ်။

## 5. Project infoSphere Example
**Feature:** Assigned Supervisor Only Proposal Approval.

- **QA:** Authorization Review Guideline သတ်မှတ်တယ်။
- **QC:** Completed Approval Feature က Acceptance Criteria ပြည့်မီသလား Review လုပ်တယ်။
- **Testing:** Assigned/Unassigned Supervisor, Student Accounts နဲ့ API Request ပို့စစ်တယ်။

## 6. Mini Challenge — Learner's Answer
**Scenario:** Duplicate Email Bugs ထပ်မဖြစ်အောင် Database Constraints Review Checklist သတ်မှတ်ခြင်း။

**Learner:** “This is quality assurance because we need to define project requirement rules or guidelines before the development of a project.”

**Review:** **Correct — QA.** Process Improvement နဲ့ Defect Prevention ဖြစ်တယ်။ ဒါပေမဲ့ QA ကို Development မစခင်မှာပဲ လုပ်ရတာ မဟုတ်ဘူး။ SDLC တစ်လျှောက်လုံး လုပ်နိုင်တယ်။

**Improved answer (English):**
> This is Quality Assurance (QA) because the team is improving the development process by introducing a Database Constraints Review Checklist to prevent recurring defects. QA activities can take place throughout the SDLC.

## 7. Misconceptions
- QA = Testing ဆိုတာ မမှန်ဘူး။ QA Scope ပိုကျယ်တယ်။
- Testing ကို QA Engineer တစ်ယောက်တည်း လုပ်ရတာ မဟုတ်ဘူး။ Developer လည်း လုပ်တယ်။
- Tests Pass ဖြစ်တာနဲ့ 100% Bug-free မဟုတ်ဘူး။

[Mini Challenge Notes](exercises/qa-qc-testing-mini-challenge.md)
