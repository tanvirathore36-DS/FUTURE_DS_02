# 📒 DAX Measures Notebook — Facebook Ads Insights Dashboard

This notebook documents all the **DAX calculations and supporting tables** created inside the Power BI file for **Task 2 — Social Media Campaign Performance Tracker (Future Interns Internship).**

---

## 📊 Base Measures

```DAX
Total Clicks =
COALESCE( SUM(data[clicks]), 0 )

Total Conversions =
COALESCE( SUM(data[conversions]), 0 )

Total Impressions =
COALESCE( SUM(data[impressions]), 0 )

Total Spend =
COALESCE( SUM(data[spent]), 0 )

---

## **📈 Performance Measures**

CTR =
DIVIDE( [Total Clicks], [Total Impressions], 0 )

Conversion Rate =
DIVIDE( [Total Conversions], [Total Clicks], 0 )

CPC =
DIVIDE( [Total Spend], [Total Clicks], 0 )

CPM =
DIVIDE( [Total Spend], [Total Impressions], 0 ) * 1000

---

## **📅 Date Table** 

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

