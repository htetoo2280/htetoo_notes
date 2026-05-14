---
id: tck0dhs5sx4l0gvx8o1d04c
title: liquidity
desc: ''
updated: 1778211023886
created: 1778149547818
---

# Liquidity
Liquidity (လျင်မြန်စွာငွေပြန်ရနိုင်မှု) ကိုတွက်တဲ့အခါ “ချက်ချင်းအသုံးပြုလို့ရတဲ့ငွေ” ကိုသာ focus လုပ်တာပါ။

Liquidity ဆိုတာ
➡️ Bank က short-term obligation (အလျင်အမြန်ပေးရမယ့်ငွေ) ကို
➡️ loss မဖြစ်ဘဲ ချက်ချင်းပြန်ပေးနိုင်ခြင်း ဖြစ်ပါတယ်


🔹 Banking logic (ရိုးရှင်း version)

Liquidity Ratio =
👉 (Liquid Assets) / (Short-term Liabilities)

---------------- 

🔹 Core Concept (အဓိက idea)

Liquidity calculation မှာ
✔ Cash
✔ Current account balance
✔ Short-term (< 30 days) assets

👉 ဒီလို highly liquid assets ကိုသာ include လုပ်တယ်

❌ Long-term / locked / market-dependent assets တွေ
👉 exclude (နုတ်) လုပ်တယ်

-----------------

# Core Idea (အရေးကြီးဆုံး)

Liquidity တွက်တဲ့ rule ကို ဒီလိုမှတ်ပါ👇

👉 ✔ Include = Cash + ချက်ချင်းပြန်ရနိုင်တာ

👉 ❌ Exclude =

- Locked
- Long-term
- rket risk ရှိ
- Paper only (not cash)


# ဘာတွေနုတ်လို့ရလဲ


1. Loans (ချေးငွေ)
Customer ကိုပေးထားတဲ့ loan တွေ
Repayment schedule ရှိ → ချက်ချင်းပြန်မရ

👉 Liquidity မှာ
❌ မထည့် (exclude)

---------

🔹 2. Fixed Assets

ဥပမာ—

Building
Furniture
IT equipment

👉 ဒီအရာတွေက

Cash ပြောင်းဖို့အချိန်ယူရတယ်
Market value မသေချာ

👉 ဒါကြောင့်
❌ Liquidity မှာ နုတ်

-----------

🔹 3. Investment (Long-term)

ဥပမာ—

Bonds (long maturity)
Equity investment

👉 Reason:

Sell လုပ်ရင် market risk ရှိ
Discount နဲ့ပဲရနိုင်တယ်

👉 ❌ Fully liquid မဟုတ်

---------

🔹 4. Non-performing Loans (NPL)
ပြန်မဆပ်တဲ့ loan

👉 ဒီဟာက

Cash inflow မရှိသလို
Risk မြင့်

👉 ❌ Liquidity မှာ မထည့်ဘူး

--------------

🔹 5. Accrued Income / Receivables

ဥပမာ—

Interest receivable
Other receivable

👉 Paper profit ပဲရှိတယ်
👉 Cash မရသေး

👉 ❌ Exclude

--------------

🔹 6. Restricted Balance

ဥပမာ—

Central Bank reserve requirement (တချို့ case)
Collateral အဖြစ် lock ထားတဲ့ fund

👉 Bank က freely သုံးလို့မရ

👉 ❌ Liquidity မထည့်

-------------


🔹 7. Interbank placement (long tenor) 
Other banks ကိုထားတဲ့ placement (long term) or money market (fx transaction)

👉 Maturity မရောက်သေးရင်
👉 Cash မဖြစ်နိုင်

👉 ❌ Exclude (short-term မဟုတ်ရင်)

--------------

🔹 8. Off-balance sheet commitments

ဥပမာ— 
Guarantees
Undrawn loan commitments

👉 Future liability ဖြစ်နိုင်

👉 Liquidity risk အဖြစ်ယူပြီး
👉 sometimes adjustment လုပ်တယ်

------------




[fn_liquidity_excel_link_for learning](<c:/Users/htetoo.lwin/Desktop/Liquidity fn working file.xlsx>)



