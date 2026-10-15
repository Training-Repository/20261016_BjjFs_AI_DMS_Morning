# Copilot Chat for Excel — Participant Exercise Guide
### Formulas & Pivot Tables for DMS (Consumer)
**Bajaj Finance Limited | M365 Copilot Training**
**File:** `BFL_DMS_Copilot_Demo.xlsx`
**Mode:** Copilot Chat (no Microsoft 365 Copilot licence required)

---

## Before You Begin

### What You Need
- **Excel** open with `BFL_DMS_Copilot_Demo.xlsx`
- **Copilot Chat** open in a second window — any of:
  - `https://m365.cloud.microsoft/chat` (M365 Copilot Chat, work account)
  - The **Copilot** button in Microsoft Edge
  - The Copilot app in Windows or Teams
- Both windows side by side (**Win + ←** and **Win + →**). You will switch between them constantly.

### How This Session Works
Copilot Chat is **not connected to your workbook.** It cannot insert formulas, build pivot tables or change anything in Excel. It can *write* all of it for you, and you paste it in.

Every exercise follows the same **two-step rhythm**:

| Step | Where | What You Do |
|------|-------|-------------|
| **1. Ask** | Copilot Chat | Paste the prompt; get the formula or the steps |
| **2. Apply** | Excel | Paste into the cell, press Enter, fill down |

> **Key habit:** because Chat cannot see your file, **you** must describe it. That is the core skill of this session, and it is the same skill that makes every other AI tool work well.

**The sheet:** headers are in **row 2**, and data runs from **row 3 to row 27** (25 accounts, as of 30 Sep 2026). Columns **N–Q are empty**, and you will fill them using Copilot Chat. *(Column M is a deliberate blank spacer. It matters in Exercise 7.)*

---

## Step 0 — Set the Context (do this once)

Open Copilot Chat and paste this **first**. Everything after it can be short, because Chat now knows your sheet.

```
I'm working in Excel on a DMS (debt management) collections tracker. You
can't see the file, so here is the layout:

Headers are in row 2. Data runs from row 3 to row 27 (25 account rows).
The data is as of 30 September 2026.

A  Account ID          (text, e.g. BFL-PL-70112)
B  Customer Name       (text)
C  Product             (Consumer Durable, Digital Product, Lifestyle Finance,
                        Personal Loan, Two-Wheeler)
D  DPD                 (number — days past due)
E  Overdue Amount (₹)  (number)
F  EMI Amount (₹)      (number)
G  Call Outcome        (PTP Confirmed, Partial PTP, Escalated, Dispute,
                        No Response, Promise Broken, Callback Requested)
H  PTP Date            (date; blank if there is no promise-to-pay)
I  PTP Amount (₹)      (number; blank if no PTP)
J  Collector Name      (text)
K  Zone                (Pune, Mumbai, Nashik, Nagpur)
L  Field Visit         (Yes / No)
M  (blank spacer — ignore it)
N  DPD Bucket          (empty — I'll add this)
O  Risk Score          (empty — I'll add this)
P  Days Since PTP Due  (empty — I'll add this)
Q  EMIs Overdue        (empty — I'll add this)

For the rest of this conversation: when I ask for a formula, give me the
formula for the FIRST data row (row 3), ready to paste and fill down.
Give the formula on its own line, then a one-line explanation. No long
preamble.
```

> 💡 **Keep this block handy.** It is the difference between sharp answers and vague ones. Save it, and adapt it for any tracker you use at work.

---

## Exercise 1 — DPD Bucket (Column N)

### Step 1 — Ask (Copilot Chat)

```
Write a formula for cell N3 that classifies each account by DPD (column D):
- "Critical" if DPD is more than 90
- "High" if DPD is 61 to 90
- "Medium" if DPD is 31 to 60
- "Low" if DPD is 30 or less
```

**Expected output:**
```excel
=IF(D3>90,"Critical",IF(D3>60,"High",IF(D3>30,"Medium","Low")))
```

### Step 2 — Apply (Excel)
1. Click **N3**, paste the formula and press Enter.
2. Select **N3** and double-click the small square at its bottom-right corner to fill down to **N27**. *(Or select N3:N27 and press **Ctrl + D**.)*

✅ **Check:** 4 Critical, 9 High, 10 Medium, 2 Low.

> **Try this:** *"What does this formula return for a DPD of exactly 90, and exactly 60?"* Chat will confirm that 90 lands in **High** (the first test is `>90`, not `>=90`) and 60 lands in **Medium**. This is the classic off-by-one trap in banded IFs.

> **Bonus:** *"Rewrite this using IFS instead of nested IFs."* Which version would you rather hand to a colleague?

