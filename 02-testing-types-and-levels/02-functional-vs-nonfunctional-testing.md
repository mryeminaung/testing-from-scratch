# Lesson 02 — Functional vs. Non-functional Testing

> **Testing from Scratch · Module 02: Testing Types and Levels**  
> Language: မြန်မာ (English Technical Terms မပြောင်းထားပါ)  
> **Status: Lesson Explained; Mini Challenge Model Answers Included**

## Learning Objectives

ဒီ Lesson ပြီးရင် **Functional Testing** နဲ့ **Non-functional Testing** ကို ခွဲခြားနိုင်ရမယ်။ Performance, Security, Usability, Reliability, Accessibility နဲ့ Compatibility Testing ကို Full Stack Project Scenarios နဲ့ ရှင်းပြနိုင်ရမယ်။ Security နဲ့ Functional Testing Overlap ဖြစ်နိုင်ပုံ၊ Risk-based Prioritization ကိုလည်း နားလည်ရမယ်။

## 1. Functional Testing ဆိုတာဘာလဲ?

**Functional Testing** က Features နဲ့ Behaviors တွေဟာ သတ်မှတ်ထားတဲ့ **Functional Requirements** အတိုင်း အလုပ်လုပ်သလား စစ်တယ်။

> **Key Question: What does the system do?**

Project infoSphere Examples —

- Student က Valid Credentials နဲ့ Login ဝင်နိုင်သလား?
- Student က Proposal Submit လုပ်နိုင်သလား?
- Assigned Supervisor က Proposal Approve လုပ်နိုင်သလား?
- Unauthorized User ကို Approval API က Reject လုပ်သလား?
- Successful Approval ဖြစ်ရင် Database Status က `approved` ဖြစ်သလား?

### Login Feature — Functional Test Cases

| ID | Input | Expected Result |
|---|---|---|
| TC-LOGIN-001 | Valid Email + Valid Password | Login Successful |
| TC-LOGIN-002 | Valid Email + Wrong Password | Login Rejected |
| TC-LOGIN-003 | Empty Email | Validation Error |
| TC-LOGIN-004 | Empty Password | Validation Error |
| TC-LOGIN-005 | Invalid Credentials | No Authenticated Session |

### Laravel Feature Test Example

```php
public function test_student_can_login_with_valid_credentials(): void
{
    $student = User::factory()->create([
        'email' => 'student@example.test',
        'password' => Hash::make('TestPassword123!'),
    ]);

    $response = $this->postJson('/api/login', [
        'email' => 'student@example.test',
        'password' => 'TestPassword123!',
    ]);

    $response->assertOk();
}
```

**Important:** ဒီ Code က Illustrative Example ဖြစ်တယ်။ Actual Login Endpoint, Authentication Contract, Test Database နဲ့ Factories အလိုက် ပြင်ရမယ်။ `200 OK` တစ်ခုတည်းနဲ့ Authentication အောင်မြင်ကြောင်း အပြည့်အဝ မသက်သေပြနိုင်ဘူး။ Token, Session သို့မဟုတ် Protected Endpoint Access ကိုပါ Verify လုပ်သင့်တယ်။

## 2. Non-functional Testing ဆိုတာဘာလဲ?

**Non-functional Testing** က Software ရဲ့ **Quality Characteristics** တွေကို Evaluate လုပ်တယ်။

> **Key Question: How well does the system work?**

ဥပမာ Login Feature အလုပ်လုပ်ပေမဲ့ 15 Seconds ကြာနေတယ်၊ Users များရင် Server Crash ဖြစ်တယ်၊ Mobile UI သုံးရခက်တယ်ဆိုရင် Non-functional Issues ရှိနေနိုင်တယ်။

### Common Non-functional Testing Types

