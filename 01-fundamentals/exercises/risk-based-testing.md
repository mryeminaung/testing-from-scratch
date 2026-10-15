# Exercise — Risk-based Testing (Project infoSphere)

**Lesson:** 02  
**Status:** Reviewed

## Issues and Learner's Priorities
| Issue | Description | Priority |
|---|---|---|
| A | Student က Unauthorized Proposal Approval လုပ်နိုင် | High |
| B | Dashboard Card Padding မှား | Low |
| C | Double Click ကြောင့် Duplicate Project Records | Medium |
| D | Report Page Load 12 Seconds | Medium |

## Learner's Reasoning
> I would prioritize issue A, that one is related with authorization. I need to verify and check that approval flow.

## Feedback (မြန်မာ)
**A — High:** သင့်တော်တယ်။ Unauthorized Approval က Security, Data Integrity နဲ့ Business Workflow ကို ထိခိုက်နိုင်တယ်။ Backend Authorization နဲ့ Database State ကို Verify လုပ်ရန်။

**B — Low:** Minor Cosmetic Issue ဆိုရင် သင့်တော်တယ်။ Usability ကို ပြင်းထန်စွာ ထိခိုက်ရင် Priority ပြောင်းနိုင်တယ်။

**C — Medium:** လက်ခံနိုင်တယ်။ Duplicate Records ကြောင့် Reporting/Evaluation မှားရင် High ဖြစ်နိုင်တယ်။ Backend Duplicate Protection လိုတယ်။

**D — Medium:** လက်ခံနိုင်တယ်။ Critical Seminar/Reporting Workflow မှာ အသုံးပြုရင် High ဖြစ်နိုင်တယ်။

## Improved Reasoning (English)
I would prioritize Issue A because unauthorized proposal approval can compromise authorization, data integrity, and academic approval rules. I would verify that only assigned supervisors can approve proposals, that unauthorized API requests are rejected, and that rejected requests do not modify database records.

## Takeaway
**Risk = Likelihood + Impact ကို စဉ်းစားပြီး Testing Priority သတ်မှတ်ရန်။** ဒီမှာ + က သင်္ချာ Formula မဟုတ်ဘဲ အဓိက Dimension နှစ်ခုကို တွဲစဉ်းစားရန် ဆိုလိုတာဖြစ်တယ်။
