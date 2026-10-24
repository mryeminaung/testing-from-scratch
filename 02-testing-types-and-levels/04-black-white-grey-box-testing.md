# Testing from Scratch — Module 02, Lesson 04
## Black-box, White-box & Grey-box Testing

> **Language:** Burmese explanations with English technical terms  
> **Project Example:** Project infoSphere (React + Laravel + PostgreSQL)  
> **Status:** Lesson taught; Exercises include sample/model answers (not submitted learner answers).

## Learning Objectives
ဒီ Lesson ပြီးရင် Tester ရဲ့ Internal Implementation Knowledge အပေါ်မူတည်ပြီး **Black-box**, **White-box**, **Grey-box** Testing Approaches တွေကို ခွဲခြားနိုင်မယ်။ Requirements, Code Structure, Database Schema တွေကို ဘယ်လိုအသုံးချပြီး Test Cases Design လုပ်မလဲဆိုတာ နားလည်မယ်။

## 1. Big Picture‌ေ
| Approach | Knowledge | Main Focus |
|---|---|---|
| **Black-box** | Internal Code မသိလည်းရ | Input, Output, Requirements, Behavior |
| **White-box** | Internal Code Structure သိ | Branches, Conditions, Paths, Logic |
| **Grey-box** | Internal Architecture အချို့သိ | External Behavior + Partial Internal Knowledge |

**Important:** ဒီသုံးမျိုးက **Testing Approaches / Techniques** ဖြစ်တယ်။ Unit, Integration, System, Acceptance တို့လို **Testing Levels** မဟုတ်ဘူး။

## 2. Black-box Testing
**Definition:** Source Code, Algorithms နဲ့ Implementation Details တွေကို မကြည့်ဘဲ Requirements နဲ့ Expected Behaviors အပေါ်မူတည်ပြီး Test Cases Design လုပ်တာ။

**Main Question:** *What does the system do?*

### Example — infoSphere Login
Requirement Example:
- Valid Credentials → Login Success
- Wrong Password → Authentication Rejected
- Empty Email → Validation Error
- Unauthenticated Protected API Request → HTTP 401

| Test ID | Input | Expected Result |
|---|---|---|
| TC-LOGIN-01 | Valid email/password | Login succeeds |
| TC-LOGIN-02 | Wrong password | Authentication rejected |
| TC-LOGIN-03 | Empty email | Validation error |
| TC-LOGIN-04 | No authentication token/session | Protected endpoint rejects request |

### Playwright Example
```typescript
import { test, expect } from '@playwright/test';

test('shows an error for a wrong password', async ({ page }) => {
  await page.goto('/login');
  await page.getByLabel('Email').fill('student@example.com');
  await page.getByLabel('Password').fill('wrong-password');
  await page.getByRole('button', { name: 'Login' }).click();
  await expect(page.getByText('Invalid credentials')).toBeVisible();
});
```

**Advantages:** User Perspective, Requirement Coverage, Source Access မလို။  
**Limitations:** Internal Branches မမြင်ရ၊ Hidden Logic Errors လွတ်နိုင်၊ Test Cases ထပ်နိုင်။

> Note: Test Credentials, UI Labels, Error Messages တွေက Illustrative Examples ဖြစ်တယ်။ Actual App Requirements အလိုက် ပြင်ပါ။

## 3. White-box Testing
**Definition:** Code Structure, `if/else` Branches, Conditions, Loops, Internal Logic တွေကို သိပြီး Test Cases Design လုပ်တာ။

**Main Question:** *How does the system work internally?*

### Example — Approval Authorization Logic
```typescript
export function canApproveProposal(
  role: string,
  isAssigned: boolean,
  status: string
): boolean {
  if (role !== 'supervisor') return false;
  if (!isAssigned) return false;
  if (status !== 'pending') return false;
  return true;
}
```

Internal Conditions သုံးခုရှိတာကို သိထားလို့ Return Paths ကို Test Cases နဲ့ Cover လုပ်နိုင်တယ်။

| Case | Role | Assigned | Status | Expected |
|---|---|---|---|---|
| 1 | student | true | pending | false |
| 2 | supervisor | false | pending | false |
| 3 | supervisor | true | approved | false |
| 4 | supervisor | true | pending | true |

### Vitest Example
```typescript
import { describe, it, expect } from 'vitest';
import { canApproveProposal } from './approval';

describe('canApproveProposal', () => {
  it('rejects non-supervisors', () => {
    expect(canApproveProposal('student', true, 'pending')).toBe(false);
  });
  it('rejects unassigned supervisors', () => {
    expect(canApproveProposal('supervisor', false, 'pending')).toBe(false);
  });
  it('rejects non-pending proposals', () => {
    expect(canApproveProposal('supervisor', true, 'approved')).toBe(false);
  });
  it('allows assigned supervisors for pending proposals', () => {
    expect(canApproveProposal('supervisor', true, 'pending')).toBe(true);
  });
});
```