| Type | Focus | Example |
|---|---|---|
| **Performance** | Response Time, Throughput, Resource Usage | Proposal List API ရဲ့ Response Time |
| **Security** | Confidentiality, Access Control, Data Protection | Unauthorized Access Prevention |
| **Usability** | Easy to Learn and Use | Proposal Form ကို ရှင်းလင်းစွာ ဖြည့်နိုင်ခြင်း |
| **Reliability** | Stable Operation | IoT Monitoring ရေရှည်အလုပ်လုပ်နိုင်ခြင်း |
| **Accessibility** | Inclusive Access | Keyboard-only Navigation, Screen Reader Labels |
| **Compatibility** | Supported Platforms | Chrome, Firefox, Mobile Browsers |

**Nuance:** Security Testing မှာ Functional Authorization Checks တွေလည်း ပါနိုင်တယ်။ Categories တွေဟာ Strictly Mutually Exclusive မဟုတ်ဘူး။

## 3. Functional vs. Non-functional — Comparison

| Aspect | Functional | Non-functional |
|---|---|---|
| Main Question | What does it do? | How well does it work? |
| Focus | Feature Behavior | Quality Characteristics |
| Examples | Login, CRUD, Approval | Performance, Reliability, Accessibility |
| Expected Results | Correct Output, State, Action | Measurable Quality Criteria |
| Typical Tools | Pest, Vitest, Postman, Playwright | k6, Lighthouse, Playwright, Security Testing Tools |

Tool တစ်ခုတည်းကို Testing Categories နှစ်ခုလုံးအတွက် သုံးနိုင်တယ်။ Tool Name တစ်ခုတည်းက Testing Category ကို မဆုံးဖြတ်ဘူး။

## 4. Project infoSphere — Proposal Approval Example

### Functional Requirements

1. Assigned Supervisor က Proposal ကို Approve လုပ်နိုင်ရမယ်။
2. Unassigned Supervisor က Proposal Approve မလုပ်နိုင်ရဘူး။
3. Successful Approval ဖြစ်ရင် Database Status က `approved` ဖြစ်ရမယ်။
4. Student က Supervisor-only Approval Action ကို မလုပ်နိုင်ရဘူး။

### Non-functional Requirements (Illustrative Targets)

1. သတ်မှတ်ထားတဲ့ Workload အောက်မှာ Approval API ရဲ့ **95th Percentile Response Time** က 1 Second ထက်နည်းရမယ်။
2. Sensitive Data ကို Unauthorized Users ဆီ မဖော်ပြရဘူး။
3. Approval UI ကို Keyboard နဲ့ အသုံးပြုနိုင်ရမယ်။
4. Supported Browsers တွေမှာ Workflow အလုပ်လုပ်ရမယ်။

> ဒီ Numbers/Targets တွေက သင်ခန်းစာအတွက် Examples ပဲဖြစ်ပြီး Actual Project Requirements မဟုတ်ဘူး။

### Test Case Matrix

| Test Case | Testing Category | Expected Result |
|---|---|---|
| Assigned Supervisor Approves | Functional | DB Status becomes `approved` |
| Student Attempts Approval | Functional + Security-related | Rejected, No Unauthorized DB Change |
| Approval API Under Expected Load | Performance | Meets Agreed Target |
| Keyboard-only Approval | Accessibility | Controls are Operable |
| Approval on Supported Browsers | Compatibility | Workflow Works |

## 5. ESP32 Smart Agriculture Monitoring Example

**Illustrative Data Flow:** ESP32 Sensor → Express API → Database → React Dashboard

### Functional Checks

- ESP32 က Sensor Data ပို့နိုင်သလား?
- Express API က Valid Readings ကို လက်ခံသလား?
- Database ထဲ Correct Values Save ဖြစ်သလား?
- Dashboard မှာ Correct Readings ပြသသလား?

### Non-functional Checks

- Dashboard Data Update Latency ဘယ်လောက်ရှိသလဲ?
- Network Disconnect ပြီးနောက် Recover ဖြစ်သလား?
- Large Data Volume အောက်မှာ API Performance ဘယ်လိုရှိသလဲ?
- Mobile Device မှာ Dashboard သုံးရလွယ်သလား?

Functional Testing က **Correct Data Flow** ကို စစ်တယ်။ Non-functional Testing က **Data Flow Quality** ကို စစ်တယ်။

## 6. Writing Measurable Non-functional Requirements

**Weak:** “The application should be fast.”

