# Lesson 01 — Software Testing Levels

> **Testing from Scratch · Module 02: Testing Types and Levels**  
> Language: မြန်မာ (English Technical Terms မပြောင်းထားပါ)  
> **Status: Completed — Hands-on Mini Challenge 3/3**

## Learning Objectives

ဒီ Lesson ပြီးရင် **Unit, Integration, System, Acceptance Testing** ကို Scope နဲ့ Objective အလိုက် ခွဲခြားနိုင်ရမယ်။ React, Laravel, PostgreSQL ပါတဲ့ Full Stack Application မှာ ဘယ် Testing Level ကို ဘာကြောင့် အသုံးပြုသလဲ ရှင်းပြနိုင်ရမယ်။

## 1. Software Testing Levels ဆိုတာဘာလဲ?

**Testing Level** ဆိုတာ Software ရဲ့ ဘယ်အပိုင်း၊ ဘယ် Scope ကို ဘယ် Objective နဲ့ စမ်းသပ်သလဲဆိုတာ ခွဲခြားတဲ့ Concept ဖြစ်တယ်။ Typical Levels 4 ခုက —

1. **Unit Testing** — Individual Testable Unit တစ်ခုကို စစ်တယ်။
2. **Integration Testing** — Components/Modules အချင်းချင်း Interaction ကို စစ်တယ်။
3. **System Testing** — Complete Integrated System ကို စစ်တယ်။
4. **Acceptance Testing** — Business Requirements နဲ့ Acceptance Criteria ကို ဖြည့်ဆည်းသလား စစ်တယ်။

> **Important:** ဒီ Levels တွေကို Testing Scope နဲ့ Objective က ဆုံးဖြတ်တယ်။ Tool Name တစ်ခုတည်းနဲ့ မဆုံးဖြတ်ဘူး။ Level တစ်ခုက Pass ဖြစ်တာနဲ့ နောက် Level မှာ Bug မရှိတော့ဘူးလို့ မဆိုလိုဘူး။

## 2. Unit Testing

**Unit Testing** ဆိုတာ Function, Method, Class, Component တစ်ခုလို Small Testable Unit ကို Focus လုပ်ပြီး Test လုပ်ခြင်းဖြစ်တယ်။ Dependencies တွေကို Mock/Stub လုပ်ပြီး Isolate လုပ်နိုင်တယ်။

### Example — TypeScript + Vitest

Requirement (ဒီသင်ခန်းစာအတွက် Example): Proposal Title မှာ Whitespace ဖယ်ပြီး အနည်းဆုံး 5 Characters ရှိရမယ်။

```ts
// proposal.ts
export function isValidProposalTitle(title: string): boolean {
  return title.trim().length >= 5;
}
```

```ts
// proposal.test.ts
import { describe, expect, it } from 'vitest';
import { isValidProposalTitle } from './proposal';

describe('isValidProposalTitle', () => {
  it('accepts a valid title', () => {
    expect(isValidProposalTitle('Smart Agriculture')).toBe(true);
  });

  it('rejects a short title', () => {
    expect(isValidProposalTitle('IoT')).toBe(false);
  });

  it('rejects whitespace-only input', () => {
    expect(isValidProposalTitle('     ')).toBe(false);
  });
});
```

ဒီ Test တွေမှာ Browser, API Server နဲ့ Database မလိုဘူး။ Logic တစ်ခုကို သီးသန့်စစ်တာကြောင့် Fast ဖြစ်တတ်ပြီး Failure ကို Locate လုပ်ရလွယ်တယ်။ **ဒါပေမဲ့ Unit Test = Database လုံးဝမသုံးရ** ဆိုတဲ့ Absolute Rule မဟုတ်ဘူး။

### Arrange–Act–Assert (AAA)

- **Arrange:** Test Data နဲ့ Dependencies ပြင်ဆင်တယ်။
- **Act:** Test လုပ်မယ့် Function/Behavior ကို Execute လုပ်တယ်။
- **Assert:** Actual Result နဲ့ Expected Result ကို Compare လုပ်တယ်။

## 3. Integration Testing

**Integration Testing** က Components နှစ်ခုနဲ့အထက် ပေါင်းစည်းပြီး Interaction မှန်ကန်သလား စစ်တယ်။ ဥပမာ **Laravel API ↔ PostgreSQL Database**။

### Example — Laravel Feature Test