### Code Coverage
| Metric | Meaning |
|---|---|
| Statement Coverage | Statements တွေ Execute ဖြစ်မှု |
| Branch Coverage | Decision Outcomes တွေ Execute ဖြစ်မှု |
| Condition Coverage | Individual Boolean Conditions ရဲ့ True/False Evaluation |
| Path Coverage | Execution Paths တွေ Cover ဖြစ်မှု |

**100% Branch Coverage ≠ 100% Bug-free.** Coverage က Execution ကိုတိုင်းတာတာ၊ Requirements မှန်/မမှန်ကို အာမမခံဘူး။

**Advantages:** Logic Defects, Uncovered Branches, Dead Code တွေ ရှာနိုင်။  
**Limitations:** Source Knowledge လို၊ Implementation ပြောင်းရင် Test Maintenance လို၊ Missing Requirements ကို Code ကြည့်ရုံနဲ့ မတွေ့နိုင်။

## 4. Grey-box Testing
**Definition:** Database Schema, API Design, System Architecture လို Internal Information အချို့ကို သိထားပေမဲ့ External Behavior ကို အဓိက Test လုပ်တဲ့ Approach ဖြစ်တယ်။

**Main Question:** *Does externally observed behavior match the system design and stored state?*

### Example — Proposal Submission API + Database
Tester က React → Laravel API → PostgreSQL Data Flow ကို သိထားတယ်။ `proposals` Table ရှိတာကိုလည်း သိတယ်။ ဒါပေမဲ့ Controller Source Code ကို အသေးစိတ် မဖတ်ဘူး။

1. Student Login ဝင်တယ်။
2. Proposal Submit လုပ်တယ်။
3. API Response က `201 Created` ဖြစ်သလား စစ်တယ်။
4. `proposals` Table ထဲ Record တကယ်ရှိသလား စစ်တယ်။
5. Status က `pending` ဖြစ်သလား Verify လုပ်တယ်။

### Laravel Feature Test Example
```php
public function test_student_can_submit_proposal(): void
{
    $student = User::factory()->create(['role' => 'student']);

    $response = $this->actingAs($student)
        ->postJson('/api/proposals', [
            'title' => 'Smart Agriculture System',
        ]);

    $response->assertCreated();

    $this->assertDatabaseHas('proposals', [
        'title' => 'Smart Agriculture System',
        'status' => 'pending',
    ]);
}
```

**Nuance:** Grey-box လို့ ခေါ်နိုင်တာက Test Design မှာ Internal Architecture/DB Knowledge အချို့ကို သုံးထားလို့ဖြစ်တယ်။ Tester က Source Code အပြည့်သိပြီး Internal Logic ကို အခြေခံရေးထားရင် White-box Characteristics လည်း ရှိနိုင်တယ်။

**Advantages:** API/DB Consistency, Data Integrity, Integration Problems တွေကို ထိထိရောက်ရောက် စစ်နိုင်။  
**Limitations:** Internal Information အချို့လို၊ Architecture ပြောင်းလဲရင် Tests Update လိုနိုင်။

## 5. Comparison
| Feature | Black-box | White-box | Grey-box |
|---|---|---|---|
| Source Knowledge | Not required | Required | Partial |
| Main Basis | Requirements | Code Structure | Requirements + Architecture |
| Focus | Inputs/Outputs | Internal Logic | Behavior + Internal Data |
| Typical Example | UI Login Test | Branch-focused Unit Test | API + DB Verification |

**Reminder:** Tool တစ်ခုတည်းက Approach ကို မဆုံးဖြတ်ဘူး။ Playwright, Vitest, Laravel/Pest တို့ကို Objective နဲ့ Test Design ပေါ်မူတည်ပြီး Approach မတူအောင် သုံးနိုင်တယ်။

## 6. Full Stack Workflow Example
Project infoSphere Approval Feature ကို Test လုပ်တဲ့အခါ:
1. **White-box:** `canApproveProposal()` Logic, Conditions, Return Paths ကို Test လုပ်တယ်။
2. **Grey-box:** Approval API Response နဲ့ Database Status ကို Verify လုပ်တယ်။
3. **Black-box:** Student/Supervisor UI Workflow ကို User Perspective ကနေ Test လုပ်တယ်။

ဒီ Order က Illustrative ဖြစ်တယ်။ Project Risks နဲ့ Development Workflow အလိုက် ပြောင်းနိုင်တယ်။

