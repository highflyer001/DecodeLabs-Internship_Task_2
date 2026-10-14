# E-commerce Orders Analysis (Excel)

A descriptive analysis of 1,200 e-commerce orders (January 2023 to June 2025). The project cleans the data in Power Query, then calculates summary statistics, detects outliers and identifies trends using Excel formulas and PivotTables.

## Objectives

- Calculate the mean, median and counts for key fields
- Identify outliers in order values
- Identify trends over time and across categories

## Dataset

| Column | Description |
|---|---|
| OrderID | Unique order identifier |
| Date | Order date |
| Year | Order date Year |
| Quarter | Order date quarter |
| CustomerID | Customer identifier |
| Product | Laptop, Phone, Tablet, Monitor, Printer, Desk, Chair |
| Quantity | Units ordered (1 to 5) |
| UnitPrice | Price per unit |
| PaymentMethod | Online, Cash, Credit Card, Debit Card, Gift Card |
| OrderStatus | Pending, Shipped, Delivered, Cancelled, Returned |
| ItemsInCart | Items in the cart at checkout (1 to 10) |
| CouponCode | FREESHIP, WINTER15, SAVE10 (blank = no coupon) |
| ReferralSource | Instagram, Email, Google, Facebook, Referral |
| TotalPrice | Quantity x UnitPrice |
| TotalRevenue | Sanity check for TotalPrice |
| Outliers | Orders above IQR |

**Data quality:** no duplicate OrderIDs, and `TotalPrice` equals `Quantity x UnitPrice` for every row. The only blanks are in `CouponCode` (309 rows), which means no coupon was used.

## Tools

- Microsoft Excel (formulas, PivotTables, charts)
- Power Query (data cleaning)

## Methods

- **Central tendency and spread:** `AVERAGE`, `MEDIAN`, `STDEV.S`, `MIN`, `MAX`
- **Counts:** `COUNTIF`, `IF`, and PivotTables
- **Outliers:** the IQR rule (fences at Q1 - 1.5 x IQR and Q3 + 1.5 x IQR) using `QUARTILE.INC`
- **Trends:** PivotTables by year and quarter, with line charts and trendlines

## Key Findings

### Summary statistics

| Metric | Mean | Median | Std Dev | Min | Max |
|---|---|---|---|---|---|
| Quantity | 2.95 | 3 | 1.41 | 1 | 5 |
| UnitPrice | 356.41 | 364.21 | 197.18 | 11.39 | 699.93 |
| ItemsInCart | 5.49 | 5 | 2.28 | 1 | 10 |
| TotalPrice | 1,053.97 | 823.62 | 819.86 | 11.39 | 3,456.40 |

- Total revenue is about 1,264,761.96
- The mean `TotalPrice` is well above the median, so the distribution is right-skewed (skewness of about 0.89). The median is the better measure of a typical order.

### Counts

Orders are spread very evenly across every category:

- **Product:** Printer 181, Tablet 179, Chair 178, Laptop 173, Desk 170, Monitor 163, Phone 156
- **Status:** Cancelled 250, Returned 247, Pending 237, Shipped 235, Delivered 231
- **Payment:** Online 258, Cash 246, Credit Card 234, Debit Card 232, Gift Card 230
- **Coupon:** FREESHIP 313, none 309, WINTER15 292, SAVE10 286
- **Referral:** Instagram 259, Email 250, Google 241, Facebook 228, Referral 222

### Outliers

- 8 orders exceed the upper IQR fence (about 3,330). No order is beyond 3 standard deviations.
- All 8 are quantity-5 orders of items priced around 670 to 690, so they are genuine large orders rather than data errors, and were kept in the analysis.
- `UnitPrice`, `Quantity` and `ItemsInCart` have no outliers.
- At the monthly level, May 2023 (about 63.8k) and June 2024 (about 68.1k) are unusually high revenue months.

### Trends

- **Revenue is declining year over year.** Comparing January to June across the three years (a fair comparison, since 2025 ends in June), revenue fell from about 286.5k to 257.1k to 231.9k, roughly 10% a year.
- **Seasonality is mostly an artefact.** January to June has three years of data and July to December only two, so raw monthly totals are misleading. After adjusting per year, June is the only clear peak.
- **Cancellation and return rate is 41.4%.** Revenue from orders that were not cancelled or returned is about 745k.
- **Products:** Chair, Printer and Laptop earn the most revenue (about 192k to 196k each) and Phone the least (about 152k).
- **Coupons have no visible effect.** Average order value is about the same with or without a coupon, and no discount appears in `TotalPrice`.
- **Order value drivers:** `UnitPrice` (r = 0.72) and `Quantity` (r = 0.62) correlate most strongly with `TotalPrice`. `ItemsInCart` is weaker (r = 0.39).
- **Repeat customers are rare.** Only 11 of 1,189 customers placed more than one order.

## Limitations

- The data ends in June 2025, so full-year comparisons involving 2025 are not valid.
- The even category splits suggest the data may be synthetic, so business conclusions about products, payment methods or referral sources should be treated cautiously.
- This is a descriptive analysis only. It shows patterns but does not explain their causes.

## Author

**[Esther Oludimu]**
@highflyer001]
