# Intuit Ecosystem Analytics - Final Analysis Report

## Executive Summary

This report presents a comprehensive analysis of Intuit's customer and usage data from June 2021. The analysis covers **9,955 unique customers** (represented by 15,000 customer-product records) and **230,000 usage events** across four products: QuickBooks, CreditKarma, Mint, and TurboTax.

### Key Findings at a Glance

- **Total Unique Customers**: 9,955 (June 2021 cohort)
- **Customers with Product Assignment**: 6,665 (66.95%)
- **Activation Rate**: 100% (of customers with product assignment)
- **Purchase Conversion Rate**: 59.83% (of activated customers with products)
- **Overall Signup to Purchase**: 40.05% (of all customers: 3,988/9,955)
- **Churn Rate**: 34.36% (of customers with product assignment)
- **Currently Active**: 25.48% (purchased and not cancelled)

---

## Methodology & Data Decisions

### Data Quality Approach

**Decision: Analyze at CUSTOMER level (not row level) and exclude only customers with ZERO product assignments**

#### Critical Methodology Correction:
The analysis is performed at the **customer level** (aggregated by Customer ID), not at the row level. This is critical because:

1. **Multiple product assignments per customer**: Customers can have multiple rows (one per product)
   - Average: 1.51 rows per customer
   - 1,249 customers have 2+ products
   - 233 customers have 3+ products

2. **Mixed assignments**: **1,989 customers (20%)** have mixed product assignments:
   - Some rows have product names assigned
   - Some rows have missing product names
   - **100% of these customers are activated**
   - **70.6% of these customers have purchases**
   - Row-level analysis would incorrectly exclude these customers!

3. **Correct approach**:
   - Aggregate to customer level first
   - A customer is "activated" if they have ANY product assignment
   - Only exclude customers with **ZERO product assignments** (3,290 customers, 33.05%)
   - Include customers with mixed assignments if they have at least one product

#### Rationale for Exclusion:
- **3,290 customers (33.05%)** have ZERO product assignments (all their rows have missing product names)
- These customers show **0% activation rate** and **0% purchase rate**
- They represent **incomplete or failed signups** that never activated
- Recovering product names from usage data is **ambiguous** and not recommended

#### What We Do:
- ✅ **Exclude** only customers with ZERO product assignments from product-specific analysis
- ✅ **Include** customers with mixed assignments if they have at least one product assigned
- ✅ **Include** for overall signup volume and channel analysis
- ✅ **Include** for usage/engagement analysis where relevant
- ✅ **Document** the methodology transparently in all findings

---

## Dataset Overview

### Customers Dataset
- **Total Unique Customers**: 9,955
- **Total Records**: 15,000 (multiple products per customer possible)
- **Customers with Product Assignment**: 6,665 (67.0%)
- **Customers with ZERO Product Assignments**: 3,290 (33.0%)
- **Customers with Mixed Assignments**: 1,989 (20.0%) - have some products assigned, some missing
- **Date Range**: All signups in June 2021 (single-month cohort)
- **Product Assignments**: QuickBooks (2,015 customers), CreditKarma (1,931 customers), Mint (1,928 customers), TurboTax (1,881 customers)
- **Channels** (at customer level): Direct (2,064), PPC (1,418), Other (1,577), Sales (674), SEO (932)

### Usage Dataset
- **Total Events**: 230,000
- **Date Range**: June 1 - September 28, 2021
- **Unique Customers**: 9,885
- **Action Types**: 7 unique action types (IDs: 1-7)
- **Total Usage Count**: 10.5M+ actions

---

## Customer Funnel & Conversion Metrics

### Overall Funnel (All 9,955 Customers)
```
Total Customers: 9,955 (100%)
  ↓
With Product Assignment: 6,665 (66.95%)
  ↓
Activated:       6,665 (100.00% of those with products)
  ↓
Purchased:       3,988 (59.83% of activated)
  ↓
Cancelled:       2,290 (34.36% of activated)
  ↓
Currently Active: 1,698 (25.48% of activated)
```

### Funnel for Customers with Product Assignment (6,665)
```
Customers with Products: 6,665 (100%)
  ↓
Activated:       6,665 (100.00%)
  ↓
Purchased:       3,988 (59.83%)
  ↓
Cancelled:       2,290 (34.36%)
  ↓
Currently Active: 1,698 (25.48%)
```