## 7. Knowledge Check — Questions with Model Answers
1. **UI Approval Button နှိပ်ပြီး Success Message စစ်တယ်; Code မကြည့်ဘူး။** → Black-box Testing.
2. **`if/else` Branches အားလုံး Execute ဖြစ်အောင် Unit Tests ရေးတယ်။** → White-box Testing.
3. **API Response + Database Table Update ကို Schema Knowledge သုံးပြီး စစ်တယ်; Controller Code မကြည့်ဘူး။** → Grey-box Testing.
4. **Branch Coverage 100% ဆိုတာ ဘာကိုဆိုလိုသလဲ?** → Measured Branch Outcomes အားလုံး Execute ဖြစ်ခဲ့တယ်; Bug-free ဖြစ်ကြောင်း မဟုတ်။

## 8. Practical Exercise — Authorization Bug
**Scenario:** Student က Supervisor-only Approval API ကို Direct Request ပို့တဲ့အခါ `200 OK` ပြန်လာပြီး Proposal ကို Approve လုပ်နိုင်နေတယ်။

**Question:** ဒီ Bug ကို Black-box, White-box, Grey-box Testing သုံးမျိုးနဲ့ ဘယ်လို Detect/Investigate လုပ်မလဲ?

### Sample Model Answers (Learner Answer မဟုတ်)

**1. Black-box Testing**  
Student Account နဲ့ Login ဝင်ပြီး Supervisor-only Approval Endpoint ကို API Request ပို့မယ်။ Requirement အရ Access Denied (ဥပမာ App Contract အပေါ်မူတည်ပြီး HTTP `403 Forbidden`) ဖြစ်သင့်တယ်။ `200 OK` ပြန်လာပြီး Proposal Status ပြောင်းသွားရင် Authorization Functional Defect ဖြစ်တယ်။ Source Code မကြည့်ဘဲ Input, Expected Output, Actual Behavior ကို Compare လုပ်တယ်။

**2. White-box Testing**  
Laravel Controller, Middleware, Policy/Gate, Role Checks နဲ့ `canApproveProposal()` Logic ကို Review လုပ်မယ်။ Student Role အတွက် Deny Branch ကို Test လုပ်မယ်။ Assigned/Unassigned Supervisor, Pending/Approved Status စတဲ့ Branches တွေကိုလည်း Cover လုပ်မယ်။ Authorization Check မရှိတာ၊ Incorrect Boolean Logic သုံးတာ၊ Policy မချိတ်ထားတာတွေကို Investigate လုပ်မယ်။

**3. Grey-box Testing**  
API Endpoint, Role Model, Database Schema ကို သိထားပြီး Student Account နဲ့ Approval Request ပို့မယ်။ Response Code နဲ့ Database `proposals.status` ကို Compare လုပ်မယ်။ Expected Behavior က Request Rejected ဖြစ်ပြီး Status မပြောင်းရဘူး။ API Response `200` ဖြစ်တာသာမက DB မှာ `approved` ဖြစ်သွားတာကို Confirm လုပ်ပြီး Access Control Defect အဖြစ် Report လုပ်မယ်။

### Professional English Model Answer
**Black-box:** I would send an approval request using a student account and compare the response with the authorization requirements. The request should be denied, and the proposal must not be approved.

**White-box:** I would inspect the authorization middleware, policies, and approval logic. I would write tests for the branches that reject students, unassigned supervisors, and invalid proposal states.

**Grey-box:** Using knowledge of the API and database schema, I would submit an approval request as a student and verify both the HTTP response and the stored proposal status. A denied request must not change the database state.

## 9. Common Misconceptions
- **Black-box = Only Manual Testing** — မဟုတ်ဘူး; Automation လည်း လုပ်နိုင်တယ်။
- **White-box = Only Unit Testing** — မဟုတ်ဘူး; Integration-level Logic ကိုလည်း White-box Approach နဲ့ Test လုပ်နိုင်တယ်။
- **Grey-box = Half the Source Code Read** — မဟုတ်ဘူး; Partial Internal Knowledge ကို Test Design အတွက် အသုံးချတာ။
- **100% Coverage = Bug-free** — မဟုတ်ဘူး; Coverage က Execution Metrics ပဲ။

## 10. Quick Revision
**Black-box:** Requirements + Inputs/Outputs; internal code မကြည့်။  
**White-box:** Internal Code + Branches/Conditions; logic ကို သိ။  
**Grey-box:** External Behavior + Partial Internal Knowledge; API/DB Schema ကို အသုံးချ။

**Next Lesson:** Exploratory Testing & Ad-hoc Testing.
