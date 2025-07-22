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

# 1. Purpose and Business Benefits

## 1.1 The goal of suggested orders is

1. Boost sales and MSL coverage
2. Optimize product assortment suggestions for weekly orders
3. Estimate order volumes at the outlet level
4. Improve clarity and understanding of:
  - Outlet-specific gaps
  - MSL for each outlet




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

# 2. Calculation Methodology

*The following sales groups are excluded from our suggestions:*

- Canada Dry  
- Wholesale  
- Sellout  

*The dashboard and analysis focus mainly on:*

- DSD (Direct Store Delivery)  
- LKA (Key Accounts)  

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

---

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