### Conversion Rates
- **Overall Signup → Product Assignment**: 66.95% (6,665 / 9,955 customers)
- **Product Assignment → Activation**: 100% (by definition - activation requires product)
- **Activation → Purchase**: 59.83% (3,988 / 6,665 customers) - **CORRECTED** from 56.78% (row-level error)
- **Purchase → Retention**: 65.64% (retention rate = 1 - 34.36% churn = 1,698 / 3,988)

### Time Metrics (Averages)
- **Days to Activation**: 5 days (median: 0 days)
- **Days to Purchase**: 18 days (median: 16 days)
- **Days to Cancel**: 48 days (median: 30 days)

---

## Product Performance Comparison

All products show similar performance metrics with purchase rates around 70%:

| Product | Unique Customers | Purchase Rate | Churn Rate |
|---------|------------------|---------------|------------|
| **QuickBooks** | 2,015 | 69.83% | 43.62% |
| **CreditKarma** | 1,931 | 69.55% | 45.05% |
| **Mint** | 1,928 | 69.29% | 41.49% |
| **TurboTax** | 1,881 | 70.07% | 43.54% |

**Key Insight**: Products show strong purchase conversion rates (~70%) at customer level. Product performance is consistent across all products, suggesting uniform onboarding and conversion processes. Note: These metrics are at customer level - a customer with multiple products appears once per product they're assigned to. Churn rates are high (41-45%), indicating retention opportunities.

---

## Channel Effectiveness Analysis

### Channel Performance Rankings

| Channel | Customers | Purchase Rate | Churn Rate | Ranking |
|---------|-----------|---------------|------------|---------|
| **Sales** | 674 | 66.17% 🥇 | 39.76% | Best purchase rate |
| **Direct** | 2,064 | 64.24% | 43.65% | 2nd |
| **PPC** | 1,418 | 57.69% | 34.91% | 3rd |
| **Other** | 1,577 | 56.12% | 21.24% 🥇 | Lowest churn |
| **SEO** | 932 | 55.04% | 31.22% | 5th |

### Key Channel Insights

1. **Sales Channel**: 
   - Highest purchase rate (66.17%) but high churn (39.76%)
   - Recommendation: Focus on post-purchase retention strategies

2. **Other Channel**: 
   - Lowest churn rate (21.24%) with good purchase rate (56.12%)
   - Recommendation: Study what makes this channel successful for retention and replicate strategies

3. **Direct & PPC**: 
   - Direct has strong purchase rate (64.24%) but higher churn (43.65%)
   - PPC shows balanced performance (57.69% purchase, 34.91% churn) - better retention than Direct
   - Recommendation: Optimize Direct channel retention while scaling PPC investment

---

## Best Product-Channel Combinations

Top 5 combinations by purchase rate:

1. **Mint + Sales**: 68.82% purchase rate
2. **TurboTax + Sales**: 67.82% purchase rate
3. **CreditKarma + Sales**: 64.59% purchase rate
4. **QuickBooks + Sales**: 63.32% purchase rate
5. **CreditKarma + Direct**: 59.91% purchase rate

**Recommendation**: Sales channel consistently performs well across all products. Consider expanding sales channel investment while addressing high churn rates.

---

## Usage Pattern Analysis

### Overall Usage Statistics
- **Customers with Usage Data**: 6,651
- **Average Total Usage per Customer**: 1,058 actions
- **Median Total Usage**: 165 actions (significant right skew)
- **Average Active Days**: 15 days
- **Average Unique Actions Used**: 5 out of 7 available

### High-Value Customers (Top 10%)
- **Count**: 666 customers
- **Average Total Usage**: 7,548 actions (7x average)
- **Average Active Days**: 23.5 days
- **Contribution**: Disproportionate share of total usage

### Usage Distribution
- **25th percentile**: < 27 actions
- **50th percentile (median)**: < 165 actions
- **75th percentile**: < 706 actions
- **Maximum**: Up to 735,059 actions (outliers)

### Usage Trends Over Time
- **June 2021**: 7.08M usage events (peak)
- **July 2021**: 2.73M usage events (-61% decline)
- **August 2021**: 504K usage events (-81% from June)
- **September 2021**: 223K usage events (-56% from August)

