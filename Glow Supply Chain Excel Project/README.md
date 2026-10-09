# Glow Fashion & Beauty Store Supply Chain Analysis Dashboard

<img width="947" height="467" alt="image" src="https://github.com/user-attachments/assets/11158c40-fba5-4f46-872a-17714614c96f" />

### 📊 Project Overview

**Have you ever thought about what happens behind the products on a beauty store shelf?**

Before a bottle of skincare or a pack of haircare reaches a customer, it passes through suppliers, manufacturing, inventory, transportation, and delivery. This project looks at the full supply chain behind Glow Fashion & Beauty Store — 100 products tracked across 5 Indian cities (Mumbai, Delhi, Bangalore, Chennai, Kolkata) — to see where revenue, risk, and inefficiency actually live.

#### The Approach

Using Excel, I cleaned the raw supply chain data, built PivotTables to answer a set of business questions one at a time, and put together an interactive dashboard with slicers to explore how product type, carrier, transport mode, and location each affect revenue, stock, and defect rates.

The questions I explored:

* Which product category drives the most revenue?
* Does a higher price mean higher revenue?
* Are inventory levels aligned with demand?
* Which shipping carrier generates the most revenue?
* Is the cheapest transportation option actually the best?
* Where are the highest defect rates occurring?

### 🕹️ Interactive Dashboard Demo

See the dashboard filters, dynamic metrics, and charts in action below:

https://github.com/user-attachments/assets/fd63c0f5-58cf-41f4-97d4-0fdc2cc99b4c

### To see the full live analysis: [Click here](https://lnkd.in/p/eyMptgdn)

### 💡 Key Data Insights & Discoveries

1. **Skincare Leads on Price and Revenue:** Skincare has the highest average product price of the three categories, and it's also the top revenue earner at ₹241,628 (41.8% of total revenue) — customers are paying a premium for it, and demand is holding strong anyway.
2. **Cosmetics Is Priced Lowest and Still Earns the Least:** Cosmetics isn't underperforming because it's expensive — it's the cheapest category and still brings in the smallest share of revenue (27.96%), pointing to a demand or visibility problem rather than a pricing one.
3. **Carrier B Moves the Most Value:** Carrier B transported and delivered the products behind **43% of total revenue (₹250,095)** — more than Carrier A and Carrier C combined with room to spare — making its reliability the most important of the three to monitor.
4. **Transport Risk Isn't the Same for Every Product:** Haircare's highest defect rate comes from sea freight (3.64%), while skincare and cosmetics are both riskiest on road transport — a one-size-fits-all shipping strategy would get this wrong.
5. **Sea Is the Cheapest Transport Mode by a Clear Margin:** Sea freight averages ₹418 per shipment, well below Road (₹553), Rail (₹542), and Air (₹562) — but it's also the highest-defect option for haircare, so the cheapest choice isn't automatically the best one.

### 🛠️ Excel Skills & Dashboard Setup

To turn 100 raw product rows into a clear, filterable dashboard, I used Excel's data cleaning, table, PivotTable, and dashboard features:

* **Data Cleaning & Preparation:** Loaded the raw `Supply_chain_data` sheet and cleaned it before building anything.
  * The source file had **two separate columns both loosely named "lead time"** — one for how long it takes a product to be ready, one for how long a supplier takes to deliver. I renamed them clearly as **Product Lead Time (Days)** and **Supplier Lead Time (Days)** so they couldn't be confused or mixed up in a pivot table.
  * Renamed **Availability** to **Supplier Availability** and **Stock levels** to **Glow Stock levels**, so column names describe what they actually measure instead of being generic.
  * Added a calculated **Defect Rate (%)** column (`= [Defect rates] / 100`), since the raw Defect rates column held an awkward decimal that wasn't formatted as a true percentage.
  * Converted the cleaned data into a structured Excel Table (`Glow`), so every PivotTable and chart in the workbook updates automatically from one source.

* **Key Metric Tracking:** Created KPI cards to highlight the main numbers, including **Total Revenue (₹577,605), Best Seller (Skincare, ₹241,628 / 41.8%), Top Regional Product (Kolkata – Skincare, ₹77,886 / 8,101 units), Top Specified Customer Segment (Female, ₹161,514 / 28.0%), and Top Transport Mode by Revenue (Rail, ₹164,990).**

 <img width="707" height="44" alt="image" src="https://github.com/user-attachments/assets/459ff942-6e9c-4223-ae43-8c278a145c99" />

* **Handling an "Unknown" Customer Segment:** The Customer demographics column included an "Unknown" value that actually generates the single highest revenue share (30.0%) of any segment — ahead of Female (28.0%). Rather than letting an unlabeled category claim the "top customer" spot, I labeled the KPI card **"Top Specified Customer"** so it reports the top *named* segment instead of an unidentified one.

* **Chart Analysis:** Built visuals to compare product type against average price, break down total sales by percentage, rank SKUs by revenue and stock level, compare shipping costs and cost distribution across carriers and transport modes, and show defect rates by product type and transport mode side by side.

* **Interactive Slicers:** Added slicers for **Product Type** and **Location**, letting users filter the whole dashboard down to a specific category (cosmetics, haircare, skincare) or city (Bangalore, Chennai, Delhi, Kolkata, Mumbai).

