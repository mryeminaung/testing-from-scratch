# Testing from Scratch — Module 02, Lesson 03
## Smoke Testing, Sanity Testing, Regression Testing & Retesting

> **Language:** Burmese explanations with English technical terms  
> **Project Example:** Project infoSphere (React + Laravel + PostgreSQL)  
> **Status:** Lesson covered; Mini Challenge model answers provided.

## Learning Objectives
ဒီ Lesson ပြီးရင် Smoke, Sanity, Regression နဲ့ Retesting တို့ရဲ့ **objectives**, **scope**, **timing** ကို ခွဲခြားနိုင်မယ်။ Bug Fix နဲ့ Deployment အခြေအနေတွေမှာ Risk-based Testing Strategy ရွေးနိုင်မယ်။

## 1. Why These Testing Types Matter
Project infoSphere မှာ New Build Deploy လုပ်တာ၊ Proposal Approval Bug Fix လုပ်တာ၊ Authentication Logic Refactor လုပ်တာ စတဲ့ Changes တွေ ဖြစ်နိုင်တယ်။ Change တစ်ခုချင်းစီမှာ Testing Objective မတူဘူး။

- **Smoke Testing:** Build အသစ်က Detailed Testing ဆက်လုပ်ဖို့ အခြေခံအားဖြင့် Stable ဖြစ်သလား?
- **Sanity Testing:** Changed Area နဲ့ Related Functionality တွေ Reasonably Work ဖြစ်သလား?
- **Regression Testing:** Change အသစ်ကြောင့် Previously Working Features တွေ ပျက်သွားသလား?
- **Retesting:** အရင် Failed ဖြစ်ခဲ့တဲ့ Specific Test Case က Bug Fix ပြီးနောက် Pass ဖြစ်သလား?

## 2. Smoke Testing
**Smoke Testing** (Build Verification Testing / BVT) ဆိုတာ New Build သို့မဟုတ် Deployment ပြီးတဲ့အခါ Critical Functionalities တွေကို **broad but shallow** အနေနဲ့ မြန်မြန်စစ်ခြင်းဖြစ်တယ်။

### Example — infoSphere New Deployment
| Smoke Check | Expected Result |
|---|---|
| Application loads | Home/Login page opens |
| Student login | Valid account can log in |
| Dashboard | Dashboard renders |
| Proposal List API | Returns expected response |
| Core data operation | Database-backed operation works |

**Smoke Pass ≠ Bug-free System.** Critical Smoke Check Fail ဖြစ်ရင် Build ကို Investigate/Fix လုပ်ပြီး Smoke Tests ပြန် Run သင့်တယ်။

## 3. Sanity Testing
**Sanity Testing** ဆိုတာ Specific Bug Fix သို့မဟုတ် Focused Change ပြီးနောက် Changed Area နဲ့ Related Behaviors တွေကို **narrow and focused** စစ်တာဖြစ်တယ်။

### Example — Approval Status Bug
**Bug:** Assigned Supervisor က Approve လုပ်ပြီးပေမဲ့ Proposal Status က `pending` ပဲဖြစ်နေတယ်။

Fix ပြီးနောက် Sanity Checks:
1. Assigned Supervisor က Approve လုပ်နိုင်သလား?
2. Database Status က `approved` ဖြစ်သလား?
3. UI Success Message မှန်သလား?
4. Student Dashboard မှာ Updated Status ပေါ်သလား?

### Sanity vs Retesting
- **Retesting:** Original Failed Test Case ကို အတိအကျ ပြန် Run တာ။
- **Sanity:** Fix နဲ့ ဆက်စပ်တဲ့ Behaviors တွေကို Quick Focused Check လုပ်တာ။

Terms တွေကို Teams အလိုက် အနည်းငယ် Overlap ဖြစ်အောင် သုံးတတ်ပေမဲ့ Objective ကို ခွဲသိထားရမယ်။