**Critical Finding**: Significant drop in usage after initial activation period suggests engagement retention challenges.

---

## Customer Segmentation

| Segment | Count | % of Total | Avg Usage | Avg Active Days |
|---------|-------|------------|-----------|-----------------|
| **Activated - No Purchase** | 3,562 | 43.2% | 5,700 | 16.6 |
| **Active** | 2,372 | 28.8% | 412 | 16.9 |
| **Churned** | 1,854 | 22.5% | 7,775 | 10.8 |
| **Power User** | 449 | 5.4% | 20,706 | 27.3 |
| **Inactive** | 4 | 0.0% | 0 | 0 |

### Key Segment Insights

1. **Activated - No Purchase (43.2%)**: 
   - Largest segment but no revenue contribution
   - High usage suggests engagement but conversion barriers
   - **Action**: Implement targeted conversion campaigns

2. **Power Users (5.4%)**: 
   - Small but highly valuable segment
   - 10x average usage
   - **Action**: Identify characteristics and replicate

3. **Churned (22.5%)**: 
   - Actually had high usage before cancelling
   - **Action**: Investigate why engaged users are cancelling

---

## Action Type Analysis

### Most Used Action Types (Across All Products)
1. **Action Type 5**: 100,969 events (most frequent)
2. **Action Type 7**: 63,238 events (second most)
3. **Action Type 4**: 20,452 events
4. **Action Type 3**: 15,615 events

### Action Type by Product

**CreditKarma**: Action type 7 dominates (794K total usage), followed by type 5 (502K)  
**Mint**: Action type 7 leads (651K), then type 4 (161K)  
**QuickBooks**: Action type 7 leads (486K), then type 5 (138K)  
**TurboTax**: Action type 7 leads (428K), then type 4 (129K)

**Note**: Action types need business context mapping to understand what features they represent. Action type 7 appears to be a core feature across all products.

---

## Temporal Trends

### Weekly Signup Trends (June 2021)
- **Week 1** (June 1-6): 1,652 signups, 56.36% purchase rate
- **Week 2** (June 7-13): 2,001 signups, 56.07% purchase rate
- **Week 3** (June 14-20): 1,844 signups, 58.13% purchase rate ⬆️
- **Week 4** (June 21-27): 1,809 signups, 58.65% purchase rate ⬆️
- **Week 5** (June 28-July 4): 935 signups, 52.73% purchase rate ⬇️

**Observation**: Purchase rates improved in weeks 3-4, then dropped in final week. Possible attribution to campaign optimization or external factors.

### Monthly Cohort (June 2021)
- Single-month cohort study
- 100% activation rate (of customers with product assignment)
- 59.83% purchase rate (customer-level, corrected from row-level analysis)

---

## Customer Engagement Analysis (Post-Activation)

### Overview
Analysis of **6,357 customers** with usage data after activation reveals critical patterns in product engagement and drop-off behavior.

### Engagement Metrics Summary
- **Average total usage per customer**: 1,311 actions (median: 164 - highly skewed)
- **Average active days per customer**: 15.7 days
- **Average unique actions used**: 5.1 out of 7 available
- **Purchased customers**: 3,784 with avg usage of 1,811 actions
- **Non-purchased customers**: 2,573 with avg usage of 576 actions (68% lower)

### What Customers Do After Activation

#### Activity Type Patterns
**Action Type 7** dominates across all products:
- **CreditKarma**: 1,697 customers use it (avg 517 actions/customer) at 40 days post-activation
- **Mint**: 1,246 customers use it (avg 405 actions/customer) at 42 days post-activation
- **QuickBooks**: 1,272 customers use it (avg 307 actions/customer) at 42 days post-activation
- **TurboTax**: 1,181 customers use it (avg 320 actions/customer) at 43 days post-activation

**Action Type 5** is second most popular (most frequent event type):
- Highest adoption (1,939 customers in CreditKarma)
- Used consistently across all products
- Average usage: 28-80 actions per customer depending on product

#### Usage by Time Since Activation

**Critical Finding**: Usage drops dramatically after 30 days for all products.