---

## Exercise 2 — Risk Score (Column O)

### Step 1 — Ask

```
Write a formula for cell O3 that multiplies DPD (column D) by the Overdue
Amount (column E) to create a Risk Score.
```

**Expected output:**
```excel
=D3*E3
```

### Step 2 — Apply
Paste into **O3**, press Enter, and fill down to **O27**.

✅ **Check:** the highest score is Vikram Deshpande, **46,54,280**.

> **Try this:** *"These numbers are too large to read. Scale them to thousands."* Chat will divide by 1,000. This is the same scale the Account Priority Matrix uses.

---

## Exercise 3 — Days Since PTP Due (Column P)

### Step 1 — Ask

```
Write a formula for cell P3 that shows how many days have passed since the
PTP Date in column H, as of 30 September 2026. If H3 is blank, return blank.
```

**Expected output:**
```excel
=IF(H3="","",DATE(2026,9,30)-H3)
```

### Step 2 — Apply
Paste into **P3**, press Enter, and fill down to **P27**. If you see a date such as `05-01-1900` instead of a number, set the column format to **Number** (Home → Number Format → General).

✅ **Check:** Pooja Tiwari 6, Mohammed Shaikh 5, Anjali Verma 4, Ganesh Pawar 3, Rashmi Singh 2 and Rohan Mishra 0. Negative numbers mean the PTP date is still ahead.

> **On live data:** ask Chat to *"use TODAY() instead of a fixed date"* so the column updates daily.

---

## Exercise 4 — EMIs Overdue (Column Q)

### Step 1 — Ask

```
Write a formula for cell Q3 that estimates how many EMIs are overdue by
dividing the Overdue Amount (column E) by the EMI Amount (column F),
rounded to the nearest whole number.
```

**Expected output:**
```excel
=ROUND(E3/F3,0)
```

### Step 2 — Apply
Paste into **Q3**, press Enter, and fill down to **Q27**.

> **On your own data:** every account in this file has an EMI amount, so the formula never errors. On a live tracker, a blank or zero EMI gives **#DIV/0!**. Ask Chat: *"Make this safe when the EMI Amount in column F is blank or zero."* You will get something like `=IF(F3=0,"",ROUND(E3/F3,0))` or an `IFERROR` wrapper.

---

## Exercise 5 — Ask Copilot Chat to Explain a Formula

Copy the formula from **N3** and paste it into Copilot Chat with:

```
Explain this formula in simple terms. What does each part do, and in what
order does it evaluate?

=IF(D3>90,"Critical",IF(D3>60,"High",IF(D3>30,"Medium","Low")))
```

**What Copilot Chat will explain:**
> *"It reads the DPD in D3 from the top down. Over 90 returns Critical. If not, over 60 returns High. If not, over 30 returns Medium. Otherwise it returns Low. Each IF runs only when the one before it was false, so the order matters."*

> **This works on any formula.** Paste the most complex formula from your own MIS and ask the same question. This is one of the most valuable habits from the session.

---

## Exercise 6 — Pivot Table: Overdue by Product and Call Outcome

Copilot Chat **cannot build the pivot for you.** It gives you the click-path, and you build it.

### Step 1 — Ask

```
Give me step-by-step instructions to build a PivotTable in Excel from the
range A2:L27, showing the total Overdue Amount for each Product, broken down
by Call Outcome. Tell me exactly which field goes into which area.
```

### Step 2 — Apply
1. Click any cell inside the data (columns A–L).
2. **Insert → PivotTable → From Table/Range**. Confirm the range is **A2:L27**, choose **New Worksheet** and click OK.
3. Drag the fields:
   - **Rows:** Product
   - **Columns:** Call Outcome
   - **Values:** Overdue Amount (₹)
4. If the value shows as **Count**, click it, choose **Value Field Settings** and select **Sum**.

✅ **Check:** Personal Loan has the highest total, **₹1,90,540**. Consumer Durable has the lowest, **₹28,700**.

### No-Pivot Alternative

```
Instead of a PivotTable, give me a SUMIFS formula that totals Overdue Amount
for a given Product and Call Outcome, so I can build a summary grid with
Products down the side and Call Outcomes across the top.
```

You will get something like `=SUMIFS($E$3:$E$27,$C$3:$C$27,$S3,$G$3:$G$27,T$2)`.

---

## Exercise 7 — Pivot Table: Collector Workload by DPD Bucket

This pivot uses the **DPD Bucket** column from Exercise 1 (column N). That column sits *after* the blank spacer column M, which changes how you select the range.

### Step 1 — Ask

