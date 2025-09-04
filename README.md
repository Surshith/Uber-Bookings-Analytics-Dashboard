# Uber-Bookings-Analytics-Dashboard

An interactive **Power BI** dashboard analyzing Uber NCR ride bookings to surface insights on **trip success rate**, **revenue trends**, **customer behavior**, and **operational efficiency**.

## 🧰 Tools & Frameworks
- Microsoft **Power BI**
- **DAX** (Data Analysis Expressions)
- **Power Query**
- Source data: CSV/Excel

## ✨ Key Features
- **Completion rate by vehicle type** (Completed ÷ (Completed + Incomplete))
- **Hourly heatmap**: Day-of-week × hour to spot peak activity
- **Trips over time**: daily/weekly/monthly trends
- **Rate per km** by vehicle type
- **Top customers** by booking value (Top N)
- **Trip duration bins** (0–45 grouped in 5-minute buckets)
- **KPI cards** for core metrics (rides/day, completion %, etc.)

## 📂 Project Structure (suggested)
```
uber-bookings-analytics-dashboard/
├─ README.md
├─ Uber Bookings Analytics Dashboard.pbix        # Add your PBIX here
├─ data/
│  └─ ncr_ride_bookings_sample.csv               # (optional) share a safe sample only
└─ images/
   ├─ dashboard.png
   ├─ heatmap.png
   └─ trends.png
```

> ⚠️ **Data privacy:** If your dataset contains sensitive information, upload an **anonymized sample** or remove PII before sharing publicly.

## 🧮 Core DAX (examples)

```DAX
-- Completed vs Total rides
Completed Rides =
CALCULATE ( COUNTROWS ( bookings ), bookings[Booking Status] = "Completed" )

Total Rides =
CALCULATE ( COUNTROWS ( bookings ), bookings[Booking Status] IN { "Completed", "Incomplete" } )

Completion Rate =
DIVIDE ( [Completed Rides], [Total Rides] )

-- Rate per km (overall, works with Vehicle Type in context)
RatePerKm =
DIVIDE ( SUM ( bookings[Booking Value] ), SUM ( bookings[Ride Distance] ) )

-- Average rides per day (Completed + Incomplete)
Avg Rides per Day =
DIVIDE (
    [Total Rides],
    DISTINCTCOUNT ( bookings[Date] )
)

-- Time-slot label (Power Query custom column in M)
-- if [Time] >= #time(0,0,0) and [Time] <= #time(5,59,59) then "00:00-05:59"
-- else if [Time] >= #time(6,0,0) and [Time] <= #time(11,59,59) then "06:00-11:59"
-- else if [Time] >= #time(12,0,0) and [Time] <= #time(17,59,59) then "12:00-17:59"
-- else if [Time] >= #time(18,0,0) and [Time] <= #time(20,59,59) then "18:00-20:59"
-- else "21:00-23:59"
```

## 🖼️ Screenshots
Add PNGs to `/images` and reference them here:

- **Dashboard Overview**  
  ![Dashboard](images/dashboard.png)

- **Hourly Heatmap**  
  ![Heatmap](images/heatmap.png)

- **Trends Over Time**  
  ![Trends](images/trends.png)

## 🚀 How to Run
1. Download this repository (or clone).
2. Open **`Uber Bookings Analytics Dashboard.pbix`** in Power BI Desktop.
3. If prompted, update the **data source** path to your local CSV/Excel.
4. Click **Refresh** to populate visuals.

## 📝 Resume Bullets (use any/all)
- Built an interactive Power BI dashboard to analyze large-scale ride booking data, enabling insights on trip success rate, revenue trends, and customer behavior.
- Created custom DAX measures and KPIs using heatmaps, column charts, and time-based analyses.
- Delivered actionable insights such as peak demand hours, top customers by booking value, and outlier trips, improving operational decision-making.

## 📜 License
MIT — see LICENSE for details.
