# Lesson 05 — SDLC and STLC

> **Testing from Scratch · Module 01: Software Testing Fundamentals**  
> Language: မြန်မာ (English Technical Terms မပြောင်းထားပါ)

## Learning Objectives

ဒီ Lesson ပြီးရင် **SDLC** နဲ့ **STLC** ရဲ့ ရည်ရွယ်ချက်၊ Phases၊ Differences နဲ့ Full Stack Project ထဲမှာ ဘယ်လိုအသုံးချရမလဲဆိုတာ ရှင်းပြနိုင်ရမယ်။

## 1. SDLC ဆိုတာဘာလဲ?

**SDLC (Software Development Life Cycle)** ဆိုတာ Software Product တစ်ခုကို စတင်စီစဉ်ခြင်းမှ Development, Testing, Deployment နဲ့ Maintenance အထိ စနစ်တကျ ဆောင်ရွက်တဲ့ Process ဖြစ်တယ်။

### Typical SDLC Phases

1. **Planning** — Project Scope, Goals, Feasibility, Timeline, Risks နဲ့ Resources ကို သတ်မှတ်တယ်။
2. **Requirements Analysis** — Stakeholder Needs ကို စုဆောင်းပြီး Functional/Non-functional Requirements, User Stories, Acceptance Criteria သတ်မှတ်တယ်။
3. **System Design** — Architecture, Database Schema, API Contracts, Frontend Components နဲ့ Authorization Design ကို ရေးဆွဲတယ်။
4. **Development** — Code Implement လုပ်ပြီး Code Review, Unit Tests, Integration Tests တွေကိုလည်း လုပ်နိုင်တယ်။
5. **Testing** — Expected Results နဲ့ Actual Results ကို နှိုင်းယှဉ်ပြီး Defects တွေ Detect လုပ်တယ်။
6. **Deployment & Maintenance** — Release, Monitoring, Bug Fixes, Security Updates နဲ့ Regression Testing ဆက်လုပ်တယ်။

> **Note:** ဒီ Phase List က Typical Model ဖြစ်တယ်။ Agile/Iterative Development မှာ Phases တွေ Overlap ဖြစ်ပြီး ထပ်ခါတလဲလဲ လုပ်နိုင်တယ်။ Testing က Development ပြီးမှသာ စတင်တာမဟုတ်ဘူး။

## 2. STLC ဆိုတာဘာလဲ?

**STLC (Software Testing Life Cycle)** ဆိုတာ Testing Activities တွေကို Analyze, Plan, Design, Execute, Evaluate နဲ့ Close လုပ်တဲ့ Process ဖြစ်တယ်။ STLC ဟာ SDLC နဲ့ ချိတ်ဆက်နေတယ်။

### Typical STLC Phases

1. **Requirement Analysis** — Requirements တွေ Testable ဖြစ်သလား Review လုပ်တယ်။ Ambiguities နဲ့ Missing Cases တွေ Clarify လုပ်တယ်။
2. **Test Planning** — Test Scope, Strategy, Resources, Tools, Schedule, Entry/Exit Criteria ကို သတ်မှတ်တယ်။
3. **Test Case Development** — Test Scenarios, Test Cases, Test Data နဲ့ Automated Test Scripts တွေ ပြင်ဆင်တယ်။
4. **Test Environment Setup** — Test Server, Database, Accounts, Seed Data နဲ့ Configurations ပြင်ဆင်တယ်။
5. **Test Execution** — Tests Run လုပ်ပြီး Expected vs Actual Results Compare လုပ်တယ်။ Defects Report လုပ်ပြီး Fix ပြီးနောက် Retesting/Regression Testing လုပ်တယ်။
6. **Test Closure** — Test Summary, Defect Summary, Remaining Risks နဲ့ Lessons Learned တွေ စုစည်းတယ်။

**Test Case Development** = ဘာကို ဘယ်လို Test လုပ်မလဲ Design လုပ်ခြင်း။  
**Test Execution** = Test ကို တကယ် Run လုပ်ပြီး Defect ရှိမရှိ စစ်ခြင်း။

## 3. SDLC vs STLC