**Improved (Illustrative):**

> Under a defined workload of 50 concurrent users, the Proposal List API should achieve a 95th percentile response time below 1 second in the specified test environment.

ဒီ Requirement မှာ —

- **Workload:** 50 Concurrent Users
- **Metric:** 95th Percentile Response Time
- **Target:** Below 1 Second
- **Environment:** Specified Test Environment

ဆိုပြီး Testable ဖြစ်လာတယ်။ Actual Threshold ကို Stakeholders, Expected Usage နဲ့ Infrastructure အလိုက် သတ်မှတ်ရမယ်။

## 7. Common Misconceptions

1. **Functional Tests Pass = Software Quality Perfect?** မဟုတ်ဘူး။ Performance, Security, Usability Issues ရှိနိုင်တယ်။
2. **Non-functional = Performance Only?** မဟုတ်ဘူး။ Reliability, Accessibility, Compatibility စတာတွေလည်း ပါတယ်။
3. **Security = Non-functional Only?** မဟုတ်ဘူး။ Authorization Rule Enforcement က Functional Behavior လည်းဖြစ်တယ်။
4. **Non-functional Tests ကို Production ရောက်မှ လုပ်ရမလား?** မဟုတ်ဘူး။ Design/Development အစောပိုင်းကတည်းက Planning နဲ့ Checks လုပ်နိုင်တယ်။

## 8. Practice Quiz — Functional or Non-functional?

| Scenario | Answer | Reason |
|---|---|---|
| Student Valid Credentials နဲ့ Login | Functional | Login Behavior |
| Proposal List API Response Time Target | Non-functional — Performance | Response Time Quality |
| Assigned Supervisor Approves Proposal | Functional | Approval Behavior |
| Keyboard-only Dashboard Navigation | Non-functional — Accessibility | Inclusive Operability |
| ESP32 Sensor Value DB ထဲ Correct Save | Functional | Data Persistence Behavior |
| IoT System Network Interruption ပြီး Recover | Non-functional — Reliability | Recoverability |

## 9. Hands-on Mini Challenge — Scenario

Project infoSphere Proposal Approval Feature မှာ Findings 4 ခု ရှိတယ်။

- **Finding A:** Assigned Supervisor က Approve လုပ်ပေမဲ့ Database Status က `pending` ဖြစ်နေတယ်။
- **Finding B:** Approval API Response Time က Expected Load အောက်မှာ 8 Seconds ဖြစ်နေတယ်။
- **Finding C:** Approval Button ကို Keyboard နဲ့ Focus မလုပ်နိုင်ဘူး။
- **Finding D:** Student က Supervisor-only Approval API ကို Access လုပ်နိုင်နေတယ်။

### Question 1 — Classification

| Finding | Model Answer | Reason |
|---|---|---|
| A | **Functional Testing** | Expected Approval Behavior / DB State မမှန်ဘူး |
| B | **Non-functional — Performance** | Response Time Quality ကို စစ်တယ် |
| C | **Non-functional — Accessibility** | Keyboard Navigation Requirement မပြည့်ဘူး |
| D | **Functional + Security Testing** | Authorization Rule ချိုးဖောက်ပြီး Security Risk ဖြစ်တယ် |

### Question 2 — Finding B က ဘယ် Type လဲ?

**Model Answer:** **Performance Testing** ဖြစ်တယ်။ Response Time ကို Agreed Performance Target, Workload နဲ့ Environment နဲ့ Compare လုပ်ရမယ်။ **8 Seconds တစ်ခုတည်းနဲ့ Requirement Fail လို့ မဆုံးဖြတ်သင့်ဘူး** — Target နဲ့ Test Conditions ကို အတည်ပြုရမယ်။

### Question 3 — Finding D က Security Issue လား? Functional နဲ့ ဆက်စပ်သလား?

**Model Answer:** Yes. Student က Supervisor-only Approval Action ကို လုပ်နိုင်နေတယ်ဆိုရင် **Broken Access Control / Authorization Failure** ဖြစ်နိုင်တယ်။ Student Role ကို Reject လုပ်ရမယ်ဆိုတဲ့ **Functional Authorization Requirement** ကိုလည်း ချိုးဖောက်နေတယ်။ ဒါကြောင့် Functional နဲ့ Security Testing နှစ်မျိုးလုံးနဲ့ သက်ဆိုင်တယ်။

