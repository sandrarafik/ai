# **Table of content**

1. Purpose and Business Benefits
2. Calculation Methodology
    1. Order Size Calculation
    2. Percentage to Keep
    3. Methodologies
        1. FS Depletion Logic
        2. Picos (MSL) Logic
    4. Historical Compliance
    5. BAN to SKU Logic
3. Metrics and Solutions
    1. Compliance
    2. Out of Stock
    3. Product Range
    4. HGMM
4. OOS Analysis
5. Others
    1. Communications
    2. Links
    3. Acronyms

---

# 1. Purpose and Business Benefits

## 1.1 The goal of suggested orders is

1. Boost sales and MSL coverage
2. Optimize product assortment suggestions for weekly orders
3. Estimate order volumes at the outlet level
4. Improve clarity and understanding of:
  - Outlet-specific gaps
  - MSL for each outlet

---

## 1.2 Four main components of suggested orders:

**1.2.1 MSL:**

- Designed to increase MSL coverage
- the benefit is to increase MSL distribution and availability, ensuring alignment with the company’s goals and targets
- Initially, all MSL suggestions were pushed without a set percentage to keep but this overwhelmed the business developers
- The focus is now on determining the optimal number of MSL suggestions per customer based on compliance
- To improve efficiency and focus

**1.2.2 Historicity**:

- Recommend product assortments based on customers' historical data
- Maintain regular stock levels of commonly purchased SKUs
- **The benefit** is to increase customer satisfaction
  - Tailored recommendations make customers feel valued
  - This boosts loyalty
- Increases outlet value by:
  - Suggesting product assortments aligned with customer preferences and purchase history
  - Leading to higher chances of repeat purchases
  - Improving sales at the outlet level
- **Frequently Sold suggestions rely on a percentage to keep**, based on order size seasonality
- Typically, this percentage is **100% during the first two weeks of the Hellenic month**
  - Business developers tend to bulk order during this time
- As the month progresses:
  - The percentage decreases
  - Focus shifts more to collection visits and less on orders



**1.2.3 Promos:**

- Where suggested orders can be used to drive promotional suggestions
- The benefit here is that promos are effectively communicated at the outlet level
- Ensuring they reach the right customers
- generate increased sales


**1.2.4 New Launches:**

- Which increases the distribution of new products
- And ensures execution excellence
- Driving successful product introductions at the outlet level

---

# 2. Calculation Methodology

*The following sales groups are excluded from our suggestions:*

- Canada Dry  
- Wholesale  
- Sellout  

*The dashboard and analysis focus mainly on:*

- DSD (Direct Store Delivery)  
- LKA (Key Accounts)  

---

## 2.1. Order Size

### 2.1.1 Calculation

- **Step 1:** Select BANs per customer  
  - The process starts by selecting which Base Article Numbers (BANs) to suggest for each customer  

- **Step 2:** Determine order size  
  - Order size is calculated as the average number of SKUs ordered per week over the last 8 weeks  

- **Why 8 weeks?**  
  - 8 weeks is used to account for seasonality  
  - A 13-week average may overlap different seasons and skew the result  

- **Country comparison**  
  - In some other countries, a manual limit is used  
  - The order size is the minimum between the average and the manual limit  

- **In our case:**  
  - No manual limit is set  
  - Therefore, order size = average number of SKUs ordered in the past 8 weeks  

### 2.1.2 Order Size Logic Example – Customer X

- *Customer X – Weekly SKU Data:*
  
|   Week |   Number of SKUs Ordered |
|--------|--------------------------|
| 202430 |                       15 |
| 202431 |                        2 |
| 202432 |                        3 |
| 202433 |                        4 |
| 202434 |                        7 |
| 202435 |                        2 |
| 202436 |                        3 |
| 202437 |                       10 |

**8-week Average Order Size:** 5.75

• Customer X has an average of 5.75 SKUs ordered per week.  
• This value is rounded to the nearest whole number.  
• Therefore, the order size is rounded to 6.  
• This means that 6 BANs (~6 SKU suggestions) will be suggested for that customer.  

