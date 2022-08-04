# Ames Housing Prediction

 - [Problem Statement](#Problem-Statement)
 - [Data Sources](#Data-Sources)
 - [Executive Summary](#Executive-Summary)
 - [Project 2 Final.ipynb Contents](#Project-2-Final.ipynb-Contents)
 - [Data Dictionary](#Data-Dictionary)
 - [Conclusion & Recommendations](#Conclusion-&-Recommendations)
 

## Problem Statement
We are a general insurance company based in Ames, Iowa specializing in home insurance. Customers typically come to us for home valuation services.

We have noticed through feedback forms that customers find our application forms:

- Tedious and overly complicated
- Usually take more than an hour for customers to fill up (total of 80 questions)
- Customers do not want to spend more than 10 mins

Due to the high dropout rates, management is concerned with the loss of revenue and share of customers to our competitors, who offer quicker and more accurate processing times.

As a group of data scientists within the firm, we have been tasked to simplify the application process through automating this process using machine learning models.

These predictive underwriting models will help to:
- Effectively predict the valuation of the property
- Improve efficiencies and the overall customer end-to-end experience
- Increasing take-up rate due to straight through processing

--- 
## Data Sources
The sources of the datasets used in this analysis:
* [`train.csv`](./datasets/train.csv): A dataset containing 80 housing features of 2051 residential homes sold in Ames, Iowa from 2006 to 2010. In addition, the sale prices are given for all 2051 of these houses.
* [`test.csv`](./datasets/test.csv): A dataset containing the same housing features as above of 878 homes.

---
## Executive Summary
**INTRODUCTION**

This project seeks to create a housing sale price prediction model. We will be playing the role of data scientists in a insurance company looking to improve the business process. The management has tasked us to digitalize all manual application forms and to create a good predictive model that can give the customer a house valuation in less than 10 minutes.

**METHODOLOGY**

Firstly, data import and cleaning was performed with one or more of these steps
- Reading and displaying the CSV datasets
- Finding features with strong correlation to sale price
- Drop off skewed columns
- Fill null values
- Feature engineering
- Dealing with outliers

Further preprocessing was then done after the initial cleaning
- Get dummies on categorical columns
- Preparing to test model by creating features matrix (X) and target vector (y)
- Conduct train/test split
- Fit and transform train X variables, transform only test X variables
- Check for skewness

Model was then fitted with the scaled X variables. We used linear regression as a base model. We also used GridSearchCV to find the best model parameters among linear regression, ridge, lasso and elastic net models. Once we have the optimal model, we are able to get the target predictions from the scaled X test variables.

We also used an unseen test set to predict sale prices. This was submitted on Kaggle to get a score, the lower the better.

**SIGNIFICANT FINDINGS**

We were able to obtain a low RMSE of 26607 and 26933 for the train and test sets respectively. The % difference is -1.23%, which gives us good generalisation.

We also checked that the errors are normally distributed, have equal variances and model fits a nice linear pattern.

Our final Kaggle public score is 32158 and private score is 23723.


### Project 2 Final.ipynb Contents
1. [Problem Statement](#Problem-Statement)
2. [Import Libraries](#Import-Libraries)
3. [Data Dictionary](#Data-Dictionary)
4. [Exploratory Data Analysis](#Exploratory-Data-Analysis)
    - Step 0. Import data
    - Step 1. Find features with strong correlation to saleprice
    - Step 2. Drop off specific skewed features
    - Step 3. Fill null values
    - Step 4. Feature engineering, get rid of multicollinearity
    - Step 5. Dealing with outliers
5. [Get Dummies on Categorical columns](#Get-Dummies)
6. [Model Preparation](#Model-Preparation)
    - Create features matrix (X) and target vector (Y)
    - Train/test split
    - Standard Scaler
    - Check skewness
6. [Model Fitting](#Model-Fitting)
    - Linear Regression (Base model)
    - GridSearch (LR, Ridge, Lasso, ElasticNet)
    - Evaluating the best model
    - Visualisations to infer results
7. [Kaggle Submission](#Kaggle-Submission)
---

## Data Dictionary

**Data Dictionary to be used for both Train and Test dataframes**

| Feature         | Type    | Description                                                            |
|-----------------|---------|------------------------------------------------------------------------|
| id              | int64   | ID of sale transaction                                                 |
| pid             | int64   | Property ID                                                            |
| ms_subclass     | int64   | Building class                                                         |
| ms_zoning       | object  | Identifies the general zoning classification of the sale               |
| lot_frontage    | float64 | Linear feet of street connected to property                            |
| lot_area        | int64   | Lot size in square feet                                                |
| street          | object  | Type of road access to property                                        |
| alley           | object  | Type of alley access to property                                       |
| lot_shape       | object  | General shape of property                                              |
| land_contour    | object  | Flatness of the property                                               |
| utilities       | object  | Type of utilities available                                            |
| lot_config      | object  | Lot configuration                                                      |
| land_slope      | object  | Slope of property                                                      |
| neighborhood    | object  | Physical locations within Ames city limits                             |
| condition_1     | object  | Proximity to main road or railroad                                     |
| condition_2     | object  | Proximity to main road or railroad (if a second is present)            |
| bldg_type       | object  | Type of dwelling                                                       |
| house_style     | object  | Style of dwelling                                                      |
| overall_qual    | int64   | Overall material and finish quality                                    |
| overall_cond    | int64   | Overall condition rating                                               |
| year_built      | int64   | Original construction date                                             |
| year_remod/add  | int64   | Remodel date (same as construction date if no remodeling or additions) |
| roof_style      | object  | Type of roof                                                           |
| roof_matl       | object  | Roof material                                                          |
| exterior_1st    | object  | Exterior covering on house                                             |
| exterior_2nd    | object  | Exterior covering on house (if more than one material)                 |
| mas_vnr_type    | object  | Masonry veneer type                                                    |
| mas_vnr_area    | float64 | Masonry veneer area in square feet                                     |
| exter_qual      | object  | Exterior material quality                                              |
| exter_cond      | object  | Present condition of the material on the exterior                      |
| foundation      | object  | Type of foundation                                                     |
| bsmt_qual       | object  | Height of the basement                                                 |
| bsmt_cond       | object  | General condition of the basement                                      |
| bsmt_exposure   | object  | Walkout or garden level basement walls                                 |
| bsmtfin_type_1  | object  | Quality of basement finished area                                      |
| bsmtfin_sf_1    | float64 | Type 1 finished square feet                                            |
| bsmtfin_type_2  | object  | Quality of second finished area (if present)                           |
| bsmtfin_sf_2    | float64 | Type 2 finished square feet                                            |
| bsmt_unf_sf     | float64 | Unfinished square feet of basement area                                |
| total_bsmt_sf   | float64 | Total square feet of basement area                                     |
| heating         | object  | Type of heating                                                        |
| heating_qc      | object  | Heating quality and condition                                          |
| central_air     | object  | Central air conditioning                                               |
| electrical      | object  | Electrical system                                                      |
| 1st_flr_sf      | int64   | First Floor square feet                                                |
| 2nd_flr_sf      | int64   | Second floor square feet                                               |
| low_qual_fin_sf | int64   | Low quality finished square feet (all floors)                          |
| gr_liv_area     | int64   | Above grade (ground) living area square feet                           |
| bsmt_full_bath  | float64 | Basement full bathrooms                                                |
| bsmt_half_bath  | float64 | Basement half bathrooms                                                |
| full_bath       | int64   | Full bathrooms above grade                                             |
| half_bath       | int64   | Half baths above grade                                                 |
| bedroom_abvgr   | int64   | Number of bedrooms above basement level                                |
| kitchen_abvgr   | int64   | Number of kitchens                                                     |
| kitchen_qual    | object  | Kitchen quality                                                        |
| totrms_abvgrd   | int64   | Total rooms above grade (does not include bathrooms)                   |
| functional      | object  | Home functionality rating                                              |
| fireplaces      | int64   | Number of fireplaces                                                   |
| fireplace_qu    | object  | Fireplace quality                                                      |
| garage_type     | object  | Garage location                                                        |
| garage_yr_blt   | float64 | Year garage was built                                                  |
| garage_finish   | object  | Interior finish of the garage                                          |
| garage_cars     | float64 | Size of garage in car capacity                                         |
| garage_area     | float64 | Size of garage in square feet                                          |
| garage_qual     | object  | Garage quality                                                         |
| garage_cond     | object  | Garage condition                                                       |
| paved_drive     | object  | Paved driveway                                                         |
| wood_deck_sf    | int64   | Wood deck area in square feet                                          |
| open_porch_sf   | int64   | Open porch area in square feet                                         |
| enclosed_porch  | int64   | Enclosed porch area in square feet                                     |
| 3ssn_porch      | int64   | Three season porch area in square feet                                 |
| screen_porch    | int64   | Screen porch area in square feet                                       |
| pool_area       | int64   | Pool area in square feet                                               |
| pool_qc         | object  | Pool quality                                                           |
| fence           | object  | Fence quality                                                          |
| misc_feature    | object  | Miscellaneous feature not covered in other categories                  |
| misc_val        | int64   | $Value of miscellaneous feature                                        |
| mo_sold         | int64   | Month Sold                                                             |
| yr_sold         | int64   | Year Sold                                                              |
| sale_type       | object  | Type of sale                                                           |
| saleprice       | int64   | Sale Price                                                             |

*Back to [Data Dictionary](#Data-Dictionary)*


---
## Conclusion & Recommendations 
Although we obtained a good Kaggle score, as well as good generalisation, there are limitations to the model.

1. The model does not work very well for higher sale prices and should be offset to give a better reading.
2. Multicollinearity still exists and the variables cannot be made fully independent.