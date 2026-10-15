# Exercise — Student Registration Test Scenarios

**Lesson:** 01 — What is Software Testing?  
**Status:** Reviewed

## Requirements
1. Student က Name, Email, Password ဖြည့်ပြီး Register လုပ်နိုင်ရမယ်။
2. Email Format Valid ဖြစ်ရမယ်။
3. Password Minimum 8 Characters ဖြစ်ရမယ်။
4. Email တစ်ခုကို တစ်ကြိမ်ပဲ Register လုပ်နိုင်ရမယ်။
5. Successful Registration မှာ Success Message ပြရမယ်။

## Learner's Initial Ideas and Feedback
1. **Empty Inputs:** Valid Scenario; Field တစ်ခုချင်းစီ Empty/Whitespace Cases ထည့်စဉ်းစားရန်။
2. **University Email Domain:** မူလ Requirement ထဲ မပါသေး; Stakeholder Clarification လိုတယ်။
3. **Uppercase/Lowercase/Special Characters:** မူလ Requirement ထဲ မပါသေး; Minimum 8 Characters ကိုပဲ အရင် Test လုပ်ရန်။
4. **Uniqueness:** Email Uniqueness ကို အတိအကျ သတ်မှတ်ရန်။
5. **200/201 Status Codes:** Status Code တစ်ခုတည်းမဟုတ်ဘဲ Response Body, Database Persistence, Error Behavior ပါ စစ်ရန်။ API Contract ပေါ်မူတည်ပြီး Expected Status သတ်မှတ်ရန်။

## Improved Scenarios
| ID | Scenario | Expected Result |
|---|---|---|
| TS-001 | Valid Registration | User Create + Success Message |
| TS-002 | Empty Required Fields | Validation Error |
| TS-003 | Invalid Email | Reject |
| TS-004 | Password 7 Characters | Reject |
| TS-005 | Password Exactly 8 Characters | Other Rules ပြည့်မီရင် Accept |
| TS-006 | Duplicate Email | Reject; No Duplicate Record |
| TS-007 | Successful Registration Message | Correct Success Message |
| TS-008 | API Response | Contract အတိုင်း Status + Body |
| TS-009 | Failed Registration | Database ထဲ New User မရှိ |
| TS-010 | Successful Registration | Database ထဲ User Record ရှိ |

## Lesson Learned
**Boundary Value Analysis:** 7, 8, 9 Characters ကို Test လုပ်ပါ။

**Mini Challenge:** API က `201 Created` ပြန်ပေမဲ့ Database ထဲ Record မရှိရင် Feature Test **Fail** ဖြစ်တယ်။ Status Code Assertion တစ်ခု Pass ဖြစ်နိုင်ပေမဲ့ Business Operation မပြီးမြောက်ဘူး။