### 2.1.3 Overall Suggestion Limit Rule
• If the overall limit for Customer X is 6 suggestions:  
  - The total number of suggestions will not exceed 6 regardless of the breakdown between MSL and FS.  

*Example:*  
• MSL count = 10  
• FS count = 4  
• Limit = 6  
  - Only the first 6 MSL suggestions will be pushed.  
  - The remaining FS suggestions will not be included.  

---

## 2.2. Percentage to Keep:

### 2.2.1 MSL:
• Currently, we push all MSL suggestions without a defined percentage to retain, using 1000 SKUs as a fixed limit.  
• This number was chosen arbitrarily to include all MSL suggestions. However, the focus is now shifting toward determining the optimal number of MSL suggestions per customer, based on compliance.  

### 2.2.2 Frequently Sold:

*4 Weeks vs. 5 Weeks*  
- The percentage for Frequently Sold (FS) suggestions depends on order size seasonality.  
- During the first two weeks of the Hellenic month, this percentage is normally kept at 100%.  
- As the month continues, the percentage goes down, and the focus shifts more to collection visits instead of pushing more orders.  

    ### Chart 1: 4-Week Month Order Distribution

| Week | Percentage of Orders |
|------|----------------------|
| W1   | 36%                 |
| W2   | 26%                 |
| W3   | 21%                 |
| W4   | 18%                 |



### Chart 2: 5-Week Month Order Distribution

| Week | Percentage of Orders |
|------|----------------------|
| W1   | 31%                 |
| W2   | 22%                 |
| W3   | 18%                 |
| W4   | 12%                 |
| W5   | 17%                 |

- The chart is calculated by determining the percentage of orders across weeks relative to the total, showing the distribution of how orders are spread.  
- "4 weeks" refers to months in 2024 with 4 weeks, and "5 weeks" refers to months with 5 weeks.  

- For a normal distribution over 4 weeks, each week would represent 25% (100% ÷ 4).  
  - If the first week accounts for 36%, then 36% ÷ 25% = 144%. This is why we push 100% for that week.  

- Similarly, for a normal distribution over 5 weeks, each week would represent 20% (100% ÷ 5).  
  - If the fifth week accounts for 17%, then 17% ÷ 20% = 85%. This is why we push 85% for that week.  

- Continuing with our example of Customer X, where the order size is 6:  
  - If the percentage to keep is now 60%, the order size for Customer X would be 4 (60% of 6).This means we push the first 4 BANs, not 6, for FS flag.

---

## 2.3. Methodologies

### 2.3.1. FS Depletion Logic

- The main goal is to calculate, for each customer and each BAN, the **average sales in PHC (Physical Cases)** and the **average number of weeks they ordered** over the past 8 weeks of data.
- **Example:**  
  If Customer X has an average of 2 weeks and 5 PHC, and they purchase 6 PHC, we expect the 6 PHC to last longer than 2 weeks. Therefore, we wait more than 2 weeks before suggesting the same BAN again.

#### Step-by-Step Breakdown:

- For each customer and each BAN:
  - Calculate:
    - **Average sales** over the past 8 weeks (excluding the most recent week)
    - **Average number of weeks** the BAN was ordered (excluding the most recent week)

- This helps predict how long the customer will continue using the product and when to suggest the BAN again.

#### Estimating Duration:

- Use the formula:

 
```
Estimated Duration = (Latest Sales / μ (Average Sales)) × μ (Average Number of Weeks)
```


  Where:
  - **Latest Sales** = Sales from the most recent week (last score week)
  - **μ(Average Sales)** = Average sales over the past 8 weeks (excluding the last week)
  - **μ(Average Number of Weeks)** = Average number of weeks over the past 8 weeks (excluding the last week)

- Calculate the **expected score week** by adding the estimated duration to the current score week.
- Subtract the expected score week from the current score week to get the **frequency score**.

#### Priority Logic:

