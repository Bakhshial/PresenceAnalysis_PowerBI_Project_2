# PresenceAnalysis_PowerBI_Project_2

## Problem Statement
Q1: Working Preference of People
Determine whether people prefer to work from home (WFH), on-site, or a mix (e.g., Monday at home and other days in the office).
Q2: Sick Leave Percentage
Calculate the percentage of sick leave taken by employees.
#### Project Overview
This project aims to analyze employee working preferences and sick leave patterns using data visualization and DAX calculations in Power BI. The analysis involves gathering and transforming data, creating measures, and generating insightful visualizations.

## Steps Involved
### 1. Gathering and Transforming Data
Combining Multiple Sheets: Data from various sheets are consolidated into a single dataset for a unified analysis.
### 2. Creating Matrices Using DAX

    Total Working Days: Calculates the total number of working days by excluding weekends (WO) and holidays (HO).
    
     DAX
    Copy code
    Total Working Days = 
    VAR totaldays = COUNT('Combined Data'[Value])
    VAR nonworkingdays = CALCULATE(COUNT('Combined Data'[Value]), 'Combined Data'[Value] IN {"WO", "HO"})
    RETURN
    totaldays - nonworkingdays
    Results: 4439 days
    
    
    Present Days: Calculates the total number of days employees were present, including both office and WFH days.
    
    
    DAX
    Copy code
    Present Days = 
    VAR Presentday = CALCULATE(COUNT('Combined Data'[Value]), 'Combined Data'[Value] = "P")
    RETURN
    Presentday + [WFH count]
    Results: 4064 days
    
    
    Presence Percentage: Determines the percentage of days employees were present.
    
    
    DAX
    Copy code
    Presence % = DIVIDE([Present Days], 'measure table'[Total Working Days], 0)
    Results: 90.70%
    
    
    Working from Home Percentage: Calculates the percentage of WFH days relative to the total present days.
    
    
    DAX
    Copy code
    Working from Home % = DIVIDE([WFH count], [Present Days], 0)
    Results: 14.20%
    
    
    Sick Leave Percentage: Calculates the percentage of sick leave days relative to the total working days.
    
    
    DAX
    Copy code
    Sick leave % = DIVIDE([SL count], [Total Working Days], 0)
    Results: 1.68%
    
    
  ### 3. Creating Columns
    
    WFH Count: Assigns values based on the type of work-from-home (full or half day).
    
    
    DAX
    Copy code
    WFH Count = SWITCH(TRUE(),
    'Combined Data'[Value] = "WFH", 1,
    'Combined Data'[Value] = "HWFH", 0.5,
    0)
    
    Month: Extracts the start date of each month for time-based analysis.
    
    
    DAX
    Copy code
    Month = STARTOFMONTH('Combined Data'[Date])
    
    SL Count: Assigns values based on the type of sick leave (full or half day).
    
    
    DAX
    Copy code
    SL Count = SWITCH(TRUE(),
    'Combined Data'[Value] = "SL", 1,
    'Combined Data'[Value] = "HSL", 0.5,
    0)

### Visualizations
#### Line Charts
Presence %, Sick Leave %, and Working from Home % by Month and Days: Displays trends in presence, sick leave, and WFH percentages over time, providing insights into seasonal patterns and fluctuations.
#### Matrices
Presence %, Sick Leave %, and Working from Home % by Name: Breaks down key metrics by individual employees to identify patterns and outliers.
Presence Days, Total Sit Days, Total WFH Days: Summarizes the total number of days present, on-site, and working from home for each employee, offering a comprehensive view of attendance and work preferences.
#### Day-wise Percentages
Presence %, Sick Leave %, and Working from Home % by Day: Provides detailed analysis of daily patterns, helping to identify specific days of the week with higher or lower percentages of presence, sick leave, and WFH.
#### Results and Insights
Presence %: 90.70% of the total working days are accounted for by employee presence.
Working from Home %: 14.20% of the present days are work-from-home days.
Sick Leave %: 1.68% of the total working days are taken as sick leave.
#### Conclusion
This analysis provides a comprehensive understanding of employee work preferences and sick leave patterns, aiding in strategic decision-making for workplace management.
