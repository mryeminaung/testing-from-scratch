# Lesson 01 — What is Software Testing?

**Status:** Completed  
**Goal:** Software Testing ရဲ့ အဓိပ္ပာယ်၊ အခြေခံ Terms နဲ့ Test Thinking ကို နားလည်ရန်။

## 1. Definition
**Software Testing** ဆိုတာ Software ရဲ့ Behavior, Functionality နဲ့ Quality ကို Requirements/Expected Results တွေနဲ့ နှိုင်းယှဉ်အကဲဖြတ်ပြီး Defects ရှိနိုင်တဲ့နေရာတွေကို ရှာဖွေဖို့ လုပ်ဆောင်တဲ့ Activities တွေ ဖြစ်ပါတယ်။

Testing လုပ်တယ်ဆိုတာ Application ကို Click လုပ်ကြည့်ရုံတင် မဟုတ်ဘူး။ **ဘာဖြစ်သင့်သလဲ (Expected Result)** နဲ့ **တကယ်ဘာဖြစ်သလဲ (Actual Result)** ကို စနစ်တကျ နှိုင်းယှဉ်ရတာပါ။ Testing က Bugs လုံးဝမရှိကြောင်း အာမခံမပေးနိုင်ပါ။

## 2. Why do we test?
- **Defect Detection:** မှားယွင်းတဲ့ Behavior ကို ရှာဖွေရန်
- **Requirement Checking:** Feature က Requirement ကို ဖြည့်ဆည်းသလား စစ်ရန်
- **Risk Reduction:** Security, Data Integrity နဲ့ Reliability Risks ကို လျှော့ချရန်
- **Regression Detection:** Feature အသစ်ကြောင့် Feature အဟောင်း ပျက်သွားသလား သိရန်
- **Release Confidence:** Deploy လုပ်ဖို့ Evidence ရရှိရန်

## 3. Testing vs. Debugging
| Testing | Debugging |
|---|---|
| Defect ရှိနိုင်ကြောင်း ဖော်ထုတ်တယ် | Defect ရဲ့ Root Cause ကို ရှာတယ် |
| Expected vs Actual ကို နှိုင်းယှဉ်တယ် | Code ကို Trace/Modify လုပ်တယ် |
| Tester နဲ့ Developer နှစ်ဖက်လုံး လုပ်နိုင်တယ် | အများအားဖြင့် Developer က Fix လုပ်တယ် |

**Typical Flow:** Test → Find Defect → Debug → Fix → Retest → Regression Test.

## 4. Core Terminology
| Term | မြန်မာလို ရှင်းလင်းချက် |
|---|---|
| Requirement | Software က လုပ်ပေးရမယ့် သတ်မှတ်ချက် |
| Test Scenario | ဘယ် Behavior/Feature ကို စမ်းမလဲဆိုတဲ့ အကြမ်းဖျဉ်းအခြေအနေ |
| Test Case | Preconditions, Steps, Data, Expected Result ပါတဲ့ အသေးစိတ်စမ်းသပ်ချက် |
| Test Data | Test မှာ သုံးတဲ့ Input |
| Expected Result | ဖြစ်သင့်တဲ့ Result |
| Actual Result | တကယ်ရရှိတဲ့ Result |
| Defect/Bug | Expected Behavior နဲ့ Actual Behavior မကိုက်ညီမှု |
| Test Environment | Test Run လုပ်တဲ့ Software/Hardware/Configuration |

## 5. Full Stack Example — Student Registration
**Requirements:** Name, Email, Password; Valid Email; Password ≥ 8 Characters; Unique Email; Success Message.

| Scenario | Expected Result |
|---|---|
| Valid Data ဖြင့် Register | User Create ဖြစ်ပြီး Success Message ပြမယ် |
| Empty Name | Validation Error ပြမယ် |
| Invalid Email | Reject လုပ်မယ် |
| Password 7 Characters | Reject လုပ်မယ် |
| Password 8 Characters | တခြား Rules ပြည့်မီရင် Accept လုပ်မယ် |
| Duplicate Email | Reject လုပ်ပြီး Duplicate Record မထည့်ဘူး |

**Important:** Requirement မှာ University Email Domain, Uppercase, Special Character မပါရင် ကိုယ့်ဘာသာ Rule အသစ် မထည့်ရပါ။ Stakeholder ကို Clarify လုပ်ရပါမယ်။

## 6. Testing Across the Stack
- **React UI:** Form Errors နဲ့ Success Message စစ်မယ်။
- **Laravel/Express API:** Status Code, Response Body, Validation, Authorization စစ်မယ်။
- **Database:** Record တကယ်သိမ်းထားသလား၊ Unique Constraint ရှိသလား စစ်မယ်။
- **E2E:** User တစ်ယောက်ရဲ့ Registration Workflow တစ်ခုလုံး စစ်မယ်။

### Important Learning Point
API က `201 Created` ပြန်တာနဲ့ Registration Feature အောင်မြင်ပြီလို့ မဆိုနိုင်ပါ။ Database ထဲ Record မရှိရင် **Business Operation မပြီးမြောက်တဲ့ Defect** ရှိနေတယ်။ Status Assertion တစ်ခု Pass ဖြစ်နိုင်ပေမဲ့ Feature Test တစ်ခုလုံး Fail ဖြစ်နိုင်တယ်။

## Practice
[Registration Test Scenarios](exercises/registration-test-scenarios.md) ကို ကြည့်ပါ။
