## Basic Feature Identification
This ML project was done related to the [Pump-It-Up](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/) competiton hosted by Driven data. Dataset contains 41 seperate characteristics of water extractions in Tanzania with the goal of of predicting their functionality status.
Amoung the 41 features,
*   _subvillage_ 
*   _region_ 
*  _region_code_  
*   _district_code_
*   _lga_  
*   _ward_  

![Status group distribution along with longitude and latitude](https://github.com/chamikaCN/Pump-it-up-competition/blob/main/ReadmeFiles/Status_group_map.png)

represent the geo-administative zones of the water extractions. Out of them **region** was selected as it is the largest of the zones as well as most balanced.
From the other features **funder**, **gps_height**, **installer**, **longitude**, **latitude**, **basin**, **population**,  **construction_year** were chosen based on the null counts and common sense.
The following 16 features showed extreme similarities or sub feature structures, and therefore only 7 of them were chosen based on the comparisons.
* **waterpoint_type**  (^)
* waterpoint_type_group
* **source**  (^)
* source_type
* source_class
* **quantity**  (^)
* quantity_group
* **water_quality**  (^)
* quality_group
* **payment**   (^)
* payment_type
* **management_group**  (^)
* management
* **extraction_type_class**  (^)
* extraction_type_group
* extraction_type

![Water Quantity](https://github.com/chamikaCN/Pump-it-up-competition/blob/main/ReadmeFiles/quantity_status_group.png)

![Water Extraction Point](https://github.com/chamikaCN/Pump-it-up-competition/blob/main/ReadmeFiles/waterpoint_type_status_group.png)

## Eleminating Class Imbalance

In the training dataset labels, there was a significant class imbalance regarding the **functional needs repair** group in **status_group**. Therefore other groups were undersampled randomly to a limit of 20000 while the above group was oversampled.

| Status_Group | Count |
|--|--|
| functional| 32259 |
|non functional | 22824 | 
|functional needs repair| 4317 |

## Handling Missing Data
Out of 16 selected features 7 criteria did not have any null or unexpected zero values.

#### Null values removal

* *funder, installer* - By assigning null entries to a new category 'Unknown'

#### Zero removal

* *longitude, latitude* - These cannot be zero because Tanzania is located away from the equator and the GMT line.  Therefore the null values were grouped by **region** and assigned the **meadian** of the region. (mean was not suitable because of many zeros) 
* *population, gps_height* - Grouped by region and assigned the mean.
*  *construction_year* -  Due to the larger zero count this feature was grouped by **scheme_name**, **installer**, **funder**, **scheme_management** and **management_group** in that order seperately and assigned the mean if still Nan.

## Preprocessing

#### New Features
**duration** feature was created by (2021 - *construction_year*) to get more subtle representation of the age.

#### Categorical Data Encoding
Label Encoding was used to encode the categorical data such as quantity and water_quality.

#### Numerical Data Scaling
All numerical data were scaled using MinMax Scaling.

## Training
A random forest classifier with,
* max_depth --> 30
* no_of_estimators --> 1000

was used to train the model. 0.2 of the training data were used as the cross-validation set selected randomly.

## Submission
Following are the screenshots taken after the submission to DrivenData platform.

![In profile](https://github.com/chamikaCN/Pump-it-up-competition/blob/main/ReadmeFiles/Profile.PNG)

![In submissions tab](https://github.com/chamikaCN/Pump-it-up-competition/blob/main/ReadmeFiles/Submissions.PNG)