| Aspect | SDLC | STLC |
|---|---|---|
| Focus | Software တစ်ခုလုံး Develop/Maintain လုပ်ခြင်း | Software Quality ကို Test/Evaluate လုပ်ခြင်း |
| Scope | Planning မှ Maintenance အထိ | Test Analysis မှ Test Closure အထိ |
| Outputs | Working Software, Releases | Test Cases, Test Results, Defect Reports |
| People | Developers, Designers, Analysts, Testers, Stakeholders | Testers, Developers, QA, Stakeholders |

### SDLC နဲ့ STLC ဘယ်လိုချိတ်ဆက်သလဲ?

- Requirements Phase → Testability Review, Initial Test Scenarios
- Design Phase → Test Planning, Test Design
- Development Phase → Unit/Integration Tests, Test Environment Setup
- Testing/Integration Phase → Test Execution, Bug Reporting, Retesting
- Deployment Phase → Smoke Tests, Release Validation
- Maintenance Phase → Regression Testing, Test Updates

ဒီ Mapping က Fixed One-to-One Relationship မဟုတ်ဘူး။

## 4. Shift-left Testing

**Shift-left Testing** ဆိုတာ Testing နဲ့ Quality Activities တွေကို Development Lifecycle အစောပိုင်းမှာ စလုပ်ပြီး Defects တွေကို စောစော Detect လုပ်တာဖြစ်တယ်။

**Example:** Project infoSphere မှာ “Only assigned supervisors can approve proposals” လို့ Requirement ရေးထားတယ်။ Requirement Review မှာ Substitute Supervisor အတွက် Rule ရှိသလားဆိုတာ ကြိုမေးနိုင်ရင် Production ရောက်မှ Authorization Workflow ပြင်ရတဲ့ Rework ကို လျှော့ချနိုင်တယ်။

## 5. Full Stack Example — Project infoSphere

**Feature:** Student Proposal Submission  
**Illustrative Stack:** React + Laravel + PostgreSQL

### SDLC Perspective

- **Requirements:** Student က Title, Description နဲ့ Supervisor ရွေးပြီး Proposal Submit လုပ်နိုင်ရမယ်။ Valid Proposal ကို Database ထဲ Save လုပ်ရမယ်။ Unauthorized User ကို Reject လုပ်ရမယ်။
- **Design:** React Form, Laravel `/api/proposals` Endpoint, PostgreSQL `proposals` Table ကို Design လုပ်တယ်။
- **Development:** Frontend Validation, Backend Validation, Authentication/Authorization နဲ့ Database Persistence ကို Implement လုပ်တယ်။
- **Testing:** API Response, Database Record, Invalid Input နဲ့ Unauthorized Request တွေ စစ်တယ်။
- **Deployment:** Release, Monitor, Fix နဲ့ Regression Testing ဆက်လုပ်တယ်။

### STLC Perspective — Example Test Cases

| Test ID | Scenario | Expected Result |
|---|---|---|
| TC-PROP-001 | Authorized Student submits valid proposal | `201 Created` **and** Database Record Exists |
| TC-PROP-002 | Required Title missing | Validation Error; no invalid record |
| TC-PROP-003 | Unauthorized user submits proposal | Access denied; no record created |
| TC-APP-001 | Assigned Supervisor approves pending proposal | Approval succeeds; status changes |
| TC-APP-002 | Unassigned Supervisor tries to approve | `403 Forbidden`; status unchanged |

> HTTP Status Code တစ်ခုတည်း Pass ဖြစ်တာနဲ့ Business Operation အောင်မြင်ပြီလို့ မဆိုနိုင်ဘူး။ Database Persistence နဲ့ Business Rules ကိုပါ Verify လုပ်ရမယ်။

### Laravel Feature Test (Illustrative)

```php
public function test_student_can_submit_a_proposal(): void
{
    $student = User::factory()->create(['role' => 'student']);
    $supervisor = User::factory()->create(['role' => 'supervisor']);

    $response = $this->actingAs($student)->postJson('/api/proposals', [
        'title' => 'Smart Agriculture Monitoring',
        'description' => 'An IoT-based monitoring system.',
        'supervisor_id' => $supervisor->id,
    ]);

    $response->assertCreated();
    $this->assertDatabaseHas('proposals', [
        'title' => 'Smart Agriculture Monitoring',
        'student_id' => $student->id,
    ]);
}
```

