
# 📒 DAX Measures Notebook — Facebook Ads Insights Dashboard

This notebook documents all the **DAX calculations** created inside the Power BI file for  
**Task 2 — Social Media Campaign Performance Tracker (Future Interns Internship).**

---

## **📊 Base Measures**

```DAX
Total Clicks =
COALESCE( SUM(data[clicks]), 0 )

Total Conversions =
COALESCE( SUM(data[conversions]), 0 )

Total Impressions =
COALESCE( SUM(data[impressions]), 0 )

Total Spend =
COALESCE( SUM(data[spent]), 0 )
````

---

## **📈 Performance Measures**

```DAX
CTR =
DIVIDE( [Total Clicks], [Total Impressions], 0 )

Conversion Rate =
DIVIDE( [Total Conversions], [Total Clicks], 0 )

CPC =
DIVIDE( [Total Spend], [Total Clicks], 0 )

CPM =
DIVIDE( [Total Spend], [Total Impressions], 0 ) * 1000
```

---

## **💰 Cost & ROI Measures (Optional)**

```DAX
Cost per Conversion =
DIVIDE( [Total Spend], [Total Conversions], BLANK() )

-- (If revenue column exists)
Total Revenue =
COALESCE( SUM(data[revenue]), 0 )

ROAS =
DIVIDE( [Total Revenue], [Total Spend], 0 )
```

---

## **📅 Date Table**

```DAX
Date Table =
VAR minDate = MINX( ALL(data), data[reporting_start] )
VAR maxDate = MAXX( ALL(data), data[reporting_start] )
RETURN
ADDCOLUMNS(
   CALENDAR( minDate, maxDate ),
   "Year", YEAR([Date]),
   "MonthNumber", MONTH([Date]),
   "MonthName", FORMAT([Date], "MMM"),
   "Quarter", "Q" & FORMAT([Date], "Q"),
   "YearMonthKey", FORMAT([Date], "YYYY-MM"),
   "MonthYear", FORMAT([Date], "MMM YYYY")
)
```

---

🧠 **Notes**

* Link `Date Table[Date]` → `data[reporting_start]` in **Model view**.
* Then go to **Modeling → Mark as Date Table → select Date column.**
* Use *Percentage format (2 decimals)* for CTR & Conversion Rate.
* Use *Currency format (₹ or $)* for Spend, CPC & CPM.
* Use `BLANK()` instead of `0` where appropriate to keep visuals clean.

```

---

