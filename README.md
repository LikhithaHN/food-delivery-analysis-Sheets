# 🍽️ Food Delivery Analysis — Google Sheets Dashboard

An end-to-end analysis of **8,568 food delivery orders** across **5 Indian cities (2015–2020)**, built entirely in Google Sheets: data cleaning, lookups, pivot tables, KPI dashboard, and a regression analysis of what drives delivery time.

🔗 **[View the live spreadsheet](https://docs.google.com/spreadsheets/d/1SgRyEL5y3HWO1whouk4umbfAoH79tBNjHVHrbqaCji4/edit?usp=sharing)** (view-only)

![Dashboard](images/dashboard.png)

---

## 📌 Business Questions

1. How are orders and revenue distributed across cities, cuisines, time slots and payment methods?
2. How well is the platform performing on delivery speed?
3. **Why are ~80% of deliveries marked late — is it an operational failure or something else?**
4. How satisfied are customers, and how much do delivery fees contribute to revenue?

---

## 🗂️ Dataset

Each row is one order, with 21 columns built from several lookup tables (cities, customers, dishes, cuisines, ratings, discounts, delivery times and distances).

| Field group | Columns |
|---|---|
| Order | Order ID, Order Date, Slot, Customer ID |
| Location | Area Code, City, Distance (km) |
| Food | Dish Code, Cuisine |
| Money | Order Value, Discount (%), Final Price, Delivery Fee, Customer Payable |
| Outcome | Delivery Time (min), Rating (1–5), Experience, Speed |

**Derived fields**

- **Final Price** = Order Value × (1 − Discount %)
- **Customer Payable** = Final Price + Delivery Fee
- **Experience**: Good (4–5), Average (3), Bad (1–2)
- **Speed**: Quick delivery (< 30 min), On time (30–45 min), Late delivery (> 45 min)

---

## 🛠️ Approach

1. **Data preparation**: combined the lookup tables into one order-level table using lookup formulas (city from area code, cuisine from cuisine code, price from dish code, and so on).
2. **Feature engineering**: calculated final price, customer payable, and the experience and speed categories.
3. **Pivot analysis**: summarised orders and revenue by city, cuisine, month, time slot, payment method, delivery speed and customer experience.
4. **Statistical analysis**: used correlation and linear regression to test whether distance explains delivery time.
5. **Dashboard**: built KPI cards and charts driven by live formulas from the data sheet.

---

## 📊 Key Metrics

| Metric | Value |
|---|---|
| Total Sales (customer payable) | ₹50,59,317 |
| Orders Delivered | 8,568 |
| Overall Rating | 3.00 / 5 |
| Avg Order Value (gross, before discount) | ₹663 |
| Avg Amount Paid per Order (net) | ₹590 |
| Avg Delivery Time | 69.1 min |
| Late Delivery Rate | 80.1% |
| Delivery Fee as % of Sales | 3.8% |

---

## 🔍 Key Findings

### 1. Distance drives delivery time
| Statistic | Value |
|---|---|
| Correlation (r) | 0.85 |
| R² | 71.7% |
| Slope | +9.1 min per extra km |
| Intercept | 14.6 min |

| Distance band | Avg delivery time | Orders |
|---|---|---|
| 2–4 km | 41.4 min | 2,139 |
| 4–6 km | 59.2 min | 2,024 |
| 6–8 km | 77.3 min | 2,164 |
| 8–10 km | 96.4 min | 2,241 |

![Distance vs delivery time](images/distance_vs_delivery_time.png)

### 2. The 80% late rate comes mainly from the threshold, not from any one city
- The "late" cutoff is 45 minutes. The regression line crosses 45 minutes at about **3.3 km**, but the **average order travels 6 km**, so most orders are expected to be late.
- The late rate is almost identical in every city, which points to a system-wide cause rather than local operations:

| City | Orders | Late | Late rate |
|---|---|---|---|
| Bangalore | 1,715 | 1,362 | 79.4% |
| Delhi | 1,804 | 1,450 | 80.4% |
| Kolkata | 1,798 | 1,433 | 79.7% |
| Mumbai | 1,582 | 1,291 | 81.6% |
| Pune | 1,669 | 1,330 | 79.7% |

### 3. Mexican leads revenue while Continental leads volume
- **Continental** has the most orders (1,323), but **Mexican** earns the most revenue (₹10.7L, 21% of sales) because of its higher prices.
- **North Indian** is lowest on both orders (680) and revenue (₹3.7L).

### 4. Customer ratings are polarised
- Good: 39.5%, Average: 21.2%, Bad: 39.3%. Customers tend to be either happy or unhappy, with few in the middle.

### 5. Demand is evenly spread
- Orders are split almost equally across the 5 time slots and the 5 payment methods (about 20% each), so no single slot or payment method dominates.

### 6. Delivery fees are distance-based
- The fee is ₹0 up to about 4 km, then roughly ₹10 for each additional km. Fees make up only **3.8% of total sales**.

---

## 💡 Recommendations

1. **Set distance-based delivery targets.** A flat 45-minute target labels most long-distance orders as late by default. Promised times that scale with distance would give a truer view of performance.
2. **Review the delivery radius** or add faster dispatch options for orders beyond about 6 km, where average delivery times exceed 60 minutes.
3. **Promote high-value cuisines** such as Mexican and Continental, and investigate why North Indian underperforms.

---

## 🚀 Next Steps

- Compare ratings across delivery-speed categories to test whether late deliveries actually lower ratings.
- Show a year-over-year monthly trend instead of combining all years into one 12-month view.
- Rebuild the dashboard in Power BI with interactive filters.

---

## 🧰 Tools & Skills

**Google Sheets**: lookup formulas, pivot tables, conditional logic, charts, KPI dashboard design
**Statistics**: correlation, linear regression, R²
**Analysis**: data cleaning, feature engineering, business storytelling

---

## 📁 Repository Structure

```
food-delivery-analysis/
├── README.md
├── data/
│   └── food_delivery_orders.csv
├── dashboard/
│   └── food_delivery_dashboard.xlsx
└── images/
    ├── dashboard.png
    └── distance_vs_delivery_time.png
```

---

👤 **Rakesh**, aspiring Data Analyst
[LinkedIn](#) · [GitHub](#)