- The **lower the frequency score**, the **higher the priority**.
  - Example:
    - Current score week = 202443
    - BAN X expected score week = 202440 → Frequency score = -3
    - BAN Y expected score week = 202435 → Frequency score = -8 → Higher priority

- **Exception:**  
  If a BAN has only 1 week of sales, it is deprioritized even if it has the lowest frequency score.

- This logic determines which BANS are suggested under the **Frequently Sold (FS)** flag.
  - If Customer X has an order size of 4, the top 4 BANS with the highest priority (lowest frequency score) are recommended.

> **Note:** The process considers the `"In range" = 'MSL & Y'` column in the product range table to ensure alignment with the customer's product range.

---

### 2.3.2. MSL Logic

- Identify the **MSL SKUs** assigned to each customer based on their **OBPPC** (Occasion, Brand, Package, Price, Channel).
- For each customer:
  - Check if the SKU was **available in the cooler** during the previous week (using red details).
    - If **available** → No suggestion
    - If **not available**:
      - Check if the **business developer placed an order** for the SKU in the same week.
        - If **ordered** → No suggestion
        - If **not ordered** → Suggest the SKU under the **MSL reason flag**

> **Note:** The process considers:
> - `"In range" = 'MSL'`
> - `"SO Flag" = 'Yes'`  
> to ensure that suggested SKUs align with the customer's product range and MSL priorities.

---

## 2.4. Historical Compliance

- To prevent repeating suggestions, we introduced the **historical compliance** parameter:
  - Set to **5 weeks**
  - With a **30% compliance threshold** (subject to change)

- If a BAN has been recommended over the last 5 weeks and complied with **less than 30%** of the time, it will be **excluded** from future suggestions.

### 2.4.1. Example Table:

| Customer | BAN | Compliance | Compliance Threshold |
|----------|-----|------------|----------------------|
| x        | 100 | 0.2        | 0.3                  |
| x        | 110 | null       | 0.3                  |
| x        | 900 | 0.5        | 0.3                  |
| x        | 800 | 0.7        | 0.3                  |

- Continuing with **Customer X**, where the order size is now **4** after applying the **60% retention rate**:
  - We identify the top 4 BANs.
  - If the first BAN doesn't meet the historical compliance requirement (e.g., 20% < 30%), we **remove it** and **replace it** with the 5th BAN to maintain 4 suggestions.

> **Note:** Historical compliance is **only applied to the FS flag**, not the MSL flag, as all MSL suggestions are currently pushed regardless of compliance.

---

## 2.5. BAN to SKU Logic

- All the steps above identify the **optimal BAN** for suggestion.
- Since final recommendations are made at the **SKU level**, and there must be a **1:1 ratio between BAN and SKU**, we now select the **optimal SKU** within each chosen BAN.

### 2.5.1. Process Overview:

- **Filter** data to include only the **last 9 weeks**
- Build **three intermediate tables**:

 #### 1. Historical Sales per Customer
 - Aggregate sales volume for each customer (ignoring reason codes)
 - Columns: `Customer`, `BAN`, `Material (per customer)`, `Volume (per customer)`

  #### 2. Country-Level Aggregation by BAN & SKU
 - Aggregate sales by BAN and SKU across the country
 - Join back to the first table using the BAN
 - Remove hidden materials and duplicates
 - Columns: `Customer`, `BAN`, `Material (per customer)`, `Volume (per customer)`, `Material (per country)`, `Volume (per country)`

  #### 3. Safe Check Table
  - For BANs with no sales at customer or country level in the last 9 weeks
  - Join all possible materials for each Customer + BAN
  - Add a **Material Numerical Order** column (ranking materials under a BAN)
  - Columns: All from above + `Material Numerical Order`

### 2.5.2. Final Selection Logic:

- Sort the combined table using three criteria:
  1. **Volume (per customer)** – descending
  2. **Volume (per country)** – descending
  3. **Material ID** – ascending (lowest ID wins in case of ties)

