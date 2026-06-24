# Quantium Data Analytics Job Simulation
End-to-end retail analytics project completed through the **Quantium Data Analytics Virtual Experience** on [Forage](https://www.theforage.com/). Working as a data analyst supporting a supermarket's **Chips category**

End-to-end retail analytics project completed through the **Quantium Data Analytics Virtual Experience** on [Forage](https://www.theforage.com/). Working as a data analyst supporting a supermarket's **Chips category**, the project runs the full analytics lifecycle: cleaning raw transaction data, profiling customer segments, designing and evaluating a controlled store experiment, and turning the findings into a commercial recommendation for a category manager.

**Tools:** Python · pandas · NumPy · Matplotlib · Seaborn · Jupyter

---

## Overview

The client wanted answers to two business questions:

1. **Who drives chip sales, and what do they buy?** — so range, pack and promotional effort can be focused where it matters.
2. **Did a new in-store layout trial actually work?** — measured against comparable stores, isolating the trial's true effect from seasonality and market-wide trends.

The work is split across three tasks, each building on the last.

| Task | Focus | Deliverable |
|------|-------|-------------|
| **1 · Customer Analytics** | Clean transaction data, engineer features, profile customer segments and product mix | Insight on which segments and products drive the category |
| **2 · Experimentation & Uplift Testing** | Match each trial store to a control store and measure trial impact | Statistical assessment of the layout trial |
| **3 · Commercial Application** | Synthesize findings into a stakeholder-ready report | Recommendations for the category manager |

---

## Repository Structure

```
quantium-data-analytics-simulation/
├── notebooks/
│   ├── Task1_Customer_Analytics.ipynb
│   └── Task2_Trial_Control_Analysis.ipynb
├── reports/
│   └── Category_Review_Chips.pdf       # Final presentation (Task 3)
└── README.md
```

---

## Task 1 — Data Preparation & Customer Analytics

**Goal:** Clean the transaction and customer datasets, then identify the customer segments and product attributes that drive chip sales.

### Data
- **Customers:** 72,637 loyalty records across seven `LIFESTAGE` groups and three `PREMIUM_CUSTOMER` tiers (Budget / Mainstream / Premium).
- **Transactions:** 264,836 rows of chip purchases.

### Cleaning & Feature Engineering
- Checked for and confirmed no missing values; removed a duplicate transaction record.
- Standardised messy product names with regex — stripped pack-size suffixes, expanded abbreviations (e.g. `Compny → Company`, `SeaSalt → Sea Salt`, `Chckn → Chicken`), and normalised spacing and casing.
- Engineered new columns:
  - **`BRAND`** — extracted from the product name.
  - **`PACK_SIZE`** — pulled from the product description (in grams).
  - **`PRODUCT_TYPE`** — classified into Potato Chips, Corn Chips, Tortilla Chips, Crackers, and Salsa.
- Merged the customer and transaction tables on `LYLTY_CARD_NBR` for segment-level analysis.

### Key Findings

**Brand & pack size — Kettle and the 175g pack lead the category:**

| Top Brands (units) | | Top Pack Sizes (units) | |
|---|---:|---|---:|
| Kettle | 41,288 | 175g | 66,389 |
| Smiths | 28,859 | 150g | 43,131 |
| Pringles | 25,102 | 134g | 25,102 |
| Doritos | 24,962 | 110g | 22,387 |
| Thins | 14,075 | 170g | 19,983 |

**Sales by affluence tier** — Mainstream is the single largest contributor:

| Premium tier | Total sales |
|---|---:|
| Mainstream | $750,744.50 |
| Budget | $676,211.55 |
| Premium | $507,452.95 |

**Top customer segments (life stage × affluence)** — three segments sit clearly at the top of the ranking:

| Segment | Total sales |
|---|---:|
| Older Families · Budget | $168,363.25 |
| Young Singles/Couples · Mainstream | $157,621.60 |
| Retirees · Mainstream | $155,677.05 |
| Young Families · Budget | $139,345.85 |
| Older Singles/Couples · Budget | $136,769.80 |

**Takeaway:** Budget Older Families, Mainstream Young Singles/Couples, and Mainstream Retirees together drive the bulk of category spend. Combined with the dominance of Kettle and the 175g pack, this points to where range, shelf space, and promotional effort should be concentrated.

---

## Task 2 — Experimentation & Uplift Testing

**Goal:** Determine whether the new store layout trial increased sales, by comparing each trial store against a statistically matched control store that did **not** run the trial.

### Methodology
1. Aggregated transactions into **monthly store metrics**: total sales, unique customers, unique transactions, and transactions per customer.
2. Defined a **pre-trial period** of seven months (Jul 2018 – Jan 2019) and kept only stores with a complete pre-trial history.
3. For each trial store, selected the **control store** with the highest correlation in pre-trial monthly sales.
4. Compared **trial vs. control** performance over the trial window (Feb – Apr 2019).

### Trial–Control Pairs

| Trial store | Control store |
|---|---|
| 77 | 233 |
| 86 | 155 |
| 88 | 40 |

### Results

| Trial store | Sales uplift vs. control | Customer uplift vs. control |
|---|---:|---:|
| **77** | **+29.1%** | +23.5% |
| 86 | +9.8% | +13.5% |
| 88 | +10.4% | +6.6% |

**Takeaway:** All three trial stores outperformed their controls during the trial. Growth was driven mainly by **attracting more customers rather than deeper discounting** — a repeatable, profitable lever. Store 77 delivered the strongest result; for stores 77 and 86 the uplift came almost entirely from new customers (transactions per customer held roughly flat), while store 88 grew through both more customers and higher purchase frequency.

---

## Task 3 — Commercial Application

The insights from Tasks 1 and 2 were packaged into a category review presentation (`reports/Category_Review_Chips.pdf`) structured for a category manager. Headline recommendations:

1. **Roll out the trial** to stores that resemble 77, 86, and 88, prioritising those serving the top customer segments.
2. **Target the high-value segments** — build the plan around Budget Older Families and Mainstream Young Singles/Couples & Retirees.
3. **Lead with Kettle & 175g** — protect availability and shelf space for the brand and pack size shoppers reach for most.
4. **Measure & refine** — keep the control-store framework to track rollout impact and confirm gains are sustained before full scale-up.

---

## Results at a Glance

- Cleaned and standardised **264k+ transactions** and profiled **72k customers**.
- Identified **3 priority segments** and a clear **brand + pack-size** focus (Kettle, 175g).
- Built a **control-store matching framework** that isolated trial effect from background trends.
- Quantified a **+29.1% best-case sales uplift**, driven by customer acquisition — providing an evidence-based case for rollout.

---

## How to Run

```bash
# Clone the repository
git clone https://github.com/nikhilrattu/quantium-data-analytics-simulation.git
cd quantium-data-analytics-simulation

# (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate

# Install dependencies
pip install pandas numpy matplotlib seaborn openpyxl jupyter

# Launch the notebooks
jupyter notebook
```

> `openpyxl` is required to read the `.xlsx` transaction file.

---

## Skills Demonstrated

- **Data cleaning & wrangling** — regex-based text normalisation, deduplication, type handling, feature engineering.
- **Exploratory analysis** — `groupby` aggregation, pivot tables, and visualisation with Matplotlib/Seaborn (bar, box, count, heatmap, point, and line plots).
- **Experiment design** — control-store selection via correlation matching and pre/post uplift measurement.
- **Commercial storytelling** — translating quantitative findings into clear, actionable business recommendations.

---

## Acknowledgements

Completed as part of the **Quantium Data Analytics Job Simulation** on Forage. The datasets and project brief are provided by Quantium through the Forage platform for educational purposes.

---

**Nikhil Rattu** · [GitHub](https://github.com/nikhilrattu) · [LinkedIn](https://www.linkedin.com/in/nikhilrattu)# quantium-data-analytics-simulation
# quantium-data-analytics-simulation