## 4. Regression Testing
**Regression Testing** ဆိုတာ Code Changes, Refactoring, Bug Fixes, Dependency Updates စတာတွေကြောင့် Previously Working Features တွေ မပျက်သွားသလား စစ်တာဖြစ်တယ်။

### Example — Approval Logic Refactor
Regression Checks:
- Proposal Rejection က အလုပ်လုပ်နေသေးသလား?
- Student က Supervisor-only API ကို Access မလုပ်နိုင်သေးဘူးလား?
- Student Dashboard Status မှန်သလား?
- Proposal History Records မှန်သလား?

Regression Scope ကို **Change Impact + Business Risk + Available Time** အပေါ်မူတည်ပြီး ရွေးချယ်နိုင်တယ်။ Test Suite အားလုံးကို အမြဲ Run ရမယ်လို့ မဆိုလိုဘူး။

### Example — Playwright Regression Test
```typescript
import { test, expect } from '@playwright/test';

test('student cannot see approval action', async ({ page }) => {
  // Assume an authenticated student test session.
  await page.goto('/proposals');

  await expect(
    page.getByRole('button', { name: 'Approve' })
  ).toHaveCount(0);
});
```

**Security Reminder:** UI မှာ Button မပေါ်တာတစ်ခုတည်းနဲ့ Backend Authorization လုံခြုံတယ်လို့ မဆိုနိုင်ဘူး။ Student Role နဲ့ Approval API ကို Request ပို့ပြီး Reject လုပ်သလားကို Backend Test နဲ့ပါ Verify လုပ်ရမယ်။

## 5. Comparison Table
| Aspect | Smoke | Sanity | Regression | Retesting |
|---|---|---|---|---|
| Goal | Build readiness | Changed area confidence | Protect existing behavior | Confirm specific fix |
| Scope | Broad, shallow | Narrow, focused | Risk/impact-based | Original failed case |
| Common Timing | New build/deployment | Focused change/fix | After changes | After defect fix |
| Example | Login + Dashboard load | Approval UI/status quick checks | Rejection/permissions unchanged | Original approval bug now fixed |

## 6. Example Workflow — Bug Fix to Deployment
1. Developer fixes Approval Status Bug.
2. **Retesting:** Original Failed Case ကို ပြန် Run တယ်။
3. **Sanity:** Related Approval Behaviors ကို Quick Check လုပ်တယ်။
4. **Regression:** Rejection, Authorization, Dashboard, History ကို Risk-based Check လုပ်တယ်။
5. New Build Deploy လုပ်တယ်။
6. **Smoke:** Critical Application Functions ကို Target Environment မှာ Quick Check လုပ်တယ်။

> Actual Order က Team CI/CD Pipeline, Release Process နဲ့ Risks အပေါ်မူတည်ပြီး ပြောင်းနိုင်တယ်။

## 7. Common Mistakes
- **Smoke = Sanity** လို့ ထင်ခြင်း — Smoke က Build-wide, Sanity က Change-focused ဖြစ်တယ်။
- **Retesting Pass = Regression Not Needed** လို့ ထင်ခြင်း — Fix က Related Features တွေကို ပျက်စေနိုင်သေးတယ်။
- **Regression = Run Every Test Always** လို့ ထင်ခြင်း — Risk-based Selection လုပ်နိုင်တယ်။
- **Smoke Pass = Ready for Release** လို့ ထင်ခြင်း — Release Readiness အတွက် အခြား Quality Evidence တွေလိုနိုင်တယ်။

## 8. Knowledge Check — Questions and Answers
1. **New Deployment ပြီးနောက် Login, Dashboard, Core API Quick Check?** → Smoke Testing.
2. **Approval Fix ပြီးနောက် Related Status Display ကို Focused Check?** → Sanity Testing.
3. **Authentication Refactor ပြီးနောက် Login, Registration, Password Reset မပျက်သလား?** → Regression Testing.
4. **Previously Failed Approval Case ကို Fix ပြီးနောက် ပြန် Run?** → Retesting.
5. **Application မဖွင့်ရလို့ Detailed Testing ရပ်ထားရ?** → Failed Smoke Check.