> **Example:**  
If materials under a BAN are numbered 1, 2, 3, and 4 and the first two criteria don’t break the tie, **Material #1** will be selected.

> **Note:** This **BAN to SKU logic** is applied to both the **FS** and **MSL** flags.

---

## 3.  Metrics and Solutions

### 3.1  Compliance

We start with the total number of suggestions, then remove two categories:

#### 3.1.1 Customers Without Orders
- If a customer places no orders at all (regardless of suggested SKUs or not), it indicates a collection visit, so these are excluded.

#### 3.1.2 Out-of-Stock Suggestions
- If a Business Developer does not comply with a suggestion because the SKU was out of stock on the day of the visit, we exclude that SKU from the total.
- There is a solution for out-of-stock scenarios, which will be discussed later.

#### 3.1.3 After these exclusions:
- The remaining count is the total executable, representing the suggestions that are expected to be carried out successfully.

#### 3.1.4 Next, we determine the total executed from the total executable (SKU Compliance) by verifying:
- Whether each suggested SKU was followed,
- Regardless of the suggested volume.

#### 3.1.5 Focus Areas:
- **2025:** MSL SKU Compliance
- **2026:** Total executed volume vs total suggested volume

---

### 3.2 Types of SKU Compliance

#### 3.2.1 Soft Compliance
- Tracks whether a Business Developer has placed an order, even if it has not yet been delivered.
- Allows for mid-week monitoring.

#### 3.2.2 Hard Compliance
- Counts orders only once they are invoiced (i.e., delivered).
- Since orders can take up to four days to arrive, Hard Compliance data may not reflect accurate performance until after the week ends.

- Soft Compliance provides a more immediate view of compliance trends.

#### 3.2.3 Job:
- DAILY | STAGING | Suggested Orders Compliance

#### 3.2.4 Output:
- DIA_SE.DM. Suggested_Order_Compliance (table)

---

### 3.3 Out of Stock

#### 3.3.1 Context:
- Other countries do not face the same out-of-stock challenges as Egypt.
- A workaround was put in place to:
  - Ensure suggestions remain consistently in stock,
  - Account for volatility and the phase-in/phase-out of SKUs.

#### 3.3.2 Solution:
- A daily job (1:00 AM) replaces the suggested material with an alternative SKU from the same BAN, selected based on highest available stock.

#### 3.3.3 Job:
- DAILY | SB_UPDATE | SO_OOS_NEW

#### 3.3.4 Output:
- DIA_SE.DM.SO_RPLC (table)

#### 3.3.5 Note:
- The job’s output:
  - Identifies the suggested materials,
  - Highlights which ones require replacement,
  - Automatically carries out the replacement.

---

### 3.4 Product Range

#### 3.4.1 The Product Range table is the primary reference for:
- Determining whether a SKU is within a customer’s product range.

#### 3.4.2 Based on the:
- "In Range" column
- "SO Flag" column

#### 3.4.3 Importance:
- Both FS (Frequently Sold) and MSL (Must Stock List) suggestions depend on these columns.
- Ensures alignment with each customer’s range.
- Serves as the base for MSL.
- Updates MSL product ranges per customer under the new OBPPC approach.

#### 3.4.4 Job:
- DAILY | STAGING | PRODUCT RANGE

#### 3.4.5 Output:
- DIA_SE.DM.PRODUCT_RANGE (table)

#### 3.4.6 Note:
- DIA_SE.LEGACY.PRODUCT_RANGE_SB is a view built on that table, that Lingaro reads.

---

### 3.5 HGMM

#### 3.5.1 We reflect our soft compliance in the HGMM report for daily tracking.

#### 3.5.2 View:
- DIA_SE.DBO. SO_Compliance_HGMM  
(View from [DIA_SE].[DM].[Suggested_Order_Compliance])

#### 3.5.3 New query editor window →