**CreditKarma**:
- 0-30 days: Avg 835 actions/customer (high engagement)
- 31-60 days: Avg 256 actions/customer (-69% decline)
- 61-90 days: Avg 94 actions/customer (-89% from peak)

**QuickBooks**:
- 0-30 days: Avg 174 actions/customer
- 31-60 days: Avg 132 actions/customer (-24% decline)
- 61-90 days: Avg 129 actions/customer (-26% from peak)
- **30-day drop-off window**: 54.9% of inactive customers stop within 30 days (median: 17 days)

**Mint**:
- 0-30 days: Avg 221 actions/customer
- 31-60 days: Avg 201 actions/customer (-9% decline)
- 61-90 days: Avg 108 actions/customer (-51% from peak)

**TurboTax**:
- 0-30 days: Avg 221 actions/customer
- 31-60 days: Avg 122 actions/customer (-45% decline)
- 61-90 days: Avg 109 actions/customer (-51% from peak)

### When Customers Stop Using Products

#### 30-Day Drop-Off Analysis

All products show similar patterns with **median stop time of 16-20 days**:

| Product | Customers Who Stopped | Median Days Active | % Stopping Within 30 Days |
|---------|----------------------|-------------------|---------------------------|
| **QuickBooks** | 1,150 | 17 days | **54.9%** |
| **TurboTax** | 1,077 | 16 days | **55.5%** |
| **Mint** | 1,097 | 17 days | **55.4%** |
| **CreditKarma** | 1,754 | 20 days | **64.4%** |

#### Drop-Off Distribution
- **0-14 days**: 20-25% of inactive customers stop (early abandonment)
- **15-30 days**: 30-40% of inactive customers stop (critical window - QuickBooks example: 247 customers = 21.5% of inactive)
- **31-60 days**: 15-25% continue to stop (extended drop-off)

**Key Insight**: The 15-30 day window post-activation is critical for all products. For QuickBooks specifically, 54.9% of inactive customers (632 out of 1,150) stop within the first 30 days, with median stop time of 17 days.

---

## Key Business Insights & Opportunities

### North Star Metric: Active Customer Base
**Definition**: Customers who actively use products on a regular basis (active within last 30 days).

**Current State**: Only **25.48% of activated customers** (1,698 out of 6,665) are currently active (purchased and not cancelled).

### Value Proposition Framework
Opportunities are prioritized based on their **impact on Active Customer Base** and **estimated effort**:

**Impact Metrics**:
- **High Impact**: >500 customers potentially added to active base
- **Medium Impact**: 200-500 customers
- **Low Impact**: <200 customers

**Value Drivers**:
1. **Conversion** (Activation → Purchase): Increases active base through revenue commitment
2. **Retention** (Prevent Churn): Maintains active base by reducing drop-offs
3. **Re-engagement** (Reactivate Inactive): Recovers lost active customers
4. **Engagement** (Increase Usage Frequency): Strengthens active base engagement

---

### 🎯 Prioritized Growth Opportunities (Tied to Active Customer Base)

#### Priority 1: 30-Day Engagement Window (HIGH IMPACT - Quick Win)
**Opportunity**: Prevent drop-off during critical 15-30 day window post-activation

**Current State**:
- **54.9% of inactive QuickBooks customers stop within 30 days** (632 customers)
- **64.4% of inactive CreditKarma customers stop within 30 days** (1,130 customers)
- Median stop time: 16-20 days across all products
- Usage drops 45-69% between 0-30 days and 31-60 days windows

**Impact on NSM**:
- **High Impact**: If we reduce 30-day drop-off by 30%, we could add **~1,000 customers** to active base
- **Value**: Prevented churn = maintained active base (no new acquisition needed)

**Specific Actions**:
1. **Day 10-15 Intervention**: Automated re-engagement emails/campaigns at 12 days post-activation (before median drop-off)
   - Target: Customers showing low usage in first week
   - Content: Feature discovery, success stories, usage tips
   
2. **Day 20-25 Milestone Campaign**: Recognize usage milestones at 20 days
   - Gamification: Show progress, unlock features
   - Personalization: Highlight most-used action types (Type 7, Type 5)
   
3. **Action Type 7 Focus**: Since it's dominant across all products, ensure it's:
   - Prominently featured in onboarding
   - Clearly explained in first 7 days
   - Accessible without friction

