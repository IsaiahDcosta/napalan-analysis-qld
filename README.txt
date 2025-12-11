# napalan-analysis-qld
Does Naplan results of students depend on the socio-economic factors of their parents
​ 

​​DATA7001​ 

​​QLD NAPLAN RESULTS​ 

​Socioeconomic factors and their influence on student performance ​ 

​Isaiah Abner DCosta

Abstract: This report investigates the influence of socioeconomic factors, specifically parental education and occupations, on the academic achievement of students in Queensland, addressing significant educational inequalities. Utilizing the NAPLAN dataset spanning 2008 to 2022, supplemented with more recent data, our research explored how these factors impact diverse student groups, including male and female students, urban and regional students, and Indigenous and non-Indigenous populations. The analysis revealed that parental background is a strong predictor of academic success, with students from more advantaged backgrounds achieving higher scores. Furthermore, geographic location and cultural background were found to play crucial roles, with urban and non-Indigenous students generally outperforming their regional/remote and Indigenous counterparts. Notably, Indigenous students in very remote areas recorded the lowest average scores. These findings underscore the urgent need for targeted support and investment, particularly for students in regional, remote, and Indigenous communities, to bridge the identified educational gap and equip stakeholders to implement more effective support systems. 

 

Content 

​​ 

​ 

​ 

​ 

​ 

​ 

​ 

​ 

​ 

​ 

​ 

​ 

​ 

​ 

​ 

1. Problem Solving with Data 

The Australian government underscores the profound benefits of educational attainment, linking it to "higher skills, leading to higher rates of employment, higher productivity and higher lifetime earnings for individuals," as well as broader societal advantages such as "increased community engagement, improved family and child health and well-being, reduced tax burden for public services, a cleaner environment and reduced crime." In essence, an educated populace fosters a happier, healthier, and more productive society (Clarke, 2022). 

