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

# **Purpose and Business Benefits**

## **The goal of suggested orders is**

1. Boost sales and MSL coverage
2. Optimize product assortment suggestions for weekly orders
3. Estimate order volumes at the outlet level
4. Improve clarity and understanding of:
  - Outlet-specific gaps
  - MSL for each outlet




## **Four main components of suggested orders:**

1. **MSL:**

- Designed to increase MSL coverage
- the benefit is to increase MSL distribution and availability, ensuring alignment with the company’s goals and targets
- Initially, all MSL suggestions were pushed without a set percentage to keep but this overwhelmed the business developers
- The focus is now on determining the optimal number of MSL suggestions per customer based on compliance
- To improve efficiency and focus

2. **Historicity**:

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



3. **Promos:**

- Where suggested orders can be used to drive promotional suggestions
- The benefit here is that promos are effectively communicated at the outlet level
- Ensuring they reach the right customers
- generate increased sales


4. **New Launches:**

- Which increases the distribution of new products
- And ensures execution excellence
- Driving successful product introductions at the outlet level