**Expected Outcome**: Reduce 30-day drop-off from 55-64% to 40-50%, adding **800-1,200 customers** to active base

---

#### Priority 2: Convert Activated Non-Purchasers (HIGH IMPACT - Medium Effort)
**Opportunity**: Convert 2,677 activated customers (40.17%) who haven't purchased

**Current State**:
- 2,677 customers activated but never purchased
- Non-purchasers have 68% lower usage (576 vs 1,811 actions)
- They use fewer unique actions (4.96 vs 5.18)
- Still show engagement but lack conversion trigger

**Impact on NSM**:
- **High Impact**: Converting 30% (803 customers) adds **~800 customers** to active base
- **Value**: Purchased customers have 3x higher usage and better retention

**Specific Actions**:
1. **Usage-Based Conversion Campaigns**:
   - Target customers with 200+ actions but no purchase (engaged but not converted)
   - Trigger: After 50 actions, show value proposition
   - After 150 actions, offer limited-time incentive
   
2. **Action Type 5 Conversion Funnel**:
   - Most frequent action type (1,939 customers in CreditKarma)
   - Use as conversion signal: After 30 Type 5 actions, prompt for upgrade/purchase
   
3. **Free-to-Paid Transition Points**:
   - Identify feature gaps: Customers trying premium features
   - Offer trial periods for premium features
   - Show ROI based on their usage patterns

**Expected Outcome**: Convert 25-30% of activated non-purchasers, adding **700-800 customers** to active base

---

#### Priority 3: Reduce Churn in High-Value Channels (MEDIUM IMPACT - Strategic)
**Opportunity**: Reduce churn in Sales and Direct channels which drive highest purchase rates but highest churn

**Current State**:
- **Sales Channel**: 66.17% purchase rate but 39.76% churn (268 out of 674 customers lost)
- **Direct Channel**: 64.24% purchase rate but 43.65% churn (900 out of 2,064 customers lost)
- **Other Channel**: Only 21.24% churn - best retention model (335 out of 1,577 customers lost)

**Impact on NSM**:
- **Medium-High Impact**: Reducing Sales churn by 10 percentage points (to 30%) retains **66 customers**
- Reducing Direct churn by 10 percentage points (to 34%) retains **200 customers**
- Combined: **~266 customers** added to active base

**Specific Actions**:
1. **Post-Purchase Onboarding for Sales Channel**:
   - Sales customers have highest purchase intent but drop after purchase
   - Implement 30-day post-purchase success program
   - Assign dedicated support for first 30 days
   
2. **Replicate "Other" Channel Success**:
   - Study retention strategies in Other channel (21.24% churn)
   - Identify differences: onboarding sequence, communication style, feature exposure
   - Apply best practices to Sales and Direct channels
   
3. **Early Warning System**:
   - Monitor usage decline in purchased customers
   - If usage drops 50% in first 30 days, trigger intervention
   - Proactive outreach before cancellation

**Expected Outcome**: Reduce churn by 8-10 percentage points in Sales/Direct channels, retaining **200-300 customers** in active base

---

#### Priority 4: Re-engage 60-90 Day Drop-Off Cohort (MEDIUM IMPACT - Long-term)
**Opportunity**: Reactivate customers who stopped using products 31-90 days post-activation

**Current State**:
- 31-60 days: 15-25% of inactive customers continue to drop off
- Usage drops 45-69% in 31-60 day window vs 0-30 days
- These customers had initial engagement but lost momentum

**Impact on NSM**:
- **Medium Impact**: Reactivating 20% of this cohort adds **~400-500 customers** to active base

**Specific Actions**:
1. **60-Day Win-Back Campaign**:
   - Target customers inactive for 30-45 days
   - Offer: "We noticed you haven't used [Product] recently"
   - Highlight: New features, improvements since they last used
   - Incentive: Free month or feature unlock
   
2. **Usage History Reminder**:
   - Show customers their previous usage patterns
   - "You were active 45 days ago, here's what you accomplished"
   - Reconnect with value they were getting
   
3. **Action Type Re-engagement**:
   - Remind customers of their most-used action types
   - "You used Action Type 7 frequently - here's an update on that feature"