```php
public function test_student_can_submit_proposal(): void
{
    $student = User::factory()->create(['role' => 'student']);

    $response = $this->actingAs($student)
        ->postJson('/api/proposals', [
            'title' => 'Smart Agriculture',
            'description' => 'IoT monitoring system',
        ]);

    $response->assertCreated();

    $this->assertDatabaseHas('proposals', [
        'title' => 'Smart Agriculture',
        'student_id' => $student->id,
    ]);
}
```

ဒီ Code က **Illustrative Example** ဖြစ်ပြီး Actual Route, Factory, Required Fields, Auth Strategy နဲ့ Schema အလိုက် Adjust လုပ်ရမယ်။

**Key Point:** HTTP `201 Created` ပြန်တာနဲ့ Database ထဲ Record ရှိကြောင်း မသက်သေပြနိုင်ဘူး။ `assertDatabaseHas()` လို Assertion နဲ့ Persistence ကို Verify လုပ်ရမယ်။

Integration Test မှာ Detect လုပ်နိုင်တဲ့ Bugs — Wrong Database Column, Incorrect API Payload, Missing Database Update, Service-to-Service Contract Mismatch စတာတွေ။

## 4. System Testing

**System Testing** က Complete Integrated Application ရဲ့ Behavior ကို စစ်တယ်။

**Project infoSphere Workflow:**

1. Student Login ဝင်တယ်။
2. Proposal Submission Page ကို သွားတယ်။
3. Proposal Details ဖြည့်တယ်။
4. Submit လုပ်တယ်။
5. Success Message ပေါ်သလား စစ်တယ်။
6. Student Dashboard မှာ Proposal ပေါ်သလား စစ်တယ်။

### Example — Playwright

```ts
import { test, expect } from '@playwright/test';

test('student can submit a proposal', async ({ page }) => {
  // Precondition: authenticated student session is already configured.
  await page.goto('/proposals/new');
  await page.getByLabel('Title').fill('Smart Agriculture');
  await page.getByLabel('Description').fill('IoT monitoring system');
  await page.getByRole('button', { name: 'Submit Proposal' }).click();

  await expect(
    page.getByText('Proposal submitted successfully')
  ).toBeVisible();
});
```

ဒီ Code မှာ Authentication Setup, Required Fields, Test Data Cleanup နဲ့ Application Selectors တွေကို Actual Project အလိုက် ထည့်ရမယ်။ Success Message စစ်ခြင်းအပြင် Persisted State ကို Verify လုပ်နိုင်ရင် Test ပိုခိုင်မာတယ်။

> **System Testing vs E2E Testing:** System Testing က Testing Level ဖြစ်ပြီး E2E က Complete Workflow ကို စမ်းသပ်တဲ့ Approach ဖြစ်တယ်။ ဆက်စပ်ပေမဲ့ အဓိပ္ပာယ်တူမဟုတ်ဘူး။

## 5. Acceptance Testing

**Acceptance Testing** က Stakeholders ရဲ့ Needs နဲ့ **Acceptance Criteria** ကို ဖြည့်ဆည်းသလား စစ်တယ်။ **User Acceptance Testing (UAT)** က Common Example ဖြစ်တယ်။

### Given–When–Then Example

- **Given** a supervisor is assigned to a proposal,
- **When** the supervisor approves the proposal,
- **Then** the proposal status should become `approved`.

University Staff တွေက Actual Workflow နဲ့ ကိုက်ညီသလား Verify လုပ်နိုင်တယ်။ ဥပမာ Substitute Supervisor Approval လို Requirement မပါသေးတာကို တွေ့နိုင်တယ်။ Technical Tests Pass ဖြစ်နေပေမဲ့ Business Need မပြည့်မီနိုင်သေးတယ်။

## 6. Comparison Table

| Level | Focus | Project infoSphere Example | Typical Tools |
|---|---|---|---|
| Unit | Individual Function/Component | `canApproveProposal()` Logic | Vitest, Pest, PHPUnit |
| Integration | Components Interaction | Laravel Approval API ↔ PostgreSQL | Pest, PHPUnit, Supertest |
| System | Complete Integrated System | Login → Submit → Approve Workflow | Playwright, Manual Testing |
| Acceptance | Business Requirements | University Staff UAT | UAT Scenarios, Manual/Automated Acceptance Tests |

**Remember:** Multiple Testing Levels က Different Risks တွေကို Detect လုပ်ပေးတယ်။ Project Requirements, Risks နဲ့ Resources အလိုက် Testing Strategy ကို ရွေးရမယ်။

## 7. Hands-on Exercise — Identify the Testing Level

