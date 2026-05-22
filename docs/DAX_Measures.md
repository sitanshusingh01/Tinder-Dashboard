# DAX Measures — Tinder User Behavior Analysis
## Power BI Implementation Reference
### Created by Sitanshu Singh

---

## STEP 1 — Calculated Column (Add inside Users_Data table)

```dax
Time Bucket =
SWITCH(
    TRUE(),
    Users_Data[Active_Hour] >= 5  && Users_Data[Active_Hour] < 12,  "Morning",
    Users_Data[Active_Hour] >= 12 && Users_Data[Active_Hour] < 17,  "Afternoon",
    Users_Data[Active_Hour] >= 17 && Users_Data[Active_Hour] < 22,  "Evening",
    "Night"
)
```

---

## STEP 2 — Core Count Measures

```dax
Total Users =
COUNTROWS(Users_Data)

Active Users =
COUNTROWS(
    FILTER(Users_Data, Users_Data[Swipe_Count_Per_Day] > 0)
)

Total Swipes =
SUM(Users_Data[Swipe_Count_Per_Day])

Total Matches =
SUM(Users_Data[Matches])

Total Conversations =
SUM(Users_Data[Conversations])

Total Meetings =
SUM(Users_Data[Meetings])

Total Relationships =
SUM(Users_Data[Relationships])
```

---

## STEP 3 — Conversion Rate Measures

```dax
Match Conversion Rate =
DIVIDE(
    [Total Matches],
    [Total Swipes],
    0
)

Conversation Rate =
DIVIDE(
    [Total Conversations],
    [Total Matches],
    0
)

Meeting Rate =
DIVIDE(
    [Total Meetings],
    [Total Conversations],
    0
)

Relationship Conversion Rate =
DIVIDE(
    [Total Relationships],
    [Total Matches],
    0
)

Drop Off Rate =
1 - [Relationship Conversion Rate]
```

---

## STEP 4 — Engagement and Proximity Measures

```dax
Avg Engagement Score =
AVERAGEX(
    Users_Data,
    Users_Data[Swipe_Count_Per_Day] * Users_Data[Session_Time_Minutes]
)

Distance Preference Percent =
DIVIDE(
    COUNTROWS(FILTER(Users_Data, Users_Data[Distance_Miles] <= 10)),
    [Total Users],
    0
)

Avg Session Time =
AVERAGE(Users_Data[Session_Time_Minutes])

Avg Swipes Per Day =
AVERAGE(Users_Data[Swipe_Count_Per_Day])
```

---

## STEP 5 — Gender Segmentation Measures

```dax
Male Users =
CALCULATE([Total Users], Users_Data[Gender] = "Male")

Female Users =
CALCULATE([Total Users], Users_Data[Gender] = "Female")

Male Match Rate =
DIVIDE(
    CALCULATE([Total Matches], Users_Data[Gender] = "Male"),
    CALCULATE([Total Swipes], Users_Data[Gender] = "Male"),
    0
)

Female Match Rate =
DIVIDE(
    CALCULATE([Total Matches], Users_Data[Gender] = "Female"),
    CALCULATE([Total Swipes], Users_Data[Gender] = "Female"),
    0
)
```

---

## STEP 6 — Time Intelligence Measures (optional if date column added)

```dax
Peak Hour Users =
CALCULATE(
    [Total Users],
    FILTER(Users_Data, Users_Data[Active_Hour] >= 18 && Users_Data[Active_Hour] <= 21)
)

Evening Engagement Lift =
DIVIDE(
    CALCULATE([Avg Engagement Score], Users_Data[Time Bucket] = "Evening"),
    CALCULATE([Avg Engagement Score], Users_Data[Time Bucket] = "Morning"),
    0
)
```

---

## Dataset Column Reference

| Column | Type | Notes |
|---|---|---|
| User_ID | Whole Number | Unique key |
| Gender | Text | Male / Female |
| Age | Whole Number | 18–50 |
| City | Text | 29 cities |
| Country | Text | 14 countries |
| Swipe_Count_Per_Day | Whole Number | 20–200 |
| Matches | Whole Number | ~5–15% of swipes |
| Conversations | Whole Number | ~50–85% of matches |
| Meetings | Whole Number | ~30–70% of convos |
| Relationships | Whole Number | ~5–20% of meetings |
| Active_Hour | Whole Number | 0–23 |
| Day_of_Week | Text | Monday–Sunday |
| Distance_Miles | Decimal | 0.5–50.0 |
| Session_Time_Minutes | Whole Number | 5–90 |
| Time Bucket | Text | Calculated column |
```