```sql
CREATE VIEW [dbo].[SO_Compliance_HGMM] AS
SELECT
    r.week,
    so.[route_code],
    SUM([Soft_Executable]) AS Suggested,
    SUM([Soft_SKU_Compliance]) AS Executed
FROM [DIA_SE].[DM].[Suggested_Order_Compliance] so
LEFT JOIN [DIA_SE].dbo.RankedWeeks r ON r.weekrank = so.weekrank
LEFT JOIN [DIA_SE].[DM].[dim_customer] d ON d.customer = so.customer
WHERE 
    so.reason_code = '(MSL) منتج أساسي'
    AND so.route_code IS NOT NULL
    AND d.sgrp_name IN ('DSD', 'LKA')
GROUP BY
    r.week,
    so.[route_code]
HAVING SUM([Soft_Executable]) > 0
GO
```

---

# 4. oos analysis 

---

# 5. others 

## 5.1. Communications

### 5.1.1. Weekly
- **When:** Every Wednesday (before Friday run)
- **Action:** Send a service request for FS order seasonality  
- **Note:** This is a temporary process until a more sustainable solution is implemented—potentially shifting to a fixed schedule every six months.

### 5.1.2. Monthly
- **Action Items:**
  - Retrieve the **top MSLs** from both **Hossam** and **Andrew**
  - Obtain the **monthly targets** from **Andrew**
- **Timing:** Ensure this communication is sent during the **last week of every Hellenic month**

---

## 5.2 Links

### 5.2.1 SO Golden Output
 **https://adb-4410390070752234.14.azuredatabricks.net/login.html?o=4410390070752234&next_url=%2Feditor%2Fnotebooks%2F3867988878003519%3Fo%3D4410390070752234&tuuid=8dea90d9-d7f3-4ef6-99d1-84fdc31c9560#command/3867988878003522** 

  - Downloading the output from the link is unnecessary because suggested orders are automatically uploaded to Salesbuzz.
  - However, it's good to have it on hand in case any manual downloads are needed.
  - Python script used to process output if downloaded manually.

### 5.2.2 Parameter Drop zone
**https://cchellenic.sharepoint.com/sites/spaces-BSS-DropZone/Manual%20Submissions/Forms/AllItems.aspx?ct=1698048586764&or=Teams%2DHL&ga=1&LOF=1&id=%2Fsites%2Fspaces%2DBSS%2DDropZone%2FManual%20Submissions%2Feg%2Fsegmex%2Fsegmex%5Fuser%5Finput&viewid=05483a9d%2D25a9%2D4dd3%2D9064%2Df5d79f096020&OR=Teams%2DHL&CT=1732803809239&clickparams=eyJBcHBOYW1lIjoiVGVhbXMtRGVza3RvcCIsIkFwcFZlcnNpb24iOiI0OS8yNDEwMjAwMTMxOCIsIkhhc0ZlZGVyYXRlZFVzZXIiOmZhbHNlfQ%3D%3D**

  - This is where we handle all manual swaps, identify strategic goods, and hide any SKUs.
  - In essence, it's where all manual inputs are applied.

### 5.2.3 Suggested Order Code
**https://spsprodweu5.vssps.visualstudio.com/_signin?realm=dev.azure.com&reply_to=https%3A%2F%2Fdev.azure.com%2FCCHBC%2FCCH%2520SAFe%2520Portfolio%2F_git%2Fdaar-aa-segmex-egypt-assortment%3Fpath%3D%252F%26version%3DGBmaster%26_a%3Dcontents&redirect=1&hid=be28867e-017c-46ad-842e-b453882cff14&context=eyJodCI6MiwiaGlkIjoiMjUwZDViZTItZWE3MS00MWIwLTk0OWYtMzJjMGQ2YjQ3ZjNmIiwicXMiOnt9LCJyciI6IiIsInZoIjoiIiwiY3YiOiIiLCJjcyI6IiJ90#ctx=eyJTaWduSW5Db29raWVEb21haW5zIjpbImh0dHBzOi8vbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbSIsImh0dHBzOi8vbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbSJdfQ2**

  - This is where Lingaro's suggested orders code is written.

