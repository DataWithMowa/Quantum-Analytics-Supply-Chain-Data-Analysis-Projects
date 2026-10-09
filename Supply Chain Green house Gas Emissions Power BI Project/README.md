# Supply Chain Greenhouse Gas Emissions Dashboard

<img width="943" height="465" alt="SupplyChain Dashboard" src="https://github.com/user-attachments/assets/8d220951-32d9-435c-b47a-bfd367756b7e" />

### 📊 Project Overview

This project was built to understand **which industries carry the heaviest greenhouse gas footprint per dollar spent**, using the EPA's Supply Chain GHG Emission Factors dataset, and to turn 1,016 sector-level records into insights that go beyond "who pollutes the most" to "where in the supply chain does that emission actually sit."

Using Power BI, I cleaned and grouped the data, calculated key metrics, and built an interactive dashboard to explore **emission factors by sector, by broad industry group, and by where the emissions fall — within the sector's own production, or in the margins (transport, wholesale, retail) around it**.

The analysis also explored:

* Which individual sectors carry the highest and lowest emission factor per dollar.
* Why the highest-emitting sector's number is driven entirely by its own operations, with no margin emissions at all.
* Which broad industry groups carry the heaviest average footprint once all 1,016 sectors are grouped.
* Which sectors are high in their own supply-chain emissions but low in margin emissions, and which show the opposite pattern.

I built the dashboard completely in **Power BI**, using data to look beyond "which sector emits the most" and understand *where* in the supply chain that emission is coming from.

### 🕹️ Interactive Dashboard Demo

See the dashboard filters, dynamic metrics, and charts in action below (53-second walkthrough): 

https://github.com/user-attachments/assets/478f52a4-9814-4521-bf10-8915a39b4476

### To see the full live analysis: [Click here](https://lnkd.in/p/e3PKrdmk)

### 💡 Key Data Insights & Discoveries

1. **Solid Waste Landfill Is the Single Highest-Emitting Sector:** It carries an emission factor of **10.989 kg CO2e per dollar**, nearly 3x higher than the next sector (Cement Manufacturing, 3.858) — and its entire footprint comes from its own operations, with a margin emission factor of 0.
2. **Agriculture, Forestry & Fishing Carries the Heaviest Average Load:** Once all 1,016 sectors are grouped into 18 broad industries, Agriculture, Forestry & Fishing has the highest average emission factor (1.24), followed by Mining, Quarrying, Oil & Gas (0.87) — well ahead of service-based groups like Finance & Insurance (0.07), the lowest.
3. **Creative and Residential-Rental Sectors Sit at the Bottom:** Independent Artists, Writers, and Performers has the lowest emission factor in the entire dataset (0.013), pointing to where low-carbon economic growth is easiest to find.
4. **Farming Dominates the Top-10 List:** Beyond Landfill and Cement, 8 of the next 9 highest-emitting sectors are farming-related — Beef Cattle Ranching, Cattle Feedlots, and five grain/rice/wheat farming categories all sit at or above 3.0.
5. **Where the Emission Sits Changes the Story:** Comparing a sector's own emissions against its margin emissions shows two different risk types — Solid Waste Landfill is high in its own operations but zero in margins, while sectors like Bituminous Coal Underground Mining are higher in margin emissions (transport, wholesale, retail) than in their own.

### 🛠️ Power BI Skills & Dashboard Setup

To turn 1,016 raw EPA sector records from one flat CSV file into a sector-level and industry-level emissions picture, I used Power BI's data cleaning, DAX, and dashboard features:

* **Data Cleaning & Preparation (Power Query):** Loaded the single `SupplyChainGHGEmissionFactors_v1.2_NAICS_CO2e_USD2021.csv` file and cast each column to its correct type — whole numbers for the NAICS code, decimal numbers for the three emission factor columns, and text for the sector title, GHG type, unit, and USEEIO reference code.

* **Data Modeling:** This project came from a single flat table of 1,016 NAICS sectors with no repeating records to split out, so one clean table was the right model — no separate fact/dimension tables were needed.

<img width="541" height="324" alt="image" src="https://github.com/user-attachments/assets/cfe613c1-7c41-4a53-8a37-487f248eb1c7" />

* **Grouping 1,016 Sectors into 18 Industries (Calculated Column):** The raw file only had a 6-digit NAICS code per sector — too granular to compare at a glance. I wrote a DAX calculated column, **Sector Group**, that reads the first 2 digits of each NAICS code and maps it to its broad industry (e.g. codes starting "11" → Agriculture, Forestry, Fishing; "31"–"33" → Manufacturing), so every one of the 1,016 sectors rolls up into one of 18 readable industry groups:

```dax
Sector Group =
VAR SectorCode = LEFT(FORMAT('SupplyChain GHGE'[2017 NAICS Code], "000000"), 2)
RETURN
SWITCH(
    TRUE(),
    SectorCode = "11", "Agriculture, Forestry, Fishing",
    SectorCode = "21", "Mining, Quarrying, Oil & Gas",
    SectorCode = "22", "Utilities",
    SectorCode = "23", "Construction",
    SectorCode IN {"31", "32", "33"}, "Manufacturing",
    SectorCode = "42", "Wholesale Trade",
    SectorCode IN {"44", "45"}, "Retail Trade",
    SectorCode IN {"48", "49"}, "Transportation & Warehousing",
    SectorCode = "51", "Information",
    SectorCode = "52", "Finance & Insurance",
    SectorCode = "53", "Real Estate & Rental",
    SectorCode = "54", "Professional & Technical Services",
    SectorCode = "56", "Administrative & Waste Services",
    SectorCode = "61", "Educational Services",
    SectorCode = "62", "Health Care & Social Assistance",
    SectorCode = "71", "Arts, Entertainment & Recreation",
    SectorCode = "72", "Accommodation & Food Services",
    SectorCode = "81", "Other Services",
    SectorCode = "92", "Public Administration",
    "Other"
)
```