```
Give me the steps for a second PivotTable showing the count of accounts for
each Collector Name, broken down by DPD Bucket. Collector Name is column J
and DPD Bucket is column N. Column M between them is a blank spacer with no
header. Tell me which field goes in which area, and how to handle that blank
column.
```

### Step 2 — Apply
1. Select **A2:Q27**. This range includes the blank spacer column M.
2. **Insert → PivotTable → From Table/Range → New Worksheet** → OK.
3. **If Excel says *"The PivotTable field name is not valid"***, the cause is the blank header in column M. Type `Spacer` into **M2**, then insert the pivot again.
4. Drag the fields:
   - **Rows:** Collector Name
   - **Columns:** DPD Bucket
   - **Values:** Account ID *(it defaults to Count, which is correct here)*

✅ **Check:** Rajesh Kumar has 6 accounts, 3 of them Critical.

### No-Pivot Alternative

```
Instead of a PivotTable, give me a COUNTIFS formula that counts accounts for
a given Collector Name and DPD Bucket, so I can build the workload grid
manually.
```

`=COUNTIFS($J$3:$J$27,$S3,$N$3:$N$27,T$2)` puts collectors down the side and buckets across the top, and avoids the blank-spacer issue entirely.

---

## ⚠️ Data Handling — Read This

This is a **synthetic training dataset**, so it is safe to describe and safe to paste. Live DMS data is not. When you use these habits on real accounts:

- Use **Copilot Chat signed in with your BFL work account** (look for the enterprise data protection indicator).
- Never paste customer PII (names, phone numbers, account numbers, PAN).
- **De-identify first.** Replace names with Cust-1, Cust-2 and so on, and paste only the columns the question needs.

> Describing the *shape* of your data, as you did in Step 0, is almost always enough. Pasting the *whole* dataset rarely is.

---

## What Changes When You Get a Copilot Licence

The habits from this session carry over. The licence removes the copy-paste, not the thinking.

| | **Copilot Chat** *(today)* | **Copilot in Excel** *(licensed)* |
|---|---|---|
| Sees your workbook | ✗ — you describe it | ✓ — reads it directly |
| Writes formulas | ✓ | ✓ |
| **Inserts** formulas into cells | ✗ — you paste | ✓ automatic |
| Builds PivotTables | ✗ — gives you the steps | ✓ builds them |
| Analyses your data | ✓ — if you paste it in | ✓ — reads the sheet |
| Formats, charts, highlights | ✗ | ✓ |
| Explains any formula | ✓ | ✓ |

---

## Quick Reference — DMS Prompts *(this session)*

| Task | Ask Copilot Chat |
|---|---|
| DPD Bucket (N) | *"Formula for N3: Critical if DPD (col D) > 90, High 61–90, Medium 31–60, Low 30 or less."* |
| Risk Score (O) | *"Formula for O3 = DPD (col D) × Overdue Amount (col E)."* |
| Days Since PTP Due (P) | *"Formula for P3: days from PTP Date (col H) to 30 Sep 2026; blank if H is blank."* |
| EMIs Overdue (Q) | *"Formula for Q3 = Overdue Amount (col E) ÷ EMI Amount (col F), rounded."* |
| Explain a formula | *"Explain this formula in simple terms, part by part."* (then paste the formula) |
| Pivot — overdue by product | *"Steps for a PivotTable from A2:L27: total Overdue Amount by Product × Call Outcome."* |
| Pivot — collector workload | *"Steps for a PivotTable: count by Collector Name × DPD Bucket; column M is a blank spacer."* |
| Highlight broken PTPs | *"Steps to conditionally format rows where column P is greater than 0 in amber."* |

## Quick Reference — Prompt Patterns *(any formula, any sheet)*

| You want | Say this |
|---|---|
| A formula | *"Write a formula for cell **X3** that…, ready to fill down to row 27"* |
| Banded categories | *"…Critical if over 90, High 61–90, Medium 31–60, Low 30 or less, based on column D."* |
| Blank / error handling | *"…if column F is blank or zero, return "" instead of #DIV/0!."* |
| A simpler version | *"Rewrite this using IFS."* / *"Can this be shorter?"* |
| To understand it | *"Explain this formula in simple terms, part by part."* |
| A pivot | *"Step-by-step instructions for a PivotTable that… Tell me which field goes in which area."* |
| A total without a pivot | *"A COUNTIFS (or SUMIFS) formula for … so I can build a summary grid."* |

---

*Bajaj Finance Limited | AI Academy — Debt Management Services (Consumer) | Microsoft Copilot Training Programme*
*Training delivered by **Technizer India** | GenAI for Enterprise Teams*