### 5.2.4 Snow Service Request
**https://login.microsoftonline.com/7a67a070-8ce9-4692-b1af-bf788306bc66/oauth2/authorize?client_id=499b84ac-1321-427f-aa17-267ca6975798&site_id=501454&response_mode=form_post&response_type=code+id_token&redirect_uri=https%3A%2F%2Fspsprodweu5.vssps.visualstudio.com%2F_signedin&nonce=5805b0e9-d68f-435e-9496-96539fd9684b&state=realm%3Ddev.azure.com%26reply_to%3Dhttps%253A%252F%252Fdev.azure.com%252FCCHBC%252FCCH%252520SAFe%252520Portfolio%252F_wiki%252Fwikis%252FCCH-SAFe-Portfolio.wiki%252F14148%252FSNOW-Service-Requests-%2528SR%2529%26ht%3D2%26hid%3Dbe28867e-017c-46ad-842e-b453882cff14%26nonce%3D5805b0e9-d68f-435e-9496-96539fd9684b%26protocol%3Dwsfederation&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&cid=5805b0e9-d68f-435e-9496-96539fd9684b&wsucxt=1&instance_aware=true**

  - Guide on how to open service requests.

### 5.2.5 Drop Zone for Targets from DP
 **https://cchellenic.sharepoint.com/sites/EgyptDIA-SegmentedExecution/Shared%20Documents/Forms/AllItems.aspx?ovuser=7a67a070%2D8ce9%2D4692%2Db1af%2Dbf788306bc66%2Cnouran%2Eabdelrahman%40cchellenic%2Ecom&OR=Teams%2DHL&CT=1738660121997&clickparams=eyJBcHBOYW1lIjoiVGVhbXMtRGVza3RvcCIsIkFwcFZlcnNpb24iOiI0OS8yNDEyMDEwMDIyMSIsIkhhc0ZlZGVyYXRlZFVzZXIiOmZhbHNlfQ%3D%3D&FolderCTID=0x0120002585918CE8167B40ACDC13C606C260D9&id=%2Fsites%2FEgyptDIA%2DSegmentedExecution%2FShared%20Documents%2FSegmented%20Execution%2F01%2E%20Use%20Cases%2FSuggested%20Orders%2FTargets%20%2D%20OOS&viewid=d3d71653%2D4dae%2D467a%2D94a7%2Db863295458f4**

  - This is where to store targets received from demand planning, for dashboard to refresh successfully.

### 5.2.6 Dashboard
 **https://app.powerbi.com/groups/d2d70cee-5c6b-4176-9ed0-f7b62e65d990/reports/f6fd8a77-8c71-40b4-904c-d9a14ae25199/ReportSection66cd415ce4e07235f8cc?experience=power-bi**

### 5.2.7 Dashboard 2
 **https://app.powerbi.com/groups/d2d70cee-5c6b-4176-9ed0-f7b62e65d990/reports/38a210cd-6837-49e0-97b2-11c74f75e6bf/ReportSection66cd415ce4e07235f8cc?experience=power-bi**
  - Same as other dashboard, however there are 2 more parameters where the OOS is added to the total executable.

### 5.2.8 Order Size Seasonality (FS % to Keep)
 **https://app.powerbi.com/groups/d2d70cee-5c6b-4176-9ed0-f7b62e65d990/reports/795c3c33-9d8c-4c6b-b435-9ccbf33c3f5e/ReportSection?experience=power-bi**

---

## 5.3. Glossary of Acronyms

- **BAN**: Base Article Number  
- **CRM**: Customer Relationship Management  
- **DSD**: Direct Store Delivery  
- **FS**: Frequently Sold  
- **HGMM**: Hellenic Good Morning Meeting  
- **LKA**: Local Key Accounts  
- **MSL**: Must Stock List  
- **OBPPC**: Occasion, Brand, Package, Price, Channel  
- **OOS**: Out of Stock  
- **PHC**: Physical Cases  
- **SKU**: Stock Keeping Unit  
- **SO**: Suggested Orders  