## 9. Hands-on Mini Challenge — Scenario
Project infoSphere မှာ Proposal Approval Bug ကို Fix လုပ်ပြီး New Build Deploy လုပ်ထားတယ်။

**A.** Deployment ပြီးနောက် Login, Dashboard နဲ့ Proposal List ကို Quick Check လုပ်တယ်။  
**B.** Previously Failed Approval Test Case ကို Fix ပြီးနောက် ပြန် Run တယ်။  
**C.** Approval Status Display နဲ့ Related UI Behaviors ကို Focused Check လုပ်တယ်။  
**D.** Rejection နဲ့ Supervisor Permissions မပျက်သွားသလား စစ်တယ်။

### Question 1 — Identify the Types (Model Answer)
- **A = Smoke Testing** — New Build Critical Functions ကို Quick Check လုပ်တာ။
- **B = Retesting** — Original Failed Case ကို ပြန်စစ်တာ။
- **C = Sanity Testing** — Changed Area Related Behaviors ကို Focused Check လုပ်တာ။
- **D = Regression Testing** — Existing Rejection/Authorization Features ကို Protect လုပ်တာ။

### Question 2 — Smoke Pass ဖြစ်ရင် Regression မလိုတော့ဘူးလား?
**No.** Smoke Testing က Critical Functions အခြေခံအဆင့်မှာ Work ဖြစ်သလားပဲ စစ်တယ်။ Approval Fix ကြောင့် Rejection Feature ပျက်သွားတာမျိုးကို Regression Testing က ရှာနိုင်တယ်။

### Question 3 — Retesting vs Regression
- **Retesting:** Approval Bug ကို Fix ပြီးနောက် Database Status `approved` ဖြစ်သလား Original Test Case နဲ့ ပြန်စစ်တယ်။
- **Regression:** Rejection, Permissions, Dashboard, History စတဲ့ Previously Working Features တွေ မပျက်သလား စစ်တယ်။

### Question 4 — 30 Minutes Remaining: Risk-based Priority
Illustrative Allocation:
| Task | Time | Why |
|---|---:|---|
| Retesting original approval bug | 8 min | Confirm fix |
| Sanity on related approval behavior | 7 min | Check changed area |
| High-risk regression: permissions/rejection | 10 min | Prevent security/business workflow regressions |
| Deployment smoke checks | 5 min | Verify critical deployed functionality |

**Nuance:** ဒီအချိန်ခွဲဝေမှုက Example ဖြစ်တယ်။ Deployment မလုပ်ရသေးရင် Deployment Smoke Check ကို Deployment ပြီးမှ Run ရမယ်။ Authorization Risk အလွန်မြင့်ရင် Regression ကို ပိုစောစစ်သင့်တယ်။

## 10. Professional English Model Answers
**Q1.** A is Smoke Testing, B is Retesting, C is Sanity Testing, and D is Regression Testing. Each activity has a different objective: build readiness, fix verification, focused change validation, and protection of existing behavior.

**Q2.** No. Passing smoke tests does not eliminate the need for regression testing. Smoke tests check critical functionality at a basic level, whereas regression tests identify unintended effects of recent changes on previously working features.

**Q3.** Retesting reruns a previously failed test case to verify a defect fix. Regression testing checks that the fix has not broken existing functionality, such as proposal rejection or supervisor authorization.

**Q4.** With limited time, I would use risk-based prioritization. I would verify the original fix, check closely related behaviors, and test high-risk authorization and rejection paths. After deployment, I would run critical smoke checks. The exact sequence depends on the release workflow and risk assessment.

## 11. Quick Revision
**Smoke:** Is the build stable enough?  
**Sanity:** Does the changed area work?  
**Retesting:** Is the reported bug fixed?  
**Regression:** Did the change break something else?

**Next Lesson:** Black-box, White-box & Grey-box Testing.
