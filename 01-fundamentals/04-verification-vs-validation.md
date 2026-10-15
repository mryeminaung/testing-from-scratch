# Lesson 04 — Verification vs. Validation

**Status:** In Progress — Practice Exercise + Mini Challenge pending

## 1. Verification
**Verification** ဆိုတာ Work Products နဲ့ Software Implementation က သတ်မှတ်ထားတဲ့ **Requirements, Specifications, Design, Standards** တွေနဲ့ ကိုက်ညီသလား စစ်ဆေးတာဖြစ်တယ်။

**Key question:** Are we building the product right?

ဥပမာ Password Minimum Length = 8 Characters ဆိုတဲ့ Specification ကို Code မှာ မှန်ကန်စွာ Implement လုပ်ထားသလား စစ်တာ။

**Activities:** Requirements Review, Design Review, Code Review, Static Analysis, Specification-based Tests.

> Verification ကို Static Review နဲ့ပဲ ကန့်သတ်မထားပါ။ Automated Tests တွေနဲ့ Specification Conformance ကို Verify လုပ်နိုင်ပါတယ်။

## 2. Validation
**Validation** ဆိုတာ Software က **Actual User Needs နဲ့ Intended Use** ကို ဖြည့်ဆည်းပေးနိုင်သလား စစ်ဆေးတာဖြစ်တယ်။

**Key question:** Are we building the right product?

ဥပမာ Registration System က Document အတိုင်း အလုပ်လုပ်ပေမဲ့ University Staff တွေက University Email Restriction တကယ်လိုအပ်ကြောင်း နောက်မှ သိလာတာ။ ဒါဟာ မူလ Exercise Requirement ထဲ မပါခဲ့တဲ့ **Additional Stakeholder Need** ဥပမာ ဖြစ်တယ်။

**Activities:** User Acceptance Testing (UAT), Prototype Evaluation, Usability Testing, Real-world Workflow Evaluation.

## 3. Comparison
| Aspect | Verification | Validation |
|---|---|---|
| Focus | Conformance to Specifications | Fitness for Intended Use |
| Key Question | Building the product right? | Building the right product? |
| Example | API Contract မှန်သလား | API က User Workflow အတွက် အသုံးဝင်သလား |
| Timing | Early and throughout SDLC | Early and throughout SDLC |

## 4. Project infoSphere Example
**Requirement:** Only assigned supervisors can approve proposals.

**Verification:** Backend Authorization က Assigned Supervisor ကိုပဲ Allow လုပ်သလား? Unauthorized Request ကို `403 Forbidden` ပြန်သလား? Database Status မပြောင်းဘူးလား?

**Validation:** Supervisor Leave ယူထားရင် Substitute Supervisor အတွက် University Workflow မှာ Approval Delegation လိုအပ်သလား? Users နဲ့ Stakeholders တွေက လက်တွေ့လိုအပ်ချက်ကို အကဲဖြတ်တယ်။

## 5. Exam Timetable Generator Example
**Verification:** Student Exam Conflict, Room Capacity, Lecturer Conflict စတဲ့ Defined Constraints တွေ ပြည့်မီသလား စစ်တယ်။

**Validation:** Travel Time, Manual Adjustment, Export Format စတာတွေက University Exam Office ရဲ့ Actual Needs နဲ့ ကိုက်ညီသလား စစ်တယ်။

## 6. Full Stack Example
| Layer | Verification | Validation |
|---|---|---|
| React | Required Field Rule မှန်သလား | User က Form ကို လွယ်ကူစွာ အသုံးပြုနိုင်သလား |
| Express/Laravel | API Contract မှန်သလား | Business Workflow ကို Support လုပ်သလား |
| Database | Unique Constraint ရှိသလား | Data Model က Actual Needs ကို Support လုပ်သလား |
| E2E | Defined Flow ကို Pass လုပ်သလား | Real User က Goal ကို ပြီးမြောက်နိုင်သလား |

## 7. Common Misconceptions
- Verification က Testing မပါဘူးဆိုတာ မမှန်ဘူး။
- Validation ကို Development ပြီးမှပဲ လုပ်ရတာ မဟုတ်ဘူး။
- Verification Pass ဖြစ်တာနဲ့ Validation Pass မဖြစ်နိုင်သေးဘူး။
- Validation က UI Testing တစ်မျိုးတည်း မဟုတ်ဘူး။

## 8. Pending Practice
[Verification vs. Validation Exercises](exercises/verification-validation-scenarios.md) ကို ဖြေပြီးမှ Lesson 04 ကို Completed သတ်မှတ်မယ်။