**Expected Outcome**: Reactivate 15-20% of 60-90 day drop-offs, adding **300-500 customers** to active base

---

#### Priority 5: Increase Engagement Frequency (LOW-MEDIUM IMPACT - Optimization)
**Opportunity**: Increase usage frequency and feature adoption for existing active customers

**Current State**:
- Average active days: 15.7 days (out of ~90 day window)
- Customers use only 5.1 out of 7 action types
- Purchased customers already show 3x higher usage (1,811 vs 576)

**Impact on NSM**:
- **Low-Medium Impact**: Increasing engagement doesn't add new customers but strengthens existing base
- Reduces risk of churn for current active customers

**Specific Actions**:
1. **Feature Discovery Campaigns**:
   - Target customers using <5 action types
   - Recommend underused actions based on their behavior
   - Weekly feature highlights
   
2. **Usage Milestones**:
   - Celebrate usage milestones (100, 500, 1,000 actions)
   - Unlock advanced features based on usage
   - Create habit-forming patterns

**Expected Outcome**: Increase engagement frequency by 20%, strengthening active base retention

---

### 📊 Opportunity Prioritization Matrix

| Opportunity | Impact on Active Base | Effort | Priority | Customers Impacted |
|------------|---------------------|--------|----------|-------------------|
| **30-Day Engagement Window** | High (1,000+) | Low | **P1** | 1,500-2,000 at risk |
| **Convert Non-Purchasers** | High (800+) | Medium | **P2** | 2,677 eligible |
| **Reduce Sales/Direct Churn** | Medium (266) | Medium | **P3** | 1,168 at risk |
| **Re-engage 60-90 Day Cohort** | Medium (400) | High | **P4** | 2,000+ eligible |
| **Increase Engagement Frequency** | Low-Medium | Low | **P5** | Current active base |

### 📈 Expected Cumulative Impact on Active Customer Base

**Current Active Base**: 1,698 customers (25.48%)

**Projected Improvements** (if all priorities executed):
- Priority 1: +1,000 customers (30-day drop-off prevention)
- Priority 2: +800 customers (conversion)
- Priority 3: +266 customers (churn reduction)
- Priority 4: +400 customers (re-engagement)
- **Total Potential**: +2,466 customers

**New Active Base**: ~4,164 customers (62.5% of activated customers - 2.45x increase)

---

### 💎 Product-Specific Recommendations

#### QuickBooks (30-Day Product Focus)
- **Critical Window**: 54.9% stop within 30 days (median: 17 days)
- **Specific Action**: Implement "QuickBooks 17-Day Challenge"
  - Day 17 check-in with personalized coaching
  - Show value delivered in first 17 days
  - Address common pain points at this stage
- **Expected**: Reduce 30-day drop-off by 25%, adding 150 QuickBooks customers to active base

#### CreditKarma (Highest Drop-Off)
- **Critical Window**: 64.4% stop within 30 days (highest among all products)
- **Specific Action**: Earlier intervention at Day 10-12
  - More aggressive re-engagement needed
  - Action Type 7 focus (most used - 1,697 customers)
- **Expected**: Reduce drop-off by 30%, adding 339 CreditKarma customers to active base

---

### 📈 Product Strategy Insights

1. **Action Type 7 Dominance**: Most critical feature across all products
   - Ensure prominent placement in onboarding
   - Make it accessible without barriers
   - Use as engagement indicator

2. **Action Type 5 Frequency**: Most frequent event type
   - Use as conversion signal (30+ events = purchase opportunity)
   - Optimize this action for speed and ease

3. **Product Parity**: All products show similar patterns
   - Standardize 30-day engagement program across products
   - Share best practices (e.g., Other channel retention strategies)

---

## Data Quality Notes & Assumptions

### Data Quality Issues

1. **Product Name Missing**: 33.05% of customers (3,290 customers) have ZERO product assignments
   - **Impact**: Excluded from product-specific analysis
   - **Note**: 1,989 customers (20%) have mixed assignments (some products assigned, some missing) - these ARE included
   - **Reason**: Customers with zero product assignments represent non-activated signups with unclear product intent

2. **Purchase Date Missing**: 68.8% missing (10,321 records)
   - **Impact**: Some products may not require purchase (free tiers, different business models)
   - **Assumption**: Purchase date applies to subscription/paid products

