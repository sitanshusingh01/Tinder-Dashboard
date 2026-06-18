# Tinder User Behavior Analysis Dashboard

A Power BI project that digs into how real people actually use a dating app. Not just the swipe numbers, but the full story from first swipe to relationship.

## About This Project

I built this because I wanted to understand something that bothered me. Dating apps report millions of matches but nobody talks about how few of those lead to anything real. This dashboard answers that question with data.

It covers 5000 simulated users across 29 cities worldwide. The dataset is designed to reflect actual behavioral patterns you would see on a platform like Tinder. Gender split, peak activity hours, distance preferences, and funnel drop offs are all modeled on documented behavioral research.



## Dataset

File: Users_Data.csv

The dataset has 5000 rows and 14 columns.

Column list:

User ID, Gender, Age, City, Country, Swipe Count Per Day, Matches, Conversations, Meetings, Relationships, Active Hour, Day of Week, Distance Miles, Session Time Minutes

A calculated column called Time Bucket is added inside Power BI using DAX. It converts the hour number into Morning, Afternoon, Evening, or Night.

Key design choices in the data:

75 percent of users are male and 25 percent are female. This reflects real platform demographics.

Activity peaks between hours 18 and 21. Evening hours dominate usage the same way they do on real apps.

60 percent of users are within 10 miles. Proximity matters more than people think.

Match rates are set between 5 and 15 percent of swipes. Conversation rates, meeting rates, and relationship rates all cascade downward from there.

---

## Steps to Build the Dashboard in Power BI

Step 1 Load the data

Open Power BI Desktop. Click Get Data then choose Text or CSV. Select Users_Data.csv from the dataset folder. Click Load.

Step 2 Add the calculated column

In the Data view, click on the Users_Data table. Go to the Modeling tab and click New Column. Paste the Time Bucket DAX formula from the DAX Measures file.

Step 3 Create all measures

In the Modeling tab click New Measure. Add each measure from the DAX Measures file one by one. Organize them in a dedicated Measures table if you prefer clean structure.

Step 4 Build the visuals

Page 1 is the executive overview. Use card visuals for KPI numbers. Use a donut chart for gender split. Use a bar chart for activity by hour. Use another bar chart or donut for time bucket distribution.

Page 2 covers user behavior. Build a matrix visual for the heatmap with day on rows and hour on columns. Use a grouped bar chart to compare male and female engagement.

Page 3 is the funnel. Use a funnel visual or a custom bar chart to show the drop at each stage from swipes to relationships.

Page 4 is proximity. Use a pie chart for the distance split. Use a map visual with city on the location field. Add a card showing the proximity percentage.

Page 5 is psychology insights. Use a line chart for engagement over session time. Add text box visuals with the insight copy you want to highlight.

Step 5 Style the dashboard

Use the red and orange color palette. Set background colors to dark tones. Add a text box in the bottom right corner that says Created by Sitanshu Singh.

---

## Key Insights from the Data

Gender imbalance has a real effect. With 75 percent male users, women receive more matches per swipe than men. This creates different experiences for each gender. Men swipe more broadly and get fewer matches per swipe. Women get more matches but face message overload.

Evening engagement is not accidental. The spike between 6 PM and 9 PM happens because people are done with work, tired, and looking for social stimulation. The app is most compelling when the brain is slightly fatigued and seeking low effort reward.

The funnel collapses fast. Over 553 thousand swipes produced only 288 relationships. That is a 0.05 percent conversion from swipe to relationship. The app is very good at creating matches and very poor at creating real outcomes.

Proximity drives outcomes. Almost 60 percent of interactions happen within 10 miles. Users who match with someone nearby are far more likely to have a conversation that leads somewhere. Distance is a friction multiplier.

---

## How to Use With Your Own Data

Replace Users_Data.csv with your own dataset. Make sure the column names match exactly. Once you refresh the data in Power BI, every visual and every DAX measure will update automatically. Nothing is hardcoded.

If you add new cities or countries, the map visual picks them up automatically. If you change the hour distribution in your data, the heatmap and activity charts update without any changes on your end.

---

## Project Structure

tinder user behavior analysis
    dataset
        Users_Data.csv
    dashboard
        Tinder_Analysis.pbix
        tinder_dashboard.html
    docs
        DAX_Measures.md
        README.md

---

## Tools Used

Power BI Desktop for the main dashboard and data model.

Python for generating the dataset with realistic distributions.

DAX for all calculated columns and measures.

---

## Final Note

This project is built to demonstrate real analytical thinking, not just visual design. The insights are grounded in documented behavioral patterns. The DAX formulas are clean and follow best practices. The layout is designed for a business audience that wants answers, not decoration.

Feel free to fork it, modify it, or use the structure as a base for your own analysis projects.

Created by Sitanshu Singh