* **DAX Measures:** Kept all measures in one dedicated `Measures (2)` table so they are easy to find:

| Measure | What it does | DAX |
|---|---|---|
| **Total Sectors** | Counts every NAICS sector in the dataset | `COUNTROWS('SupplyChain GHGE')` |
| **Avg Emission Factor** | Average emission factor with margins, across all sectors | `AVERAGE('SupplyChain GHGE'[Supply Chain Emission Factors with Margins])` |
| **Highest Emission Sector** | Returns the name of the single highest-emitting sector | `VAR MaxValue = MAX([Emission Factors with Margins]) RETURN CALCULATE(SELECTEDVALUE([2017 NAICS Title]), [Emission Factors with Margins] = MaxValue)` |
| **Highest Emission Value** | Returns that sector's emission factor | `MAX('SupplyChain GHGE'[Supply Chain Emission Factors with Margins])` |
| **Lowest Emission Sector** | Returns the name of the single lowest-emitting sector | `VAR MinValue = MIN([Emission Factors with Margins]) RETURN CALCULATE(SELECTEDVALUE([2017 NAICS Title]), [Emission Factors with Margins] = MinValue)` |
| **Lowest Emission Value** | Returns that sector's emission factor | `MIN('SupplyChain GHGE'[Supply Chain Emission Factors with Margins])` |
| **Top Industry Group** | Returns the broad industry group with the highest average emission factor | `VAR MaxAvg = MAXX(VALUES([Sector Group]), CALCULATE(AVERAGE([Emission Factors with Margins]))) RETURN CALCULATE(SELECTEDVALUE([Sector Group]), FILTER(VALUES([Sector Group]), CALCULATE(AVERAGE([Emission Factors with Margins])) = MaxAvg))` |

<img width="209" height="135" alt="image" src="https://github.com/user-attachments/assets/14a6653a-bf91-49d7-bfd8-f143138248b4" />

* **Key Metric Tracking:** Created KPI cards to highlight the main numbers, including **Total Sectors (1,016), Avg Emission Factor (0.386), Highest Emission Sector (Solid Waste Landfill, 10.989), Lowest Emission Sector (Independent Artists, Writers, and Performers, 0.013), and Top Industry Group (Agriculture, Forestry, Fishing, 1.24 avg).**

<img width="664" height="55" alt="image" src="https://github.com/user-attachments/assets/ea58c129-84a6-4c8e-a6e5-472b006f210d" />

* **Chart Analysis:** Used a **ranked bar chart** to show the top 10 highest-emitting sectors, a **scatter chart** comparing each sector's emission factor without margins against its margin emission factor (to separate "high in its own operations" sectors from "high in transport/retail margins" sectors), and a **grouped bar chart** comparing average emission factor across all 18 industry groups.

* **Interactive Slicers:** Added slicers for **Sector Group** and **Sector Title**, letting users filter the whole dashboard down to a specific broad industry or sector.

<img width="111" height="30" alt="image" src="https://github.com/user-attachments/assets/4a7e912d-8b94-404b-a146-2eea8c74679f" />

### 📈 Strategic Recommendations & Next Steps

* **Target landfill diversion first.** Solid Waste Landfill's emission factor is nearly 3x the next-highest sector, and it's driven entirely by on-site operations (zero margin emissions) — a waste-reduction or methane-capture policy aimed squarely at this sector would have an outsized impact relative to its size.
* **Treat farming as a cluster, not a single line item.** 8 of the top 10 highest-emitting sectors are farming categories, so policy or efficiency programs aimed at agriculture should expect to move several related sectors at once, not just one.
* **Separate "operational" emitters from "margin" emitters before acting.** Sectors like Bituminous Coal Underground Mining carry more of their emissions in the margins (transport, wholesale, retail) around them than in their own operations — a different kind of intervention (logistics, distribution) than a sector like Solid Waste Landfill needs.
* **Use the low-emission sectors as a growth lens.** Independent Artists/Writers/Performers and Lessors of Residential Buildings sit at the very bottom of the list — useful reference points for where economic growth can happen with the smallest emissions cost.

### 📂 How to Open and Explore the Dashboard

1. You can download the full file here: [Supply_Chain_GHGE_Project.pbix](https://github.com/DataWithMowa/Quantum-Analytics-Supply-Chain-Data-Analysis-Projects/tree/main/Supply%20Chain%20Green%20house%20Gas%20Emissions%20Power%20BI%20Project/Full%20Project)
2. Open the file locally using Power BI Desktop.
3. Go to the Dashboard page.
4. Use the Sector Group and Sector Title slicer to filter all the charts down to one broad industry at a time.
5. Hover over the scatter chart to compare a sector's own emissions against its margin emissions.

### 🤝 Connect & Support

Thank you for taking the time to go through this project! If you have any questions or feedback, please reach out directly:

* 💼 **LinkedIn:** [Mowaninuola Umarudeen](https://www.linkedin.com/in/mowaninuolaumarudeen/)
* 📧 **Email:** [mowatheanalyst@gmail.com](mailto:mowatheanalyst@gmail.com)

*📈 **Did you find this useful?** Consider giving this repository a ⭐ **Star** if it helped you!*