<img width="230" height="86" alt="image" src="https://github.com/user-attachments/assets/5b6d86de-170e-4b0a-81d6-dd6406e74804" />

### 📈 Strategic Recommendations & Next Steps

* **Re-check the "top revenue SKU isn't well-stocked" story.** SKU51 is the single highest revenue earner (₹9,866), and it's also tied for the *highest* stock level in the whole dataset (100 units, alongside SKU12 and SKU59) — the opposite of a stockout risk. Worth re-reading the Stock Level by SKU chart carefully before repeating that finding.
* **Don't cut Cosmetics prices further.** It's already the cheapest category and still earns the least — the problem looks like demand or visibility, not price.
* **Keep Carrier B's reliability under close watch.** Since it carries 43% of all revenue-generating shipments, any disruption there has an outsized effect on the business.
* **Avoid a blanket "cheapest transport mode wins" rule.** Sea is cheapest overall, but it's also the highest-defect option for haircare — transport mode should be chosen per product category, not store-wide.

### 📊 Behind the Data: Pivot Table Breakdown

<details>
<summary><b>Click to expand and view individual Pivot Tables 🔍</b></summary>
<br>

To build the final dashboard, I broke down the raw data using these targeted pivot tables and charts:

#### 1. Average Price & Revenue by Product Type
*Shows the average product price next to the total revenue for each category — skincare brings in the most despite not being the cheapest.*

<img width="1629" height="503" alt="Screenshot 2026-10-09 062747" src="https://github.com/user-attachments/assets/e4fbabaf-876a-4b3d-ab68-34ff7eaa62c9" />

#### 2. Sales Share by Product Type
*Breaks total revenue down into percentages across cosmetics, haircare, and skincare, to see how the pie actually splits.*

<img width="1049" height="422" alt="Screenshot 2026-10-09 062846" src="https://github.com/user-attachments/assets/169e3705-3d71-4205-ba3c-b8dcf68b726b" />

#### 3. Revenue by Shipping Carrier
*Ranks the three carriers by total revenue moved, showing how much of the business each one physically transports and delivers.*

<img width="1517" height="439" alt="Screenshot 2026-10-09 062915" src="https://github.com/user-attachments/assets/f26d375d-17ff-45f9-b907-d1bbc6d203bf" />

#### 4. Revenue by SKU
*Ranks every SKU from highest to lowest revenue, to spot the small group of top performers driving the bulk of sales.*

<img width="1295" height="907" alt="Screenshot 2026-10-09 062955" src="https://github.com/user-attachments/assets/285c62f8-a01c-4c7e-acd8-e19e75394cac" />

#### 5. Stock Levels by SKU
*Ranks every SKU by how many units are currently held in stock, to check whether inventory lines up with what's actually selling.*

<img width="1885" height="903" alt="Screenshot 2026-10-09 063035" src="https://github.com/user-attachments/assets/af5b3bd2-09e5-4dcd-aeb8-7a8931dadfb0" />

#### 6. Shipping Costs by Carrier
*Compares the average shipping cost per carrier, to separate true cost differences from costs driven purely by shipment volume.*

<img width="1282" height="455" alt="Screenshot 2026-10-09 063117" src="https://github.com/user-attachments/assets/e8a8eeeb-d83c-437b-ada7-e712abe288c2" />

#### 7. Cost Distribution by Transport Mode
*Compares average transportation cost across Air, Road, Rail, and Sea, to see which mode carries the heaviest price tag.*

<img width="1506" height="508" alt="Screenshot 2026-10-09 063149" src="https://github.com/user-attachments/assets/122f650a-636e-4555-85a5-f4ebca81e3ee" />

#### 8. Defect Rates by Product Type & Transport Mode
*Breaks down average defect rate for each product category by the transport mode used, to find which combination carries the most risk.*

<img width="1266" height="539" alt="Screenshot 2026-10-09 063236" src="https://github.com/user-attachments/assets/8b5c1204-7767-4e86-a1de-278eddbd4aaa" />

</details>

### 📂 How to Open and Explore the Workbook

1. You can download the full file here: [Glow_Supply_Chain_Project.xlsx](https://github.com/DataWithMowa/Quantum-Analytics-Supply-Chain-Data-Analysis-Projects/tree/main/Glow%20Supply%20Chain%20Excel%20Project/Full%20Project)
2. Open the file locally using Microsoft Excel.
3. Go to the **DashBoard** sheet.
4. Use the **Product Type** and **Location** slicers to filter all the charts dynamically.
5. Check the **Pivot Engine** sheet to see the PivotTable behind each chart, and the **Glow** sheet for the cleaned source data.

### 🤝 Connect & Support

Thank you for taking the time to go through this project! If you have any questions or feedback, please reach out directly:

* 💼 **LinkedIn:** [Mowaninuola Umarudeen](https://www.linkedin.com/in/mowaninuolaumarudeen/)
* 📧 **Email:** [mowatheanalyst@gmail.com](mailto:mowatheanalyst@gmail.com)

*📈 **Did you find this useful?** Consider giving this repository a ⭐ **Star** if it helped you!*
