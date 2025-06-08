# ✈️ Airline Flight Delay & Cancellation Analysis

## 📌 Problem Statement

Flight delays and cancellations create a negative impact on passenger satisfaction, airline efficiency, and airport operations. The aim of this project is to analyse flight delay and cancellation patterns using SQL and visualize key insights using Power BI. This helps in identifying areas of improvement for airlines and making data-driven operational decisions.



## 🗃️ Dataset Overview

I used mock flight data stored in a PostgreSQL database. The data was exported to `.csv` files and used in Power BI for visualization.

### 📂 Tables:

1. **flights.csv**
   - `flight_id`
   - `airline_id`
   - `origin_airport_id`
   - `destination_airport_id`
   - `scheduled_departure` (datetime)
   - `actual_departure` (datetime)
   - `delay_minutes`
   - `is_cancelled`

2. **airline.csv**
   - `airline_id`
   - `airline_name`

3. **airports.csv**
   - `airport_id`
   - `airport_name`
   - `city`
   - `country`

---

## 🔍 Analysis Goals

- Calculate average delays by airline
- Identify cancellation trends
- Compare destination airport performance
- Analyse delays by time of day
- Create interactive dashboards in Power BI

---

## 💾 SQL Queries Used

### ✅ 1. Average Delay by Airline
```
SELECT a.airline_name,
       ROUND(AVG(f.delay_minutes)::NUMERIC, 1) AS avg_delay
FROM flights f
JOIN airline a ON f.airline_id = a.airline_id
WHERE f.is_cancelled = FALSE
GROUP BY a.airline_name;

### ✅ 2. Cancelled Flights by Airline

SELECT a.airline_name,
       COUNT(*) AS cancelled_flights
FROM flights f
JOIN airline a ON f.airline_id = a.airline_id
WHERE f.is_cancelled = TRUE
GROUP BY a.airline_name;

### ✅ 3. Delays by Destination Airport

SELECT ap.airport_name,
       ROUND(AVG(f.delay_minutes)::NUMERIC, 1) AS avg_arrival_delay
FROM flights f
JOIN airports ap ON f.destination_airport_id = ap.airport_id
WHERE f.is_cancelled = FALSE
GROUP BY ap.airport_name
ORDER BY avg_arrival_delay DESC;

### ✅ 4. Delay by Hour of Departure

SELECT EXTRACT(HOUR FROM f.scheduled_departure) AS hour,
       ROUND(AVG(f.delay_minutes)::NUMERIC, 1) AS avg_delay
FROM flights f
WHERE f.is_cancelled = FALSE
GROUP BY hour
ORDER BY hour;

📊 Power BI Dashboard

Visuals Created:
  
 ->Bar Chart: Average Delay per Airline

 ->Pie Chart: % of Cancelled Flights per Airline

 ->Line Chart: Delay Trend by Departure Hour

 ->Map: Delay by Destination Airport

 ->Slicers: Airline, Airport, Date Range

🔎 Key Insights
  
 ->IndiGo had the highest average delay.

 ->Most cancellations occurred with SpiceJet.

 ->Delays were highest during evening hours (5–9 PM).

 ->Delhi and Mumbai airports saw the highest inbound delays.

### 📁 Project Structure

airline-delay-analysis/
│
├── data/
│   ├── flights.csv
│   ├── airline.csv
│   └── airport.csv
│
├── dashboard/
│   └── flight_dashboard.pbix
│
├── queries.sql
├── flight_delay_report.md
└── Airline_flight_data_report.md

🚀 Conclusion
This project demonstrates how SQL and Power BI can work together for real-world business analytics. By analyzing flight delays and cancellations, we gained useful operational insights that could help improve airline services and reduce passenger frustration.

🔗 Author
Sheela Devi
3rd Year | Biomedical Engineering
Passionate about data, dashboards, and databases 💻📊💡
