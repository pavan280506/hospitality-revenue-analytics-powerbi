# Hotel Booking Demand Dataset  
**Version:** 1.0  
**Last Updated:** 2026  
**Data Classification:** Public (CC BY 4.0)

---

## 1. Introduction

This dataset contains structured booking transaction records for two hotel categories:
- Resort Hotel  
- City Hotel  

Each record represents a single reservation and captures booking behavior, guest attributes, stay details, pricing metrics, and final reservation outcomes.

The dataset is anonymized and does not contain personally identifiable information (PII).

---

## 2. Dataset Overview

| Attribute | Value |
|------------|--------|
| Total Records | 119,390 |
| Total Features | 32 |
| Time Period Covered | 2015 – 2017 |
| Data Format | CSV |
| Granularity | Booking-Level |
| Hotels Included | Resort Hotel, City Hotel |

---

## 3. Data Schema Summary

The dataset consists of the following feature groups:

### 3.1 Hotel Information
- `hotel`
- `is_canceled`

### 3.2 Booking Timeline
- `lead_time`
- `arrival_date_year`
- `arrival_date_month`
- `arrival_date_week_number`
- `arrival_date_day_of_month`

### 3.3 Stay Information
- `stays_in_weekend_nights`
- `stays_in_week_nights`

### 3.4 Guest Profile
- `adults`
- `children`
- `babies`
- `country`
- `is_repeated_guest`
- `previous_cancellations`
- `previous_bookings_not_canceled`

### 3.5 Booking Channel & Commercial Details
- `meal`
- `market_segment`
- `distribution_channel`
- `deposit_type`
- `agent`
- `company`
- `customer_type`

### 3.6 Room & Reservation Attributes
- `reserved_room_type`
- `assigned_room_type`
- `booking_changes`
- `days_in_waiting_list`

### 3.7 Financial Metrics
- `adr` (Average Daily Rate)
- `required_car_parking_spaces`
- `total_of_special_requests`

### 3.8 Reservation Status
- `reservation_status`
- `reservation_status_date`

---

## 4. Data Characteristics

- Data Types: Integer, Categorical (String), Decimal, Date
- Categorical values stored as text labels
- Country codes follow ISO standards
- Room types and commercial identifiers are anonymized
- Reservation outcomes include: Canceled, Check-Out, No-Show
- ADR represents average price per room per night

---

## 5. Data Governance

- All personally identifiable information (PII) has been removed.
- Dataset is anonymized for research and analytical purposes.
- No sensitive financial or personal identifiers are included.
- License: Creative Commons Attribution 4.0 International (CC BY 4.0)

---

## 6. Source Reference

Antonio, N., Almeida, A., & Nunes, L. (2019).  
*Hotel Booking Demand Datasets.*  
Data in Brief, Volume 22.

---

## 7. Disclaimer

This dataset is provided for analytical and research purposes.  
The data reflects historical booking transactions and should not be interpreted as real-time operational data.

---