3. **Usage Product Name Missing**: 11.5% missing (26,455 events)
   - **Impact**: Some usage events cannot be attributed to specific products
   - **Note**: Does not significantly impact analysis

4. **Customer Gap**: 70 customers signed up but have no usage data
   - **Impact**: Minimal, represents <1% of dataset

### Business Assumptions

1. **Missing Product Names**: Only customers with ZERO product assignments are excluded
   - Customers with mixed assignments (some products assigned, some missing) are INCLUDED
   - Customers may have signed up generally without specific product intent
   - Usage data may not reflect signup intent (recovery not recommended)
   - **Critical**: Analysis is at CUSTOMER level, not row level

2. **Single-Month Cohort**: All signups in June 2021
   - Represents a focused cohort study
   - Enables clean cohort analysis

3. **Cancel Date**: Only applies to subscription products
   - Not all products are subscription-based
   - Free products may not have cancellation concept

4. **Usage Data**: Represents post-activation engagement
   - Usage occurs after product activation
   - Usage patterns indicate product adoption and value realization

5. **Action Types**: Require business context mapping
   - Action type IDs (1-7) need feature mapping
   - Critical for understanding product usage patterns

---

## Recommendations Summary

### Immediate Actions (Quick Wins)

1. ✅ **Launch re-engagement campaigns** for July/August cohorts (address usage decline)
2. ✅ **Implement conversion campaigns** for activated non-purchasers (43% opportunity)
3. ✅ **Study "Other" channel** retention strategies and replicate
4. ✅ **Analyze churned high-users** to understand cancellation drivers

### Strategic Initiatives (Long-term)

1. 📊 **Channel optimization**: Reduce Sales channel churn while maintaining purchase rate
2. 📈 **Scale PPC/SEO**: Balanced performance suggests scalable growth opportunity
3. 💎 **Power user program**: Identify and replicate power user characteristics
4. 🔍 **Product differentiation**: Test strategies to break product parity and optimize individually
5. 📱 **Usage retention**: Address 70% usage decline through onboarding and habit formation

### Analysis & Investigation Needs

1. **Action type mapping**: Map action type IDs to actual product features
2. **Churn analysis**: Deep dive into why engaged users cancel
3. **Conversion barriers**: Identify why 43% of activated users don't purchase
4. **Channel attribution**: Understand what makes "Other" channel successful for retention

---

## Metrics to Track Going Forward

### Funnel Metrics
- Overall signup to purchase rate (current: 40.05%, target: improve)
- Activation to purchase rate (current: 59.83%, target: improve to 65%+)
- Purchase to retention rate (current: 65.64%, target: improve to 75%+)

### Channel Metrics
- Channel-specific purchase rates
- Channel-specific churn rates
- Channel efficiency (purchase rate / churn rate ratio)

### Engagement Metrics
- Monthly active users (address 70% decline)
- Usage frequency per customer
- Feature adoption rates (after action type mapping)

### Product Metrics
- Product-specific conversion rates
- Product-specific retention rates
- Product-channel combination performance

---

## Conclusion

The analysis reveals significant opportunities for growth, particularly in:
1. **Converting activated users** (40% gap - 2,677 customers not purchasing)
2. **Reducing churn** (34% churn rate - 2,290 customers cancelling)
3. **Maintaining engagement** (70% usage decline from June to July)

The data shows strong initial activation and purchase conversion (59.83%), but challenges in retention (34.36% churn) and long-term engagement. The customer-level analysis ensures accurate insights by correctly including customers with mixed product assignments while maintaining transparency about data limitations.

**Methodology Note**: This analysis aggregates to customer level first, then only excludes customers with ZERO product assignments. This corrects for the previous row-level analysis that incorrectly excluded 1,989 customers with mixed assignments.

**Next Steps**: Prioritize re-engagement campaigns, conversion optimization, and churn reduction initiatives based on the insights above.

---

*Analysis Period: June - September 2021*  
*Analysis Date: 2024*  
*Dataset: 9,955 unique customers (15,000 customer-product records), 230,000 usage events*  
*Methodology: Customer-level aggregation (corrected from row-level analysis)*