**Scenario A:** Password Validation Function ကို API/Database မခေါ်ဘဲ Test လုပ်တယ်။  
**Answer:** Unit Testing — Individual Logic ကို Isolate လုပ်ထားတယ်။

**Scenario B:** Laravel API က Proposal ကို PostgreSQL ထဲ Save လုပ်သလား Test လုပ်တယ်။  
**Answer:** Integration Testing — API နဲ့ Database Interaction ကို စစ်တယ်။

**Scenario C:** Browser မှာ Login → Proposal Submission → Dashboard Flow ကို Test လုပ်တယ်။  
**Answer:** System Testing — Complete Integrated Workflow ကို စစ်တယ်။

**Scenario D:** University Staff က Approval Workflow ကို Operational Requirements နဲ့ Compare လုပ်တယ်။  
**Answer:** Acceptance Testing — Business Needs ကို Evaluate လုပ်တယ်။

**Scenario E:** Mocked Dependencies သုံးပြီး React Form Error Display ကို Test လုပ်တယ်။  
**Answer:** Unit-level Component Test — Isolated Component Behavior ကို စစ်တယ်။

## 8. Hands-on Mini Challenge — Your Original Answers & Review

**Question 1:** `canApproveProposal()` Function, Laravel API–Database Update, Full Workflow, University Staff Review ကို Testing Levels ခွဲပါ။

**Your Original Answer:**

> A=unit testing, B=integration testing, C=system testing, D=acceptance testing

**Review: Correct (1/1).** Scope နဲ့ Objective အလိုက် မှန်ကန်စွာ ခွဲနိုင်တယ်။

**Question 2:** Unit Tests အားလုံး Pass ဖြစ်ရင် Integration Testing လိုသေးသလား?

**Your Original Answer:**

> Yes, integration testing is still needed as we can't verify testing only by unit tests passed.

**Review: Correct (1/1).** Unit Tests Pass ဖြစ်တာက Components တွေ အတူတူအလုပ်လုပ်တဲ့အခါ မှန်ကန်ကြောင်း Guarantee မပေးနိုင်ဘူး။ API–DB Interaction မှာ Defects ရှိနိုင်တယ်။

**Improved English:**

> Yes, integration testing is still necessary because passing unit tests does not guarantee that different components work correctly together.

**Question 3:** Full Stack Developer က Testing Level တစ်ခုတည်း သုံးသင့်သလား?

**Your Original Answer:**

> No, we need to test the system or software using different type of testing, from unit to acceptance testing.

**Review: Correct (1/1).** Different Levels တွေက Different Risks တွေကို စစ်တယ်။ `different type of testing` ထက် `different testing levels` က ဒီ Context မှာ ပိုတိကျတယ်။

**Improved English:**

> No. A full stack developer should use multiple testing levels because each level addresses different risks and aspects of software quality. The testing strategy should be based on project requirements, complexity, risks, and resources.

### Final Result

**3/3 — Passed. Lesson 01 Completed.**

## 9. Professional English Model Answers

1. **A — Unit Testing:** The `canApproveProposal()` function is tested independently. **B — Integration Testing:** The Laravel Approval API is tested together with the database. **C — System Testing:** The complete proposal workflow is tested across the integrated application. **D — Acceptance Testing:** University staff evaluate whether the workflow meets their business requirements.
2. **Yes.** Integration testing is still necessary because passing unit tests does not guarantee that components work correctly together. Interaction defects may remain even when individual functions behave correctly.
3. **No.** A full stack developer should apply multiple testing levels according to project risk. Unit, integration, system, and acceptance testing provide different evidence about software quality.

## 10. Quick Revision Quiz

1. What is the difference between Unit Testing and Integration Testing?
2. Does a successful API Status Code guarantee database persistence?
3. Why can Acceptance Testing fail even when technical tests pass?
4. Is Playwright exclusively a System Testing tool?

**Answers:** (1) Individual Unit vs Interaction; (2) No; (3) Unmet Business Needs; (4) No, Test Scope/Objective matters.

## Key Takeaways

- **Unit → Integration → System → Acceptance** ဆိုတာ Testing Scope အလိုက် Conceptual Progression ဖြစ်တယ်။
- Unit Tests Pass ဖြစ်တာနဲ့ Integration Tests မလိုတော့ဘူးလို့ မဆိုလိုဘူး။
- HTTP Success Status နဲ့ Actual Persisted State ကို သီးခြား Verify လုပ်သင့်တယ်။
- Testing Level ကို Tool မဟုတ်ဘဲ **Objective and Scope** က ဆုံးဖြတ်တယ်။
