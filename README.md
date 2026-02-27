# 🏨 Hotel Analytics & Revenue Optimization Platform

An end-to-end Business Intelligence solution designed to transform hotel booking data into strategic insights for occupancy management, revenue optimization, guest segmentation, pricing strategy, and demand forecasting.

This project demonstrates expertise in enterprise data modeling, KPI engineering, advanced DAX development, and predictive analytics using Power BI and Python (Prophet).

---

# 1. Executive Overview

The objective of this initiative is to design a scalable and performance-optimized hotel analytics ecosystem that enables leadership teams and revenue managers to:

- Monitor occupancy and revenue performance in real time  
- Analyze guest behavior and loyalty trends  
- Optimize pricing strategies dynamically  
- Identify upsell and cross-sell opportunities  
- Forecast future booking demand  

The solution is structured into modular analytical components built on a robust star schema architecture.

---

# 2. Data Architecture & Modeling

## 2.1 Star Schema Design

The analytical model follows a clean star schema to ensure:

- Accurate aggregations  
- Optimized query performance  
- Scalable extension across properties and geographies  

### Fact Table
**Raw_Fact**  
Booking-level transactional data including revenue, ADR, cancellations, stay duration, and booking channel information.

### Dimension Tables
- Date_Dimension  
- Hotel_Dimension  
- Room_Dimension  
- Customer_Dimension  

---

## 2.2 Data Engineering & Feature Creation

Key transformations and enhancements:

- Generated surrogate keys: `booking_id`, `hotel_id`, `room_id`, `customer_id`
- Derived analytical columns:
  - `arrival_date`
  - `date_key`
  - `total_nights`
  - `stay_type`
  - `Revenue`
  - `cost`
  - `discount`
  - `room_category`
- Revenue normalized to 0 for canceled bookings
- Meal plans mapped to cost structures
- Market segments mapped to discount logic
- Room types categorized into logical tiers
- High-null fields removed
- Referential integrity validated via one-to-many relationships

The model supports drilldowns, segmentation, and enterprise-grade reporting.

---

# 3. Occupancy & Revenue Performance Module

This module evaluates hotel performance using hospitality industry-standard KPIs.

## 3.1 Core Measures

### Total Revenue
```dax
Total Revenue =
SUM(Raw_Fact[Revenue])
```

### Total Bookings (Confirmed)
```dax
Total Bookings =
CALCULATE(
    COUNT(Raw_Fact[booking_id]),
    Raw_Fact[is_canceled] = 0
)
```

### ADR (Average Daily Rate)
Weighted ADR based on occupied room nights:

```dax
ADR =
DIVIDE(
    [Total Revenue],
    CALCULATE(
        SUM(Raw_Fact[total_nights]),
        Raw_Fact[is_canceled] = 0
    )
)
```

### Occupancy %
```dax
Occupied Room Nights =
CALCULATE(
    SUM(Raw_Fact[total_nights]),
    Raw_Fact[is_canceled] = 0
)

Available Room Nights =
COUNTROWS('Room_Dimension') *
COUNTROWS('Date_Dimension')

Occupancy % =
DIVIDE(
    [Occupied Room Nights],
    [Available Room Nights]
)
```

### RevPAR
```dax
RevPAR =
DIVIDE(
    [Total Revenue],
    [Available Room Nights]
)
```

## 3.2 Analytical Insights

- Peak vs off-peak demand identification  
- Channel performance comparison (Direct vs OTA)  
- Revenue impact of cancellations  
- Seasonal occupancy patterns  
- Pricing efficiency evaluation  

---

# 4. Guest Intelligence Module

Focused on behavioral segmentation and revenue contribution analysis.

## 4.1 Guest Classification Logic
```dax
Guest Type =
SWITCH(TRUE(),
    Raw_Fact[children] > 0 || Raw_Fact[babies] > 0, "Family",
    Raw_Fact[adults] = 1 && Raw_Fact[children] = 0, "Solo",
    Raw_Fact[market_segment] = "Corporate", "Business",
    Raw_Fact[adults] = 2 && Raw_Fact[children] = 0, "Couple",
    "Other"
)
```

## 4.2 Loyalty Segmentation
```dax
Loyalty Segment =
IF(
    Raw_Fact[is_repeated_guest] = 1 ||
    Raw_Fact[previous_bookings_not_canceled] > 0,
    "Loyal Guest",
    "First-time Guest"
)
```

## 4.3 High-Spender Identification
```dax
High Spender Status =
VAR RevenueThreshold =
    PERCENTILEX.INC(
        ALL(Raw_Fact),
        Raw_Fact[Revenue],
        0.9
    )
RETURN
IF(
    MAX(Raw_Fact[Revenue]) >= RevenueThreshold,
    "High Spender",
    "Standard"
)
```

## 4.4 Business Applications

- Revenue contribution by country and segment  
- Booking source profitability  
- VIP identification  
- Loyalty-driven targeting strategies  
- Cancellation behavior analysis  

---

# 5. Forecasting & Predictive Analytics

Demand forecasting implemented using Python (Prophet) integrated with Power BI.

## 5.1 Workflow

1. Generated month-end aggregation key  
2. Aggregated monthly booking counts  
3. Exported data for model training  
4. Trained Prophet model (24-month forecast horizon)  
5. Reintegrated forecast output into dashboard  

## 5.2 Deliverables

- Actual vs forecast comparison  
- Confidence interval visualization  
- Peak demand projection  
- Seasonal trend extrapolation  

## 5.3 Business Impact

- Capacity planning  
- Workforce optimization  
- Campaign scheduling  
- Long-term pricing calibration  

---

# 6. Revenue Strategy & Optimization Dashboard

This module supports data-driven pricing and upsell optimization.

## 6.1 Upsell Revenue Estimation
```dax
Estimated Upsell Revenue =
VAR MealUpsell = [Meal Upsell Revenue]
VAR SpecialRequestsUpsell =
    SUMX(
        Raw_Fact,
        Raw_Fact[total_of_special_requests] * 15
    )
RETURN
MealUpsell + SpecialRequestsUpsell
```

## 6.2 Dynamic Pricing Logic
```dax
Optimal Price Point =
VAR CurrentOccupancy = [Occupancy %]
VAR CurrentADR = [ADR]
VAR PriceAdjustment =
    SWITCH(TRUE(),
        CurrentOccupancy >= 85, 1.15,
        CurrentOccupancy >= 70, 1.05,
        CurrentOccupancy >= 50, 1.00,
        CurrentOccupancy >= 40, 0.95,
        0.85
    )
RETURN
CurrentADR * PriceAdjustment
```

## 6.3 Strategic Capabilities

- Season-based pricing recommendations  
- Segment profitability analysis  
- Discount performance tracking  
- Upsell opportunity quantification  
- Year-over-Year growth monitoring  

---

# 7. Technology Stack

- Power BI Desktop  
- Power Query  
- DAX (Data Analysis Expressions)  
- Python  
- Prophet (Time-Series Forecasting)  
- CSV-based data integration  

---

# 8. Business Value Delivered

This platform enables:

- KPI-driven revenue management  
- Operational performance monitoring  
- Strategic pricing optimization  
- Advanced guest segmentation  
- Forecast-informed decision-making  
- Scalable deployment across hotel chains  

---

# 9. Conclusion

The Hotel Analytics & Revenue Optimization Platform integrates structured data modeling, business intelligence, and predictive forecasting into a unified decision-support system.

It reflects enterprise-level BI implementation standards and demonstrates end-to-end capability in data engineering, analytical modeling, and strategic revenue intelligence.

---