Despite this understanding, Australia faces rising educational inequality, with public schools becoming increasingly underfunded compared to the private system, and growing socioeconomic segregation in its schooling system, with the country ranking 8th among 71 participating countries in this regard (State School Teachers' Union of WA, 2017).  

This segregation means schools often cater to students from similar socioeconomic backgrounds. Compounding this inequality, funding disparities are evident: the 2021 Report on Government Services revealed that combined commonwealth and state funding for independent schools has increased at over six times the rate of public-school funding. Concurrently, private school fees have tripled since 2000, contributing to a steady increase in private school enrolments and a decline in the public system (Henebery, 2023). 

This report examines data from the National Assessment Program – Literacy and Numeracy (NAPLAN), which has consistently highlighted significant disparities in student scores and underscored enduring inequality among student cohorts. The analysis seeks to further investigate the multifaceted factors influencing these academic outcomes, with a specific focus on understanding and quantifying the extent of inequality between different student groups. 

Specifically, this project aims to understand how socioeconomic factors, particularly parental education and occupations, influence student academic achievement in Queensland. It seeks to identify and highlight educational inequalities concerning different student demographics, including gender, urban/regional location, and Indigenous status. The goal is to provide actionable insights for stakeholders such as schools, governments, and policymakers to foster targeted support in vulnerable communities and address these disparities, contributing to a data-informed discussion on achieving more equitable educational opportunities and outcomes across Australia. 

 

2. Getting the Data I Need 

NAPLAN is a series of assessments that happen yearly, where students in Years 3, 5, 7 and 9 are tested on fundamental literacy and numerical skills, serving as an important measure that indicates whether students are reaching beneficial educational outcomes. 

ACARA reports NAPLAN national results for each year level tested and domain for Australia as a whole, by state/territory as well as by: 

gender 

Indigeneity 

language background other than English status 

parental occupation 

parental education 

remoteness 

2.1 Change in Testing Procedure 

In 2023, the testing process was reworked, with the test moving online platform, and the introduction of four proficiency levels as opposed to the prior 10 bands.  

Figure 1 

NAPLAN original banding system 

Understanding NAPLAN Results  

(Understanding NAPLAN Results: Uncover Easy Way of Interpreting NAPLAN Bands, n.d.) 

Figure 2 - New NAPLAN Banding System 

Our 5-minute guide to understanding NAPLAN 

(Manoj Arachige, 2024) 

 

2.2 Data Files 

For this project, the data was sourced from two provided Excel Workbook (.XLSX) files that are publicly accessible from the ACARA website (Australian Curriculum Assessment and Reporting Authority, 2024). 

Prior to 2023, NAPLAN results were reported using 10 achievement bands, including national minimum standards. From 2023 onwards, results are reported against four proficiency levels, replacing the previous band system and national minimum standards, introducing 4 new bands: 

Due to the change in testing methodology, reporting has been split into two different files 

The first file contains all test results data from 2008 to 2022, with the 10-band ranking system 

The second file contains test result data from 2023 onwards, with the new proficiency levels 

To facilitate analysis, these files were merged to form a complete dataset. This was done using a basic python script using pandas. The result was then outputted into an xlsx file to be accessed for further analysis. (Refer to the appendix for the Python scripts used above). 

The source files were in .xlsx format, amounting to a total data size of 35MB, encompassing over 90,000 rows and 120 columns. 

The final dataset followed the structure outlined below: 

Attribute 

Description 

Data Type 

MEAN 

Mean Naplan Score 

Decimal 

YEAR_LEVEL 

(3,5,7,9) 

Int 

MEAN_SD 

Mean Naplan Score Standard Deviation 

Decimal 

AVERAGE_AGE 

Average Age 

String 

STATE 

(QLD, NSW, VIC, NT, WA) 

String 

DOMAIN 

(Grammar, Numeracy, Spelling, Reading) 

String 

MEAN_CI 

Mean Confidence Interval 

Decimal 

SUBGROUP 

Attribute Type and Value 

String 

ENROLLED_STUDENTS 

Count of students 

Int 

CALENDAR_YEAR 

Year of Test 

Int 

 

File Attributes: 523 KB, 9374 rows. 

 

 

 

3. Is My Data Fit for Use 

The data was assessed for quality and deemed largely fit for use. 

Strengths: Sourced from official records, it exhibited high overall completeness (though older records had some missing fields like "GAIN" and "NOTATTEMPTED"), reliability in accuracy (no spelling/grammatical errors), high freshness (core analytical fields were up to date), and no duplicate records. It also conformed to defined fields and formats (validity and uniqueness). 

Weaknesses & Handling: Some inconsistencies existed due to data coming from two different sources (e.g., "STATE" field having abbreviations in one and full names in another). Missing data in older records (e.g., pre-2012) was identified as Missing at Random (MAR), likely due to older data collection systems. However, these missing fields were not core to the modeling and were safely ignored. Inconsistent data, such as different terms for "not stated" and "unknown" in "PARENTAL_OCCUPATION," were unified during preprocessing. 

 

4. Making the Data Confess 

The data was analysed to reveal insights through several steps: 

Initial Review: A 2015 Australian Bureau of Statistics (ABS) logistic regression analysis was reviewed, indicating students with higher-educated parents were 2.2 times more likely to meet NAPLAN standards. 

Data Preparation: Python, with Pandas, was used for data cleaning and transformation. Categorical fields like "AVERAGE_AGE" (e.g., "8yrs 7mths") were converted to discrete numerical values. 

Exploratory Data Analysis (EDA): Visualizations (histograms, boxplots using Matplotlib and Seaborn) were created.  

Predictive Modelling: Scikit-learn was used for building models.  

A Multiple Linear Regression model, incorporating factors like year level, subject domain, and parental background, explained a significant portion of the variation in student scores, achieving an R2 score of 92.76%. 

Figure 3 – Linear Regression Model R2 Score 

 

Classification models (Random Forest, Logistic Regression, XGBoost) were used to categorize student performance (Low, Medium, High). Random Forest achieved 95% accuracy, and XGBoost was noted as the best overall for balance and stability. These models confirmed the strong link between student scores and their background. 

Figure 4 - Random Forest model results presented using a confusion matrix 

 

Figure 5 - Logistic Regression model results presented using a confusion matrix 

 

 

Figure 6 - XGBoost model results presented using a confusion matrix 

 

 

 

 

 

 

 

 

 

 

5. Storytelling with Data  

Starting the analysis of the data, the distribution of scores was plotted over a histogram.  

Figure 7 – Distribution of Mean NAPLAN Scores 

A graph with numbers and lines

AI-generated content may be incorrect. 

From the figure above, the graph does not show a typical unimodal distribution pattern as there are multiple changes in magnitude, but this is to be expected as the dataset contains rows for distinct year levels, each with a different distribution of scores. 

To show a more accurate distribution of scores, each year-level must be separated and plotted in a standalone histogram.  

 

 

Figure 8 – Distribution of Mean NAPLAN Scores across Year Levels 

A graph of a number of data

AI-generated content may be incorrect. 

By plotting cohorts separately, we can see a few trends emerging 

Progressive Increase in Central Tendency: A clear trend indicates that as the cohort year advances, the average score also increases. This is evident when comparing the mean scores across the year levels: 

The Year 3 cohort has a mean score of 385.68. 

This increases for the Year 5 cohort to a mean score of 467.72. 

The Year 7 cohort demonstrates a further increase, with a mean score of 516.72. 

The Year 9 cohort exhibits the highest mean score of 551.63. This progression suggests an improvement or accumulation of the measured attribute with increasing year level. The standard deviations (Year 3: 33.54; Year 5: 31.16; Year 7: 33.49; Year 9: 33.69) indicate a relatively consistent spread of scores around the mean for each cohort. 

Distributional Characteristics: While each cohort's scores form a unimodal distribution (as suggested by the histograms), the relationship between the mean and median provides insight into their symmetry. 

For Year 3, the mean (385.68) is slightly less than the median (388.08). 

For Year 5, the mean (467.72) is less than the median (470.86). 

For Year 7, the mean (516.72) is less than the median (523.70). 

For Year 9, the mean (551.63) is less than the median (558.90). The consistently lower mean compared to the median across all year levels suggests that the distributions are not perfectly symmetrical. 

Evidence of Negative Skewness: The observation that the mean is consistently lower than the median for all cohorts (Year 3: 385 < 388; Year 5: 467 < 470; Year 7: 516 < 523; Year 9: 551 < 558) is indicative of a negative (left) skew in the score distributions. 

This asymmetry implies that while a large number of students score around or above the median, the distribution has a longer tail towards the lower scores. This is further supported by examining the range of scores. For instance, in Year 7, scores extend from a minimum of 347.40 up to a maximum of 585.00, with the mean (516.72) being pulled away from the median (523.70) towards these lower values. 

Similarly, for Year 9, the scores range from 390.80 to 622.30, with the mean (551.63) lower than the median (558.90). 

This observed left skew indicates that students scoring below the central tendency (as represented by the median) are, on average, dispersed further from this central point than students who score above it. The interquartile ranges (IQR) provide a measure of spread for the central 50 of the data (Year 3: 42.00; Year 5: 36.82; Year 7: 38.93; Year 9: 39.87). 

 

Figure 9 – Box Plots of Mean NAPLAN Scores across Year Levels 

A graph of a number of blue and black boxes

AI-generated content may be incorrect. 

Parental Education and Employment 

Figure 10 – Box Plots of Mean NAPLAN Scores across Parental Education 

A graph of a graph showing a number of squares

AI-generated content may be incorrect. 

 

Analysis of student mean scores by parental education level, supported by descriptive statistics and the provided box plot, reveals clear patterns: 

Mean Scores and Parental Education: A positive correlation exists higher parental education levels correspond to higher student mean scores. 

Bachelor's Degree: Highest mean score (527.64). 

Diploma: Mean score 494.58. 

Certificate: Mean score 479.77. 

Year 12 Completion: Mean score 477.84. 

Not Stated: Mean score 479.92 (comparable to Certificate/Year 12). 

Year 11 Completion: Lowest mean score (449.25). 

Score Dispersion (Standard Deviation): Score variability within each group is relatively consistent, with standard deviations mostly between 65 and 69. The 'Year 11' (SD=68.72) and 'Not Stated' (SD=67.37) groups show slightly greater dispersion. This indicates a similar spread of scores around the group means, despite differing average performances. 

Distribution Shape (Mean vs. Median & Box Plot): Comparing group means with medians (estimated from the box plot) suggests slight negative (left) skew for most groups (Bachelor, Diploma, Certificate, Year 12, Year 11), as means are generally lower than medians. The 'Not Stated' group appears more symmetrical (mean ≈ median) and shows a wider interquartile range, indicating greater variability in its central 50 of scores. 

Student academic scores are positively associated with parental education levels, with the bachelor’s degree group achieving the highest mean. Most groups display a slight negative skew. Score variability (standard deviation) is broadly similar across groups, though the 'Not Stated' and 'Year 11' categories show slightly more spread. These findings underscore the influence of parental educational background on student academic outcomes. 

Plotting scores with parental occupation shows similar trends. 

Figure 11  – Box Plots of Mean NAPLAN Scores across Parental Occupation 

 

A graph of a number of purple squares

AI-generated content may be incorrect. 

The above box plot shows how students’ academic performance correlates with their parents’ occupational status. Below are key observations we can make: 

Group 1 has the highest median NAPLAN scores and the narrowest score distribution, indicating both high and consistent performance. 

Scores gradually decline from Group 1 to Group 4, suggesting a clear negative trend between lower parental occupational status and student performance. 

Students whose parents are "Not in Paid Work" have the lowest median scores and widest range, indicating more variability and lower overall achievement. 

The “Unknown/Not Stated” category sits in the middle, showing a mixed performance trend. 

This visual strongly suggests that parental occupation is positively associated with student academic achievement, with students from higher occupational backgrounds performing significantly better on average. 

 

 

Location 

Figure 12 – Bar graph of Performance by Remoteness 

A graph of different colored bars

AI-generated content may be incorrect. 

Considering the above graph, which shows the distance from NAPLAN scores depending on the distance a student lives from a major city, few key observations can be made.  

Students in the major cities have the highest score. 

Scores visibly decrease after ‘outer regional’ areas. 

The gap between the lowest and the highest is about 85.4 points. 

This shows that living in/near a major city area does positively impacts the NAPLAN scores of students. 

 

 

 

 

 

 

 

 

Indigeneity 

Figure 13 – Bar graph of Performance by Indigeneity 

 

From the simple plot above, we see an obvious score distance between non-indigenous students and indigenous. 

 

 

 

 

 

 

 

 

 

 

Score Time Series 

Figure 14 – Time Series of performance by subgroup 

A graph of a number of people

AI-generated content may be incorrect. 

Considering the average score of subgroups in the above graph there is a clear dip in average scores around 2011 (This is due to changes in the examinations which introduced heavy writing prompts). Between genders female students tend to maintain a steady gap to male students throughout above time period. Other subgroups indigenous and non-indigenous students do also maintain a steady gap, but around 2020 it shows a considerable downward trajectory for indigenous students. 

 

 

 

 

Model Results 

5.1 Linear Regression Model 

When looking at the coefficients outputted by the linear regression model, we can visualize the estimated impact of a given subgroup on a student’s score: 

Figure 15 – Linear Regression Model Coefficients 

 

The results show that the greatest predictors for students that receive high scores are students that: 

Have highly educated parents  

Have parents in high status jobs (senior managers & professionals) 

Live in a major city 

Are non-indigenous 

On the other end of the scale, the worst performing subgroup is remote and indigenous students. Six of the bottom seven subgroups contain indigenous students, with the worst scoring group having scores most impacted by the compounding negative factors of remoteness and indigeneity. 

5.2 Logistic Regression Model 

Plotting the logistic regression coefficients (Positive and Negative), we see repeating trends. 

Figure 16 – Positive Logistic Regression Model Coefficients 

A graph of a bar graph

AI-generated content may be incorrect. 

Students that: are non-indigenous, live in the city and have highly educated and employed parents, have the greatest Log-Odds increase in receiving a ‘high’ score. 

Figure 17 – Negative Logistic Regression Model Coefficients 

A graph with a bar graph

AI-generated content may be incorrect. 

Whilst looking at subgroups that negatively impact the chance of scoring high, again the groups most negatively impacted are students that are indigenous & remote, with the worst performance shown from those who are in both groups. 

 

 

5.3 Random Forest Model 

Figure 18 – Random Forest Feature Importances 

 

From analysis of the random forest model feature importance results, it seems to be suffering from over-reliance on a student’s year level, which indicates the model has multicollinearity, ignoring other attributes and relying almost entirely on the year level of the student.  

In future it would benefit the model to remove student year level to create a model that would attempt to quantify other subgroups in a meaningful way. 

 

5.4 XGBoost Model 

Figure 19 – XGBoost Feature Importances 

 

From plotting the feature importances given by the XGBoost model, we can see a similar outcome of multicollinearity where the relationship between a year level and score takes the most importance in predicting score outcomes.  

This model has performed better than the random forest, as it has identified key subgroups that impact scoring results outside of the student’s level. These features of importance here are the same as those identified previously earlier in other models: 

Parental Education 

Indigeneity 

Remoteness 

 

 

We can confirm the results given in our models simply by plotting the best performing groups: 

Figure 20 - Top 15 subgroups by average NAPLAN scores 

 

And by plotting the subgroups at risk: 

Figure 21- Subgroups at Risk: Mean NAPLAN score less than 400 

 

 

6. Conclusion 

Model results differed slightly, but ultimately the same main trends are repeated (that parental education and background is a main predictor of high scores, and indigeneity and distance from cities are the main predictors of low scores) 

The analysis revealed significant educational inequalities in Queensland, primarily driven by socioeconomic factors. Key findings consistently showed that parental background (education level and occupation type) is a strong predictor of academic success, with students from more advantaged backgrounds achieving higher and more consistent scores. Geographic location and cultural background also play crucial roles: urban students and non-Indigenous students generally outperformed their regional/remote and Indigenous peers. Notably, Indigenous students in very remote areas recorded the lowest scores, often below 400.  

These results underscore the urgent need for targeted support and investment, particularly for students in regional and remote areas, and Indigenous communities, to help bridge the identified educational gap.  

 

Response to feedback comments: 

Feedback 1: 

Overall, the video was very good. However, I would love to see you all add some information about the distributions of the values in your datasets. The overall number of rows was mentioned, but it would be nice to see how this data was distributed – perhaps how many students were from each year or each state, and how this distribution compares to Australia’s overall school demographics. This improvement could also include giving a numerical/statistical value for the quantity of invalid data values, since you mentioned you had some. Knowing these sample sizes would help put your statistical analysis and conclusions into context. 

Response: 

The group added additional distribution information in visuals, but the focus of this assignment was student performance in QLD, so as such we didn’t include data from other states. This would serve for future in-depth analysis. 

Feedback 2 

Recommendations: 1. The analysis and visualizations look really impressive! One thing that could be interesting to explore further is whether household income has an impact on students' educational outcomes. It could add another layer of insight into the factors affecting academic performance. 2. Some interesting patterns might be discovered by looking at how gender, indigeneity, and year of study interact. For instance, are girls doing better than boys in every assessment year? Do non-Indigenous students tend to score higher than Indigenous students in Years 3, 5, 7, and 9? And within the Indigenous group, are female students outperforming their male peers? Looking at these overlaps could help you find more meaningful insights into student performance. 

Response: 

The level of data provided by NAPLAN doesn’t include any information around household income, a potential general test we could do for this would involve state level information of average wages, but this would be a very broad estimation. 

The scores over time visual (figure 14) display how the subgroups of male, female, indigenous have performed over time, and it shows trends have remained stable. In terms of investigating trends between subgroups of different types, (i.e. by indigeneity, gender and year level), the source data is summarized at the group level, so we are unable to investigate this granularly. 

Reference List: 

References 

Australian Curriculum Assessment and Reporting Authority. (2024). NAPLAN national results. Www.acara.edu.au; Australian Curriculum, Assessment and Reporting Authority. https://www.acara.edu.au/reporting/national-report-on-schooling-in-australia/naplan-national-results 

Clarke, M. (2022). Introduction - Department of Education, Australian Government. Department of Education. https://www.education.gov.au/integrated-data-research/benefits-educational-attainment/introduction 

Henebery, B. (2023, September 15). Damning OECD report amplifies calls to boost public school funding. Www.theeducatoronline.com; The Educator Australia. https://www.theeducatoronline.com/k12/news/damning-oecd-report-amplifies-calls-to-boost-public-school-funding/283244 

Manoj Arachige. (2024, August 24). Our 5-minute guide to understanding NAPLAN. KIS Academics Blog. https://kisacademics.com/blog/our-5-minute-guide-to-naplan/ 

State School Teachers' Union of WA. (2017, May 18). Social Segregation in Australian Schools is Amongst the Highest in the World. SSTUWA. https://www.sstuwa.org.au/research/social-segregation-australian-schools-amongst-highest-world 

Understanding NAPLAN Results : Uncover easy way of interpreting NAPLAN Bands. (n.d.). Edulyte. https://www.edulyte.com/naplan-results/ 

 

 

 

 

 

 

 

 

Appendix 

1-  Python Script Used to merge data: 

import pandas as pd 

# Load all sheets from both files 

df_08_22 = pd.read_excel("naplan 08-22.xlsx", sheet_name=None) df_22_curr = pd.read_excel("naplan 22-current.xlsx", sheet_name=None) 

#Concatenate all sheets from each file 

df1 = pd.concat(df_08_22.values(), ignore_index=True) df2 = pd.concat(df_22_curr.values(), ignore_index=True) 

#Standardize column names 

df1.columns = df1.columns.str.strip().str.lower() df2.columns = df2.columns.str.strip().str.lower() \ 

#Align on common columns 

common_cols = list(set(df1.columns) & set(df2.columns)) df1 = df1[common_cols] df2 = df2[common_cols] 

#Merge the two datasets 

merged = pd.concat([df1, df2], ignore_index=True) 

Filter to Queensland only (if state column exists) 

if "state" in merged.columns: merged = merged[merged["state"].str.upper() == "QLD"] 

#Save the final cleaned dataset 

merged.to_excel("naplan_qld_combined_cleaned.xlsx", index=False) 

 

 

 

2-  Jupyter Notebook used for modelling, visualization 

 
