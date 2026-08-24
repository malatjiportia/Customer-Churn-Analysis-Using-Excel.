# Bank Customer Churn Analysis Using Excel

## Overview
This project analyzes churn behavior for roughly 10,000 customer accounts at a European bank, using Microsoft Excel (Power Query, PivotTables, and formulas) to identify the key drivers of churn and produce an interactive dashboard for retention decision-making.

**Tools used:** Microsoft Excel, Power Query, PivotTables, calculated columns/formulas
**Data source:** Maven Analytics — Bank Customer Churn dataset

## Problem Statement
Customer churn directly affects revenue and growth, and large, unmerged datasets make it hard to identify the drivers of attrition without a structured analysis. This project consolidates customer and account data to uncover churn patterns and translate them into actionable retention recommendations.

## Objectives
1. Identify key factors contributing to customer churn
2. Calculate churn rate and observe trends across segments
3. Use Excel tools (PivotTables, charts, formulas) for analysis
4. Build a dashboard for clear data visualization
5. Provide actionable insights to reduce churn

## Data Overview
Two source datasets, joined on `CustomerId`:

| Dataset | Key Fields |
|---|---|
| Customer Info | CustomerId, Surname, CreditScore, Geography, Gender, Age, Tenure, EstimatedSalary |
| Account Info | CustomerId, Balance, NumOfProducts, HasCrCard, Tenure, IsActiveMember, Exited (target) |

Merged into a single `BankChurnClean` sheet using Power Query's Merge Queries function.

## Data Cleaning
- **Merging:** Customer Info and Account Info joined on `CustomerId`
- **Missing values:** 3 rows removed (missing Age, negative EstimatedSalary, blank Surname) — dataset reduced from ~10,000 to 9,997 rows
- **Duplicates:** 1 duplicate record removed
- **Standardization:** TRIM applied across all columns; PROPER applied to Surname; numeric fields (CreditScore, EstimatedSalary, Balance) converted to Number/Currency format
- **Invalid entries corrected:** Geography inconsistencies standardized — 1,618 "FRA" and 1,655 "French" entries mapped to "France"; decimal separators corrected in currency fields
- **Calculated columns added:**
  - **Age Group:** 18–30, 31–45, 46–60, 61+
  - **Credit Score Group:** Poor, Fair, Good, Very Good, Excellent
  - **Balance Group:** No Balance, Low, Mid-Tier, Upper-Mid-Tier, High Balance

## Key Metrics
| Metric | Value |
|---|---|
| Total customers | 9,997 |
| Total churned | 2,037 |
| Overall churn rate | 20.4% |

## Findings by Segment

| Segment | Churn Rate | Insight |
|---|---|---|
| Low Balance | 66.67% | Highest-risk group overall |
| Product 4 users | 100.00% | Every customer on this product churned |
| Product 3 users | 82.71% | Near-total churn; urgent review needed |
| Age 46–60 | 51.12% | Churns at more than double the portfolio average |
| Germany | 32.46% | Roughly double Spain (16.68%) and France (16.16%) |
| Mid-tier Balance | 31.88% | Elevated despite moderate wealth |
| Female customers | 25.08% | vs. 16.46% for male customers |
| Age 18–30 | 7.52% | Most loyal segment |
| Product 2 users | 7.58% | Healthiest product retention |

**Notes:**
- Credit score is a comparatively weak churn predictor — rates are fairly uniform (18.6%–22.0%) across all bands.
- "Total Active Customers" on the dashboard refers to the `IsActiveMember` flag, which is a separate measure from churn status (`Exited`) — the two shouldn't be summed together.

## Strategic Recommendations

**Priority 1 — Immediate**
- Emergency product review for Products 3 & 4 (pricing, features, exit survey data)
- Proactive outreach for low-balance customers (fee waivers, balance-building incentives)

**Priority 2 — High impact**
- Root-cause investigation into Germany's elevated churn (competitive landscape, local product fit)
- Dedicated retention program for the 46–60 age cohort (relationship managers, loyalty tiers)

**Priority 3 — Sustained improvement**
- Audit customer journey and marketing touchpoints for gender-related friction
- Build referral/advocacy programs around the loyal 18–30 segment
- Study Product 2's low churn rate and apply learnings to other products

## Metrics to Track Going Forward
| Metric | Target | Priority |
|---|---|---|
| Overall churn rate | < 15% | High |
| Low-balance churn rate | < 40% | Critical |
| Product 3 churn rate | < 30% (post-fix) | Critical |
| Germany churn rate | < 22% | High |
| 46–60 age group churn | < 35% | High |
| Product 2 churn rate | Maintain < 10% | Medium |

## Conclusion
The three most actionable risks — Product 3/4 failure, the low-balance segment, and Germany's market-specific churn — are discrete and addressable. Fixing these could plausibly reduce overall churn by an estimated 5–8 percentage points, with sustained gains from age-cohort retention programs and balance-building initiatives.

## Limitations
This is a cross-sectional snapshot rather than a time-series view, so trend-over-time claims are directional rather than measured. Segment relationships (e.g., gender, geography) are correlational, not causal.

