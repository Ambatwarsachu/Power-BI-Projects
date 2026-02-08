https://www.kaggle.com/datasets/batthulavinay/indian-food-nutrition

🥗 Indian Food Nutrition Analysis Dashboard



Project Documentation



1\. Project Overview



The objective of this project is to analyze the nutritional composition of popular Indian dishes and convert raw nutritional data into actionable health insights.



This dashboard helps:



Identify high-protein, high-carbohydrate, and high-fat dishes



Evaluate sugar and sodium risk levels



Compare dishes using a standardized Health Score



Support health-aware food decisions using data



All values are calculated per 100g to ensure fair and standardized comparison across dishes.



2\. Dataset Description



The dataset Indian\_Food\_Nutrition contains nutritional values per 100g of each dish.



Available Columns

Column Name	Description

Dish Name	Name of the Indian dish

Calories (kcal)	Total energy per 100g

Carbohydrates (g)	Carbs per 100g

Protein (g)	Protein per 100g

Fats (g)	Fat per 100g

Free Sugar (g)	Free sugar per 100g

Fibre (g)	Dietary fiber per 100g

Sodium (mg)	Sodium per 100g

Calcium (mg)	Calcium per 100g

Iron (mg)	Iron per 100g





3\. Why Per 100g Standardization?



Using per-100g values ensures:



Fair comparison between dishes



No bias from serving size



Industry-standard nutritional analysis



This approach is commonly used by:



Food labels



WHO \& FSSAI guidelines



Nutrition research studies



4\. Derived Calculations \& Logic

4.1 Macro-Based Calorie Calculation (4-4-9 Rule)



Nutrition science defines calorie contribution as:



Macronutrient	Calories per gram

Carbohydrates	4 kcal

Protein	4 kcal

Fat	9 kcal

DAX Calculations



Calories from Carbohydrates



Carb Calories = 'Indian\_Food\_Nutrition'\[Carbohydrates (g)] \* 4





Calories from Protein



Protein Calories = 'Indian\_Food\_Nutrition'\[Protein (g)] \* 4





Calories from Fat



Fat Calories = 'Indian\_Food\_Nutrition'\[Fats (g)] \* 9





📌 Purpose:



Understand which macronutrient contributes most to total energy



Identify calorie-dense foods



4.2 Macro Percentage of Total Calories



This shows energy distribution, not raw quantity.



Example: % of Calories from Protein

Protein Calorie % =

DIVIDE(

&nbsp;   \[Protein Calories],

&nbsp;   'Indian\_Food\_Nutrition'\[Calories (kcal)]

)





(Similarly calculated for Carbs \& Fat)



📌 Why this matters:



Two dishes may have equal calories but very different nutrition profiles



Helps classify food as protein-heavy, carb-heavy, or fat-heavy



5\. Nutritional Category Logic

5.1 Sodium Risk Category



Sodium is critical for identifying health risk.



DAX Example

Sodium Risk Category =

SWITCH(

&nbsp;   TRUE(),

&nbsp;   'Indian\_Food\_Nutrition'\[Sodium (mg)] < 120, "Low",

&nbsp;   'Indian\_Food\_Nutrition'\[Sodium (mg)] < 400, "Moderate",

&nbsp;   "High"

)





📌 Interpretation:



Low → Heart-friendly



Moderate → Acceptable



High → Needs caution



5.2 Sugar Level Category



Free sugar directly impacts obesity and diabetes risk.



Sugar Level Category =

IF(

&nbsp;   'Indian\_Food\_Nutrition'\[Free Sugar (g)] <= 5,

&nbsp;   "Low Sugar",

&nbsp;   "High Sugar"

)





📌 Purpose:



Quickly flag unhealthy dishes



Enable filtering in visuals



6\. Health Score (0–100)

6.1 Why a Health Score?



There is no single metric that defines “healthy food”.

So we create a composite score combining:



Protein \& Fiber (positive factors)



Sugar, Sodium \& Fat (negative factors)



Energy balance



6.2 Health Score Logic (Conceptual)



Higher score = nutritionally balanced dish



Health Score =

VAR Score =

&nbsp;   ( \[Protein (g)] \* 2 +

&nbsp;     \[Fibre (g)] \* 2 )

&nbsp;   -

&nbsp;   ( \[Free Sugar (g)] +

&nbsp;     \[Fats (g)] +

&nbsp;     \[Sodium (mg)] / 100 )

RETURN

MIN(100, MAX(0, Score))





📌 Key points:



Score is relative, not medical advice



Used for comparison, ranking, and visualization



Normalized between 0–100



7\. High-Protein / High-Carb Dish Identification

Method Used:



Sorting by Protein or Carbohydrates



Top N filters



Dynamic slicer selection



📌 Why this works:



Values are per 100g



No serving size distortion



Clean comparison logic



8\. Visual Design Decisions

Scatter Plot



X-Axis: Energy (kcal)

Y-Axis: Health Score (0–100)

Legend: Sodium Risk Category



📌 Insight Generated:



Calorie-dense dishes are not always unhealthy, and sodium risk plays a key role in overall health evaluation.



9\. Business \& Real-World Use Cases



This dashboard can be used by:



Nutritionists



Food startups



Health-conscious consumers



Policy \& compliance teams



Use cases:



Menu optimization



Healthy food recommendation



Regulatory analysis



Consumer awareness



10\. Key Takeaways



Analytics is not about visuals — it’s about decisions



Standardized data enables fair insights



Derived metrics turn raw numbers into meaning



Health is multi-dimensional, not single-metric



11\. Limitations \& Future Enhancements



Serving size data not available



Thresholds can be aligned with WHO/FSSAI



Micronutrient weighting can be improved



Predictive health impact modeling can be added



12\. Tools Used



Power BI



DAX



Data modeling \& visualization best practices

