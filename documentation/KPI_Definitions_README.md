# 📊 KPI Definitions -- Food Nutrition & Dietary Insights Dashboard

This document explains all **Key Performance Indicators (KPIs)** used in
the Food Nutrition & Dietary Insights Power BI Dashboard.

Each KPI is created using **DAX (Data Analysis Expressions)** and is
fully interactive with report filters such as:

-   Meal Type\
-   Food Category\
-   Food Item

------------------------------------------------------------------------

# 🔢 Average-Based KPIs

## 1️⃣ Avg Calories (kcal)

**Description:**\
Shows the average calorie content per food item.

``` dax
Avg Calories (kcal) =
AVERAGE(daily_food_nutrition[Calories (kcal)])
```

------------------------------------------------------------------------

## 2️⃣ Avg Sugar (g)

**Description:**\
Represents the average sugar content per food item.

``` dax
Avg Sugar (g) =
AVERAGE(daily_food_nutrition[Sugars (g)])
```

------------------------------------------------------------------------

# ❤️ Health Score KPI

## 3️⃣ Health Score

**Description:**\
Custom composite metric based on Calories, Sugar, and Sodium.

``` dax
Health Score =
VAR AvgCal = AVERAGE(daily_food_nutrition[Calories (kcal)])
VAR AvgSugar = AVERAGE(daily_food_nutrition[Sugars (g)])
VAR AvgSodium = AVERAGE(daily_food_nutrition[Sodium (mg)])
RETURN
ROUND(
    100
    - (AvgCal / 10)
    - (AvgSugar * 2)
    - (AvgSodium / 50),
    0
)
```

------------------------------------------------------------------------

# 🥗 Healthy Food Indicators

## 4️⃣ Healthy Food %

``` dax
Healthy Food % =
DIVIDE(
    [Weight Loss Foods],
    [Total Food Items],
    0
) * 100
```

## 5️⃣ Weight Loss Foods

``` dax
Weight Loss Foods =
CALCULATE(
    COUNT(daily_food_nutrition[Food ID]),
    daily_food_nutrition[Calories (kcal)] < 300,
    daily_food_nutrition[Sugars (g)] < 5
)
```

## 6️⃣ Muscle Gain Foods

``` dax
Muscle Gain Foods =
CALCULATE(
    COUNT(daily_food_nutrition[Food ID]),
    daily_food_nutrition[Protein (g)] > 20
)
```

------------------------------------------------------------------------

# ⚠️ Risk KPIs

## High Calorie Foods

``` dax
High Calorie Foods =
CALCULATE(
    COUNT(daily_food_nutrition[Food ID]),
    daily_food_nutrition[Calories (kcal)] > 400
)
```

## High Sugar Foods

``` dax
High Sugar Foods =
CALCULATE(
    COUNT(daily_food_nutrition[Food ID]),
    daily_food_nutrition[Sugars (g)] > 10
)
```

## High Sodium Foods

``` dax
High Sodium Foods =
CALCULATE(
    COUNT(daily_food_nutrition[Food ID]),
    daily_food_nutrition[Sodium (mg)] > 300
)
```

## Low Sodium Foods

``` dax
Low Sodium Foods =
CALCULATE(
    COUNT(daily_food_nutrition[Food ID]),
    daily_food_nutrition[Sodium (mg)] < 140
)
```

## High Cholesterol Foods

``` dax
High Cholesterol Foods =
CALCULATE(
    COUNT(daily_food_nutrition[Food ID]),
    daily_food_nutrition[Cholesterol (mg)] > 200
)
```

------------------------------------------------------------------------

# 📈 Totals & Aggregations

``` dax
Total Food Items = COUNT(daily_food_nutrition[Food ID])
Total Calories = SUM(daily_food_nutrition[Calories (kcal)])
Total Protein (g) = SUM(daily_food_nutrition[Protein (g)])
Total Carbs (g) = SUM(daily_food_nutrition[Carbohydrates (g)])
Total Fat (g) = SUM(daily_food_nutrition[Fat (g)])
Total Fiber (g) = SUM(daily_food_nutrition[Fiber (g)])
Total Sugar (g) = SUM(daily_food_nutrition[Sugars (g)])
Total Water (ml) = SUM(daily_food_nutrition[Water_Intake (ml)])
```

------------------------------------------------------------------------

# 🖼️ UX Enhancement KPI

## Meal Type PNG

``` dax
Meal Type PNG =
SWITCH(
    SELECTEDVALUE(daily_food_nutrition[Meal_Type]),
    "Breakfast", "<Breakfast Image URL>",
    "Lunch", "<Lunch Image URL>",
    "Dinner", "<Dinner Image URL>",
    "Side", "<Side Image URL>",
    "Snack", "<Snack Image URL>",
    BLANK()
)
```

------------------------------------------------------------------------

# 🧠 Summary

These KPIs provide:

-   Nutritional balance overview\
-   Health risk identification\
-   Goal-based dietary insights\
-   Interactive visual analysis

⭐ Demonstrates advanced DAX, analytical thinking, and professional
Power BI dashboard design.

------------------------------------------------------------------------

Generated on 2026-02-18
