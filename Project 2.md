<div style="
display: flex;
width: 100%;
font: 300 14px IBM Plex Sans;
color: #8E72F3;
text-align: right;
margin-bottom: 0;">
	<div style="display: inline-block; width: 40%;">
	</div>
	<div style="display: inline-block;">
		<p style="margin: 5px 0 6px 0">Piashev Ivan, Shutov Alexey, Ilya Suchkov / G213 / HSE DSBA</p>
		<p style="margin: 6px 0 5px 0">14 May 2024</p>
	</div>
</div>

# Project 2
<p style="
font: 300 16px IBM Plex Sans;
color: #b9b9b9;
text-align: left;
text-transform: uppercase;
margin-bottom: 0;
margin-top: 0;
border-bottom: 2px solid gainsboro;
padding-bottom: 8;">
Elements of econometrics
</p>
<br>

#### Table of Contents

1. Introduction & Objectives
2. Data Description
3. Preprocessing Data
4. Model Estimation
5. Results and Interpretations
6. Discussion

<br>

#### Introduction & Objectives

The real estate market is a vital component of any economy, reflecting the demand and supply dynamics, economic trends, and societal preferences. In Moscow, a major metropolitan area, understanding the factors influencing real estate prices is crucial for various stakeholders, including buyers, sellers, investors, and policymakers. This project proposal aims to conduct an econometric study utilizing data scraped from cian.ru, a prominent real estate platform in Russia, to predict the prices of flats with 1/2/3/4 rooms in Moscow.

The primary objective of this study is to develop a predictive model to estimate the prices of residential flats in Moscow. Specifically, we aim to achieve the following:

- Gather data from cian.ru regarding real estate listings in Moscow, focusing on flats with 1, 2, 3 or 4 rooms.
- Identify relevant variables that could potentially influence the price of residential flats, such as proximity to metro stations, location within Moscow, total area, living area, floor level, construction year, property type (new vs. secondary market), ceiling height, and number of rooms.
- Analyze the relationship between these variables and the sale prices of flats using econometric techniques.
- Develop and validate a model that can accurately forecast the prices of residential flats based on the identified variables.
- Provide insights into the key determinants of real estate prices in Moscow and their respective impacts.

#### Data Description

Data will be scraped from [cian.ru](https://cian.ru), a popular real estate website in Russia, using web scraping techniques. The data will include information on residential flats available for sale in Moscow, focusing on flats with 1, 2, 3 or 4 rooms. Variables of interest will include:

1. Minutes from the nearest metro station.
2. Region of Moscow (e.g., North, South, West).
3. Total area of the flat.
4. Living area.
5. Floor level of the flat.
6. Number of floors in the building.
7. Construction year of the building.
8. Property type (new vs. secondary market).
9. Type of property (flat vs. apartment).
10. Ceiling height.
11. Number of rooms.

#### Preprocessing Data

Initialy, we have to get rid of different outliers which we had faced during plotting data. For example we used scatter plot of price.

![[Screenshot 2024-05-14 194742.png|center|500]]

Then we removed ten biggest outliers from sample and got much better sample to work with further:

![[Screenshot 2024-05-14 194758.png|center|500]]

Moreover, we have done the following with our dataset:
1. replaced `nan` in ceiling height with median values of the column and dropped other `nan` values from `region_of_moscow`, `construction_year` and `is_new` columns
2. deleted unuseful rows from `construction_year` column
3. added new features, such as `absolute_height` (which shows how high is the flat in turms of number of floors) and `average_room_size`
4. defined explicitly which columns store numerical and categorical data
5. created a DataFrame with dummy variables
6. removed outliers from numerical and categorical columns

After completion all these steps we got clear DataFrame without `nan` values:

![[Screenshot 2024-05-14 203149.png|center|500]]

#### Model Estimation

Firstly, we got the following distributon for frequency of the particular price in the market:

![[Screenshot 2024-05-14 195239.png|center|500]]

As far as we have to predict numerical variable `price` and use econometric models to fit, we agreed to use OLS for linear regression model. We added constant term to the independent variables (all columns except `price`) and used `sm.OLS(y, X).fit()` from `statsmodels.api` python library. 

Here are the regression summary:

![[Screenshot 2024-05-14 195255.png|center|500]]

![[Screenshot 2024-05-14 195305.png|center|500]]

![[Screenshot 2024-05-14 195316.png|center|500]]

Here standard errors (`std err` column) assume that the covariance matrix of the errors is correctly specified. Moreover, the smallest eigenvalue we got is `3.93e-28`, which might indicate that there are strong multicollinearity problems or that the design matrix is singular.

And here are the observed vs predicted values plot:

![[Screenshot 2024-05-14 195327.png|center|500]]

#### Results and Interpretations

#### Discussion
