# Project QueryMatch: Streamlining Bank Reconciliation and Variance Analysis utilizing Power Query.
Used Excel and Power Query to reconcile accounting records of a small retail company in District 2 with bank statements.
## Dataset
`Detailed Ledger_Jan 2024`- 34 transactions recorded in January for the company.

`Bank Statement_Jan 2024` - 36 bank statement records in Janurary.
## Preview 

On April 30, 2024, the accountant detected 8 reconciliation differences representing 7 distinct discrepancies between the ledger and bank statement, then performed the required adjustments.
<img width="1392" height="163" alt="image" src="https://github.com/user-attachments/assets/f416a923-aa5b-4bf1-98b5-5e63b5110ab3" />

## How to implemet 

**Note: Transactions recorded in the company's books are opposite to those on the bank statement; meaning a Debit (Dr) for the company corresponds to a Credit (Cr) on the bank statement, and vice versa.**

### Step 1: Upload `Detailed Ledger_Jan 2024` and `Bank Statement_Jan 2024` to Power Query 

 **Detailed Ledger_Jan 2024**

 Column tab ➡️Customn Column ➡️ Named `Net cash flow` ➡️ Custom column formula: Enter `= Dr - Cr`

 **Bank Statement_Jan 2024**

 Column tab ➡️Customn Column ➡️ Named `Net cash flow` ➡️ Custom column formula: Enter `= Cr - Dr`

 ### Step 2: Merge and identify discrepancies
 
 Use **Merge Queries as New**:

- Use `Detailed Ledger_Jan 2024` as the primary table for reconciliation.
- Join type: **Full Outer Join**
- Key column: `Date` and `Net cash flow`

After merge, Add column `Discrepancies` = `Bank Statement.Net Cash Flow` - `Net Cash FLow` ➡️ Filter and retain `null` ➡️ Replace all `null` for blank ➡️ **The result as the table at preview part**

### Step 3: Classify discrepancies

Overall, there are 3 types of errors causing discrepancies between the bank reconciliation and the general ledger.
- Timing difference: Transactions recorded in the cash book but not yet reflected in the bank statement.
- Business's errors and ommission: Transactions correctly recorded in the bank statement but not recorded in the cash book.
- Bank errors: The bank incorrectly recorded receipts and payments between different businesses.

<img width="1001" height="187" alt="image" src="https://github.com/user-attachments/assets/3bff21a4-39b7-40ab-946d-f9a360db2914" />

The discrepancies were classified into three primary categories: business errors and omissions (3 instances), timing differences (2 instances), and bank errors (1 instance).

### Step 4: Reconciliation Statement

#### ADJUSTED CASH BOOK BALANCE

| | VND | VND |
|:---|---:|---:|
| **Cash book balance b/d** | | **6,750,000** |
| Add: Bank interest | 45,000 | |
| | | 45,000 |
| Less: Bank charges | 110,000 | |
| &emsp;&emsp;Bank charges | 22,000 | |
| &emsp;&emsp;Bank charges | 11,000 | |
| | | 143,000 |
| **Corrected cash book balance** | | **6,652,000** |

#### BANK RECONCILIATION

|  | VND | VND |
|:---|---:|---:|
| **Balance as per cash book (corrected)** | | **4,802,000** |
| Add: Correction of overstatement | 450,000 | |
| Add: Uncleared lodgements | 5,200,000 | |
| Less: Unpresented cheques | 3,800,000 | |
| **Balance as per bank statement** | | **6,652,000** |

→ **The two adjusted balances agree.** ✅



 
 