### Question 4 — Testing Time 2 Hours ကျန်ရင် Priority ဘယ်လိုပေးမလဲ?

**Model Answer:** **Finding D ကို အရင်ဆုံး Prioritize** လုပ်မယ်။ Unauthorized Approval က Access Control နဲ့ Business Data Integrity ကို ထိခိုက်စေနိုင်တယ်။

Illustrative Risk-based Priority —

1. **D — Unauthorized Approval:** High Security / Data Integrity Risk
2. **A — Approval Status Not Updated:** Core Workflow Failure
3. **B — Slow API:** Performance Impact; Target နဲ့ Workload အပေါ်မူတည်
4. **C — Keyboard Accessibility:** User Needs / Compliance အပေါ်မူတည်ပြီး Priority မြင့်နိုင်တယ်

> **Nuance:** ဒီ Ranking က Absolute မဟုတ်ဘူး။ Actual Impact, Affected Users, Release Criteria, Severity နဲ့ Likelihood အလိုက် ပြောင်းနိုင်တယ်။ 2 Hours ဆိုတာ Investigation, Verification, Reporting နဲ့ Risk Communication ကို ဦးစားပေးစီမံဖို့ Constraint ဖြစ်တယ်။

## 10. Professional English Model Answers

**Q1 — Classification**

> Finding A is a functional defect because the proposal status is not updated as expected. Finding B is a performance concern because the API response time must be evaluated against the agreed performance target. Finding C is an accessibility issue because the approval button cannot be reached using a keyboard. Finding D is both a functional authorization failure and a security issue because students can access a supervisor-only operation.

**Q2 — Performance**

> Finding B relates to performance testing. We need to compare the observed response time against measurable requirements under a defined workload and test environment. An eight-second response time alone does not establish whether the agreed performance requirement has been violated.

**Q3 — Security and Functional Overlap**

> Yes. Finding D may represent a broken access control vulnerability. It also violates the functional authorization requirement that only authorized supervisors may perform approval actions. Therefore, it is relevant to both functional and security testing.

**Q4 — Risk-based Priority**

> I would prioritize Finding D because it represents a potentially serious authorization vulnerability. Allowing students to access a supervisor-only approval API could compromise access control and business data integrity. I would investigate and verify this issue first, followed by the failed approval workflow in Finding A. The remaining findings should be prioritized according to their measured impact, accessibility requirements, and release risks.

### Exercise Status

**Model Answers provided by assistant at learner's request.** ဒီ Lesson မှာ Student Original Answers မရှိသေးလို့ Model Answers ကိုသာ ထည့်ထားတယ်။ Learner ဖြေထားသလို မဖော်ပြထားဘူး။

## 11. Quick Revision Quiz

1. Functional Testing ရဲ့ Main Question ကဘာလဲ?
2. Non-functional Testing မှာ Performance အပြင် ဘာတွေ ပါသလဲ?
3. Unauthorized Approval API Access က ဘာကြောင့် Functional နဲ့ Security နှစ်မျိုးလုံးနဲ့ သက်ဆိုင်သလဲ?
4. “The system should be fast” က ဘာကြောင့် Weak Requirement ဖြစ်သလဲ?

**Answers:** (1) What does the system do? (2) Reliability, Accessibility, Usability, Security, Compatibility, etc. (3) Authorization Behavior + Security Risk; (4) No measurable workload, metric, target, environment.

## Key Takeaways

- **Functional Testing = Correct Features and Behaviors.**
- **Non-functional Testing = Quality Characteristics and Constraints.**
- Security နဲ့ Functional Testing က Overlap ဖြစ်နိုင်တယ်။
- Non-functional Requirements တွေကို **Measurable** ဖြစ်အောင် ရေးရမယ်။
- Limited Testing Time မှာ **Risk-based Prioritization** အသုံးပြုရမယ်။
