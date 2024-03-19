# SQL DEFORESTATION PROJECT

![](https://github.com/akpanmary46/SQL1/blob/main/IMAGE%20OF%20DEFORESTATION.png)

# DOCUMENTATION ON THE SQL DEFORESTATION PROJECT

# INTRODUCTION
THIS IS SQL PROJECT FRO DEFORESTATION .THE PROJECT IS DIVIDED INTO 3 CATEGORIES THAT IS FOREST_AREA,LAND_AREA AND REGION_AREA..THIS PROJECT HELP IN DECISION MAKING AND UNDERSTANDING DATASET.

# PROBLEM STATEMENT
1.TO IDENTIFY NUMBER OF COUNTRIES INVLOVE IN DEFORESTATION

2.TO DETERMINE THE HIGHEST AVERAGE INCOME

3.TO DETERMINE TOTAL AREA SQUARE KM WITH THE HIGHEST INCOME

4.TO SHOW COUNTRIE FROM EACH REGION HAVING HIGHEST TOTAL FOREST AREA


# RESEARCH QUESTION
THE AIM IS TO FIND SOLUTION TO THE ISSUES FACING DEFORESTATION BY ANSWERINGG THE QUESTIONS BELOW:

QUESTION 1. WHAT ARE THE TOTAL NUMBER OF COUNTRIES INVOLVED IN DEFORESTATION?

QUESTION 2. SHOW THE INCOME GROUPS OF COUNTRIES HAVING TOTAL AREA RANGING FROM 75,000 TO 150,000 SQUARE METER?

QUESTION 3. CALCULATE AVERAGE AREA IN SQUARE MILES FOR COUNTRIES IN THE 'UPPER MIDDLE INCOME REGION'COMPARE THE RESULT WITH THE REST OF THE INCOME CATEGORY.

QUESTION 4. DETERMINE THE TOTAL FOREST AREA IN SQUARE KM FOR COUNTRIES IN THE 'HIGH INCOME'GROUP.COMPARE RESULT WITH THE REST OF THE  INCOME  CATEGORIES.

QUESTION 5. SHOW COUNTRIES FROM EACH REGION(CONTINENT)HAVING THE HIGHEST TOTAL FOREST AREAS

# SKILLS
IN ANALYSING THE DATASET,THE SKILLS USED IN ANALYSING AND DERIVING INSIGHT ARE THE CLEANING AND TRANSFORMATION OF DATA,CTE THE DATA 

# DATA SOURCE
THE DATASET USED IN ANALYSING ARE 'FOREST_AREA.CSV' 'LAND_AREA.CSV' AND 'REGION_AREA.CSV'

# TOOLS
SQL SERVER IS THE TOOL USED IN ANALYSING THE DATESET

# DATA CLEANING/DATA TRANSFORMATION
IN ENSURING A GOOD AND WELL CONSTRUCTED DATASET. I WENT THROUGH THE COLUMN FOR DUPLICATE KEY,I CHECKED FOR ERRORS AND INACCURACY AND NULL VALUES WITHIN THE DATASET.BELOW ARE THE STEP USE IN ENSURING THAT THE DATASET IS READY FOR ANALYIS 

1.DATA CHECK

2.CONVERTING DECIMAL VALUES TO 3 DECIMAL PLACES 

3.HANDLING NULL VALUES BY USING THE UPDATE KEY AND THE CASE STATEMENT

SELECT *FROM FOREST WHERE FOREST_AREA_SQKM IS NULL;

![](https://github.com/akpanmary46/SQL1/blob/main/DATA%20CLEANING%201.png)

SET FOREST_AREA_SQKM = CASE WHEN FOREST_AREA_SQKM IS NULL THEN 0
 ELSE FOREST_AREA_SQKM
 ENDS;

![](https://github.com/akpanmary46/SQL1/blob/main/CLEANING%202.png)

SET FOREST_AREA_SQKM = ROUND (FOREST_AREA_SQKM)


BEFORE

![](https://github.com/akpanmary46/SQL1/blob/main/DIRTY%20DATA%20DECIMAL.png)

AFTER

![](https://github.com/akpanmary46/SQL1/blob/main/CLEAN%20DECIMAL.png)

SET TOTAL_AREA_SQ_MI = WHEN TOTAL_SQ_MI IS NULL THEN 0
 ELSE TOTAL_AREA_SQ_MI
 ENDS;
 
 ![](https://github.com/akpanmary46/SQL1/blob/main/CLEAN%20LAND%20WHEN%20IS%200.png)

# DATASET ANALYSIS

SELECT COUNT DISTINCT COUNTRY_NAME AS COUNTRIES_NOT_INVOLVED_IN_DEFORESTATION FROM FOREST WHERE FOREST_AREA_SQKM !=0; 
  
![](https://github.com/akpanmary46/SQL1/blob/main/SQL%20PROJECT%201.png)

SELECT DISTINCT REGION.COUNTRY_NAME,INCOME_GROUP FROM REGION FULL JOIN LAND ON REGION.COUNTRY_CODE=LAND.COUNTRY_CODE
WHERE TOTAL_AREA_SQ_MI BETWEEN 75000 AND 150000;

![](https://github.com/akpanmary46/SQL1/blob/main/SQL%20PROJECT%20Q2.JPG)

SELECT AVG (TOTAL_AREA_SQ_MI)FROM LAND F
JOIN REGION R ON F.COUNTRY_CODE=R.COUNTRY_CODE AND F.COUNTRY_NAME=R.COUNTRY_NAME
WHERE INCOME_GROUP = 'UPPER MIDDLE INCOME';

![](https://github.com/akpanmary46/SQL1/blob/main/SQL%20PROJECT%20Q3.png)

SELECT COUNT(F.COUNTRY_CODE) FROM FOREST F
JOIN REGION R ON F.COUNTRY_CODE=R.COUNTRY_CODE AND F.COUNTRY_NAME=R.COUNTRY_NAME
WHERE INCOME_GROUP = 'HIGH INCOME';

![](https://github.com/akpanmary46/SQL1/blob/main/SQL%20PROJECT%20Q4.png)

WITH EDDY_CTE AS
(SELECT  DISTINCT FOREST.COUNTRY_NAME, REGION.REGION,FOREST_AREA_SQKM,
ROW_NUMBER() OVER(PARTITION BY REGION.REGION ORDER BY FOREST_AREA_SQKM DESC) AS RANK FROM REGION
JOIN FOREST ON REGION.COUNTRY_CODE=FOREST.COUNTRY_CODE)
SELECT *FROM EDDY_CTE
WHERE RANK = 1

![](https://github.com/akpanmary46/SQL1/blob/main/SQL%20PROJECT%20Q5.png)


#INSIGHT

1.THE TOTAL NUMBER OF COUNTRIES INVOLVED IN DEFORESTATION ARE 524 IN TOTAL AND IT IS ONLY 208 COUNTRIES INVOLVED IN DEFORESTATION WHILE 316 DID NOT INVOLVED IN DEFORESTATION.

2.FROM THE ANALYSIS ABOVE,ONLY 26 COUNTRIES HAVE TOTAL AREA RANGING FROM 75,000 TO 150,000 SQUARE METER.

3.THE UPPER MIDDLE INCOME=390072.34,AVERAGE OF HIGH INCOME= 186746.88,AVERAGE OF LOW INCOME=170275.70 AND THE AVERAGE OF LOWER MIDDLE INCOME=174123 WITH THE ANALYSIS ABOVE,THE UPPER MIDDLE INCOME HAS THE HIGHEST AVERAGE AREA IN SQUARE MILES.

4.THE UPPER MIDDLE INCOME=1485,HIGH INCOME= 2133,LOW INCOME=891 AND LOWER MIDDLE INCOME=1188 WITH THE ANALYSIS ABOVE,THE HIGH INCOME HAS THE HIGHEST TOTAL FOREST AREA IN SQUARE KM.

5.FROM THE RANKING ABOVE BRAZIL FROM LATIN AMERICA AND CARIBBEAN HAS THE HIGHEST FOREST AREA SQKM WITH A FIGURE OF 5467050SQMI,FOLLOWED BY CANADA FROM NORTH AMERICA WITH A FIGURE OF 3482730SQMI,CHINA FROM EAST ASAIA AND PACIFIC WITH A FIGURE 2098635SQMI,CONGO.DEM.REP FROM SUB-SAHARAN AFRICA WITH A FIGURE 1603630SQMI,INDIA FROM SOUTH ASIA WITH A FIGURE 708604SQMI,IRAN.ISLAMIC REP FROM MIDDLE EAST AND NORTH AFRICA WITH FIGURE 106919.805SQMI RUSSIAN FEDERATION FROM EUROPE AND CENTRAL ASIA WITH A FIGURE 8151356SQMI AND WORLD FROM WORLD WITH FIGURE 41282696SQMI.

# CONCLUSION
DEFORESTATION TOOK PLACE IN ONLY 208 COUNTRIES OUT OF 524 COUNTRIES,THE REMAINING 316 COUNTRIES WAS NOT INVOLVE IN DEFORESTATION.THEY SHOULD ENCOURAGE COUNTRIES AND IMPLEMENT FINANCIAL INCENTIVES FOR SUSTAINABLE FORESTRY AND ALSO ENCOURAGE PRIVATE SECTORS.











THE FULL PROJECT CAN BE SEEN [HERE](https://github.com/akpanmary46/SQL1/blob/main/PROJECT%20WORK.sql)
