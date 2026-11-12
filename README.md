" Healthcare Data Analysis And Insights

" 1) Problem Statement 

'This project aims to analyze a comprehensive healthcare dataset
comprising medical examinations, hospitalization details, and customer profiles to extract
insights into patient health profiles, medical histories, and healthcare costs. By exploring
relationships between various health metrics, identifying trends, and visualizing key patterns, we
aim to deliver actionable insights to healthcare stakeholders for informed decision-making
through rigorous data cleaning, transformation, exploration, and analysis.

" 2)Dataset Description 

3 data sheet including the dataset, customer data this contains name and id ,medical examination data contains customer weight,
diabetes status,heart issues,concer history ,number of surgeries are includ,hospitalization data contains customer birth data and charge

"  3)Data Pre Processing

## 3) Data Preprocessing - With Formulas

### A. Data Cleaning

1. **Missing '?' check**: `=COUNTIF(range,"?")` use cheythu count eduthu.

2. **Fill month/year**:
   - Month: `=IF(A2="?", "Sep", A2)`
   - Year: `=IF(A2="?", ROUND(AVERAGE(range),0), A2)`

3. **Mode fill (smoker, Hospital tier, City tier)**:
   - `=MODE(range)` eduthittu `=IF(A2="?", MODE_value, A2)`

4. **State ID**: `=IF(A2="?", "Unknown", A2)`

### B. Data Transformation

1. **Split Names (Title, First Name, Last Name)**:
   - Title: `=LEFT(A2, FIND(" ",A2)-1)`
   - First Name: `=MID(A2, FIND(" ",A2)+1, FIND(" ",A2, FIND(" ",A2)+1)-FIND(" ",A2)-1)`
   - Last Name: `=RIGHT(A2, LEN(A2)-FIND(" ",A2, FIND(" ",A2)+1))`
   - (Or) `=TEXTSPLIT(A2," ")`

2. **NumberOfMajorSurgeries to Number**:
   - `=VALUE(SUBSTITUTE(SUBSTITUTE(A2," surgeries","")," surgery",""))`
   - `=IF(A2="None",0,A2)`

3. **Heart Issues / smoker clean**: `=UPPER(TRIM(A2))` then `=IF(A2="YES","Yes",IF(A2="NO","No",A2))`

4. **Weight Status**:
   - `=IF(BMI<18.5,"Underweight",IF(BMI<25,"Normal Weight",IF(BMI<30,"Overweight","Obesity")))`
   - Formula: `=IF(C2<18.5,"Underweight",IF(C2<=24.9,"Normal Weight",IF(C2<=29.9,"Overweight","Obesity")))`

5. **Diabetes Status**:
   - `=IF(HbA1C<5.7,"Normal",IF(HbA1C<=6.4,"Prediabetes","Diabetes"))`

6. **Date of Birth**:
   - `=DATE(year,MONTH(DATEVALUE(month&" 1")),date)`
   - Format: `=TEXT(DATE(A2,B2,C2),"DD-MMM-YYYY")`

7. **Age Calculation (as of 8th June 2023)**:
   - `=DATEDIF(DOB, DATE(2023,6,8), "Y")`
   - `=YEARFRAC(DOB, DATE(2023,6,8))` 

8. **Charges Currency**:
   - Format cells as Currency -> `$`
   - `=TEXT(A2,"$#,##0.00")`