ဒီ Code က Example ဖြစ်ပြီး Actual Project ရဲ့ Routes, Factories, Database Schema နဲ့ Requirements အတိုင်း Adjust လုပ်ရမယ်။

## 6. Waterfall vs Agile

- **Waterfall:** Phases တွေကို အစီအစဉ်အတိုင်း အဓိကဆောင်ရွက်တဲ့ Sequential Approach။ Early Reviews နဲ့ Testing Activities တွေကိုလည်း လုပ်နိုင်တယ်။
- **Agile:** Short Iterations/Sprints တွေနဲ့ Plan → Build → Test → Feedback → Improve ကို ထပ်ခါတလဲလဲ လုပ်တယ်။

## 7. Retesting vs Regression Testing

- **Retesting:** မူလ Failed Test Case ကို Bug Fix ပြီးနောက် ပြန် Run လုပ်ပြီး Defect Fixed ဖြစ်သလား စစ်ခြင်း။
- **Regression Testing:** Fix/Change ကြောင့် Existing Features တွေ ပျက်သွားသလား စစ်ခြင်း။

## 8. Hands-on Exercise — Reviewed Answer

**Scenario:** Proposal Submission API က `201 Created` ပြန်ပေမဲ့ Database ထဲ Proposal Record မရှိဘူး။

**Q1 — Pass or Fail?**  
**Fail.** HTTP Status Code/Success Message တစ်ခုတည်းကို အားမကိုးရဘူး။ Requirement အရ Proposal Record ကို Database ထဲ Persist လုပ်ရမယ်။

**Q2 — Which STLC Phase?**  
**Test Execution.** Test Case ကို Run လုပ်ပြီး Expected Result နဲ့ Actual Result Compare လုပ်တဲ့အချိန် Defect ကို Detect လုပ်တယ်။ `Test Case Development` က Test Cases ရေးဆွဲတဲ့ Phase ဖြစ်တယ်။

**Q3 — After the Bug Fix?**  
**Retesting** ကို အရင်လုပ်ပြီး Database Persistence မှန်သွားသလား စစ်မယ်။ ထို့နောက် **Regression Testing** နဲ့ Related Features တွေ မပျက်သွားသလား စစ်မယ်။ Automated Test ထည့်သင့်တယ်။

### Professional English Answer

> **1. Fail:** A successful HTTP response does not guarantee that the business operation was completed successfully. The proposal must also be persisted in the database.  
> **2. Test Execution:** The defect is detected when actual results are compared with expected results during test execution.  
> **3. Retesting and Regression Testing:** First, rerun the failed test to verify the fix. Next, run regression tests to ensure related features still work. Add automated coverage to prevent recurrence.

## 9. Quick Quiz

1. SDLC ရဲ့ Main Purpose က ဘာလဲ?
2. STLC မှာ Test Scope နဲ့ Strategy ကို ဘယ် Phase မှာ သတ်မှတ်သလဲ?
3. Requirement Review ကို Development မစခင် လုပ်တာ ဘယ် Concept နဲ့ ဆက်စပ်သလဲ?
4. Bug Fix ပြီး မူလ Failed Test ကို ပြန် Run လုပ်တာ ဘာလဲ?
5. Test Results နဲ့ Lessons Learned တွေ စုစည်းတဲ့ Phase က ဘာလဲ?

<details><summary>Answers</summary>

1. Entire Software Development Lifecycle ကို စီမံခြင်း
2. Test Planning
3. Shift-left Testing
4. Retesting
5. Test Closure

</details>

## Key Takeaways

- SDLC = Software Product တစ်ခုလုံးကို Develop, Release, Maintain လုပ်တဲ့ Process။
- STLC = Testing Activities တွေကို Plan, Design, Execute, Evaluate လုပ်တဲ့ Process။
- STLC က SDLC နဲ့ ချိတ်ဆက်နေတယ်။
- Testing ကို Development ပြီးမှသာ စလုပ်ရတာမဟုတ်ဘူး။
- API Success ≠ Database Persistence Success။

**Lesson Status: Completed** ✅
