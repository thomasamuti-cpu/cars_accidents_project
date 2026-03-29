# 1.0 Project Overview

### 1.1 Real Life Problem
Traffic accidents are a common and persistent public safety issue worldwide, occurring daily in both urban and rural settings. According to the World Health Organization, road traffic accidents result in over a million fatalities each year, with many people experiencing both health and financial losses. In major cities, these accidents can be contributed by either:

* Human related factors such as distracted driving, speeding or impaired driving.

* Vehicle related factors such as vehicle defect and vehicle model.

* Environmental related factors such as poor weather, low visibility and road surface issues such as poorly maintained roads.

Understanding these factors is essential to reducing traffic accidents and developing effective safety measures.


### 1.2 Invested stakeholders
Several groups might benefit significantly from the traffic accidents data and insights drawn from understanding the primary contributory causes. These might include:

1. Government and city authorities - who might use this to identify high risk areas and improve on road infrastructure while implementing policies aimed at reducing accidents.

2. Public safety organizations - such as the Vehicle Safety Board who might use the data to aid in designing regulation and safety campaigns and enforcement strategies based on observed trends.

3. General public and drivers - who might benefit from better awareness of risk factors.

4. Vehicle manufacturers - who might leverage on insights to improve car safety features such as weather detection systems.

# 2.0 Business Understanding
### 2.1 Business Problem
Large cities such as the City of Chicago experience frequent traffic accidents often. To address this challenge, there is need for a predictive model that can identify **primary contributory cause of car accidents** using key influencing factors including:

1. Human Factors such as sex and age.

2. Vehicle Factors such as vehicle make.

3. Environmental Factors such as weather patterns.

4. Temporal Factors such as Date and Time of the Accidents.

5. Road Design Characteristics such as road defects and road surface conditions.

Such a model would support data driven decision making aimed at reducing accident rates and improving overall road safety.

### 2.2 Business Questions
The project seeks to answer the following business questions:

1. What are the most common primary contributory causes of traffic accidents?

2. How do human characteristics contribute to accident occurrence?

3. How do vehicle characteristics contribute to accident occurrence?

4. How do environmental conditions such as weather influence accident occurrence?

5. Are there specific times when accidents are more likely to occur?

6. How does road design impact the likelihood of accidents?

7. Can we accurately predict the primary cause of an accident given the human, vehicle, environmental, temporal and road design characteristics?

### 2.3 Business Objectives
The main objectives of this project are to:

1. Develop a predictive model that can classify the primary contributory cause of traffic accidents.

2. Identify key factors (Human, Vehicle, Environmental, Temporal) that significantly influence accident occurrence.

# 3.0 Data Understanding
### 3.1 Data Description and Sources
* This project utilized 3 datasets that contain information on the accident occurence, characteristics of people involved as well as the vehicle characteristics. These are:

1. City of Chicago Accident Dataset - sourced from https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if.
This dataset has 1.04 million rows and 48 columns. Each row is a traffic crash with the row identifier as the CRASH_RECORD_ID.
2. Vehicle Accident Dataset sourced from https://data.cityofchicago.org/Transportation/Traffic-Crashes-Vehicles/68nd-jvt3.  It has 2.28 million rows and 29 columns. Each row is a person with the row identifier as the PERSON_ID. The dataset also has CRASH_RECORD_ID.
3. Driver/Passenger Accident Dataset sourced from https://data.cityofchicago.org/Transportation/Traffic-Crashes-People/u6pd-qa9d. It has 2.12 million rows with 71 columns. Each row is a vehicle with the row identifier as the CRASH_UNIT_ID. This dataset however also has a CRASH_RECORD_ID.

**Note**: Our goal is to merge the three datasets using the common CRASH_RECORD_ID, creating a unified dataset that combines all relevant features for our analysis.

From the merger, we aim to use the following columns from the following datasets:

1. City of Chicago Dataset: 

* Weather condition - Weather condition at time of crash.
* Lighting condition - Light condition at time of crash.
* Road defects - Road defects, as determined by reporting officer.
* Crash type - A general severity classification for the crash. Can be either Injury and/or Tow Due to Crash or No Injury / Drive Away.
* Primary Contributory Cause - The factor which was most significant in causing the crash.
* Crash hour - The hour of the day component of CRASH_DATE.
* Crash day - The day of the week component of CRASH_DATE.
* Crash month - The month component of CRASH_DATE.

2. Vehicle Dataset:

* Number of passengers - Number of passengers in the vehicle. The driver is not included.
* Make - The make (brand) of the vehicle.
* Vehicle Use - The normal use of the vehicle.
* Vehicle Defect - Defect the vehicle had.
* Exceeds speed limit - Whether vehicle exceeded speed limit.

3. Passenger Dataset:

* Person type - Type of roadway user involved in crash.
* Sex - Gender of person involved in crash.
* Age - Age of person involved in crash.
* Driver Vision - What, if any, objects obscured the driver’s vision at time of crash.
* Physical Condition - Driver’s apparent physical condition at time of crash.
* Driver Action - Driver action that contributed to the crash.
* Pedpedal Action - Action of pedestrian or cyclist at the time of crash.

### 3.2 Target Variable
* Our target variable is: Primary contributory cause which is a multiclass classification problem.
There are 40 values of the aforementioned target variable and we aim to predict the most common primary contributory causes based on our feature variables.

### 3.3 Feature Variables
* All the other aforementioned variables other than primary contributory cause will act as our feature variables. They will be specifically selected following a merger of the 3 Datasets.

### 3.4 Challenge with large samples of rows
Following the merger, we expect 2 challenges:

1. Since a single crash may involve more than just the driver, each CRASH_RECORD_ID could correspond to multiple people. To simplify the analysis, we will focus on drivers, examining each crash event from the perspective of the drivers involved.
2. A single crash can involve multiple vehicles, so if a crash involves two cars with one person in each, it would result in at least two rows—one for each individual involved in the same crash.
3. The dataset contains millions of rows, which may exceed available computing resources. To manage this, we will limit our analysis to approximately 500,000 randomly selected samples after data cleaning, which will also help reduce the dataset size naturally.

# 4.0 Data Preparation and Cleaning
## 4.1 Data Preparation

We used several libraries to prepare and analyse the dataset:
1. Pandas - to read our csv files and perform exploratory data analysis.
2. Matplotlib - for visualizations.
3. Scikit-learn – for model fitting and evaluation. The models used were:
* Decision Forest Classifier – Base model to capture complex patterns in the dataset.
* Random Forest Classifier  - To handle high dimensional data.
* Neural Networks – To handle situations of class imbalance.

## 4.2 Data Cleaning
Prior to data analysis we selected the following columns from the following datasets:

1. City of Chicago Dataset: 
* Lighting condition - Light condition at time of crash.
* Weather condition - Weather condition at time of crash.
* Road defects - Road defects, as determined by reporting officer.
* Crash type - A general severity classification for the crash. Can be either Injury and/or Tow Due to Crash or No Injury / Drive Away.
* Primary Contributory Cause - The factor which was most significant in causing the crash.
* Crash hour - The hour of the day component of CRASH_DATE.
* Crash day - The day of the week component of CRASH_DATE.
* Crash month - The month component of CRASH_DATE.

2. Vehicle Dataset:
* Number of passengers - Number of passengers in the vehicle. The driver is not included.
* Make - The make (brand) of the vehicle.
* Vehicle Use - The normal use of the vehicle.
* Vehicle Defect - Defect the vehicle had.
* Exceeds speed limit - Whether vehicle exceeded speed limit.

3. Passenger Dataset:
* Person type - Type of roadway user involved in crash.
* Sex - Gender of person involved in crash.
* Age - Age of person involved in crash.
* Driver Vision - What, if any, objects obscured the driver’s vision at time of crash.
* Physical Condition - Driver’s apparent physical condition at time of crash.
* Driver Action - Driver action that contributed to the crash.
* Pedpedal Action - Action of pedestrian or cyclist at the time of crash.

### Final Output: 
* All 3 data sets were merged with a total of 21 columns and 1,192,524 entries.
* Dataset were filtered to contain ONLY the data that focused on drivers.
* ‘Exceeding speed limit’ and ‘pedestrian action’ columns  were dropped since they contained > 95% missing data.
* The column ‘Age’ was also noted to have a large number of missing values which was 26.6% of total data.
* The column also had negative values.
* Filling the missing values would have led to erroneous results.
* Therefore both the missing and negative values were dropped.

The final total entries were: 858,550 rows and 21 columns.

# 5.0 Exploratory Data Analysis

The primary contributory ca
## Findings
Most accidents:
1. Occured when the weather was clear. However, when not clear, they occured in rainy conditions.
![alt text](<Figures/Highest Causes of accidents based on Weather Condition.png>)
2. Occured in the daylight followed by darkly lighted roads.
![alt text](<Figures/Highest Causes of crashes based on lighting conditions.png>)
3. Occured where roads had no defects followed by roads with worn out surfaces and potholes.
![alt text](<Figures/Highest causes of crashes based on road defect.png>)
4. Did not involve any crash type injuries.
![alt text](<Figures/Highest causes of creashes based on crash type.png>) .
5. Did not have a primary cause but in those with a cause, the most common was either failing to give right of way or following too closely.
![alt text](<Figures/Highest causes of crashes based on Primary Contributory Cause.png>)
6. Involved Chevrolets, Fords and Nissans.
![alt text](<Figures/Highest causes of crashes based on Vehicle Make.png>)
7. Involved personal cars.
![alt text](<Figures/Highest causes of crashes based on Vehicle Use.png>)
8. Involved cars with no defects but of those which had brakes and tires had a defect.
![alt text](<Figures/Highest causes of crashes based on Vehicle Defect.png>)
9. Involved more men than women.
![alt text](<Figures/Highest causes of crashes based on Sex.png>)
10. Were not caused by distractions, but of those were, the most common distractions were moving or parked vehicles.
![alt text](<Figures/Highest causes of crashes based on Driver Vision.png>)
11. Involved drivers with normal physical conditions, or drivers with impaired alcohol levels, emotionally unstable or fatigued.
![alt text](<Figures/Highest causes of crashes based on Driver Physical Condition.png>)
12. Had no preceding driver action. Of those which had, drivers either failed to yield or followed too closely. 
![alt text](<Figures/Highest causes of crashes based on Driver Action.png>)
13. Involved drivers aged 20-40 years.
![alt text](<Figures/Distribution of Age in Crashes.png>)
14. Occured between 3:00 p.m -5:00 p.m.
![alt text](<Figures/Distribution of crashes based on hour of the day.png>)
15. Occured on Fridays and Saturdays.
![alt text](<Figures/Distribution of crashes based on the day of the week.png>)
16. Occured in May and August.
![alt text](<Figures/Distribution of crashes based on month of the year.png>)

## Model Results
* We started by building baseline models including Decision Tree, Random Forest Classifier, and Neural Network
1. Initial models suffered from class imbalance by overfitting.
![alt text](<Figures/First round of model accuracy comparison with 50% of the data.png>)

2. Second round with increased sample size - 80% also suffered from overfitting with low accuracy scores.
![alt text](<Figures/Second round of model comparison with 80% of the data..png>)

3. We improved the model by grouping the target variable into 5 broad causes (Environmental, Vehicle Defect, Impairment/Distraction, Driver Error, and Unknown)

* Results:
Training Accuracy: Decision Tree (55.03%), Random Forest Classifier (72.26%), Neural Network (95.94%).
Testing Accuracy: Decision Tree (54.42%), Random Forest Classifier (69.66%), Neural Network (93.56%).

* The Neural Network emerged as the best-performing model, balancing training and testing accuracy and successfully capturing complex patterns. We saved the model here: 
[text](<Trained Saved Models/neural_network_80_percent.pkl>)

#### Link to Tableau: 
* Summarized dashboard on 'Primary COntributory Causes of Crashes and Associated Factors.'

https://public.tableau.com/views/DashboardonthePrimaryContributoryCausesofCrashesandAssociatedFactors/Dashboard1?:language=en-GB&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link

# 6.0 Recommendations
From our project:
1. The most primary contributory cause of accidents was failing to yield right of way.
2. Human, vehicle, environmental and temporal characteristics all contributed significantly to accident crashes.
3. We can safely predict with the above characteristics, the primary contributory factor to accident crashes with a 93% accuracy using trained neural networks (cars_accidents_project/random_forest_80_percent.pkl).

# 7.0 Limitations
1. Computational Resource Constraints: The original dataset is massive, containing over 850,000 distinct entries. Training complex machine learning algorithms (such as Neural Networks and Random Forests) on standard local hardware (e.g., machines with 16 GB of RAM) resulted in severe memory exhaustion and computationally prohibitive training times. Consequently, to balance computational feasibility with model performance, the final models were trained on an 80% representative sample of the dataset rather than the entirety of the data.

2. Dataset Granularity and Passenger Exclusion: The raw dataset is recorded at the "person" level rather than the "crash" level, meaning every individual involved (including passengers) generates a distinct row. To prevent artificial inflation of the data and to focus our insights strictly on the active decision-makers on the road, we filtered the dataset to analyze only drivers. While this was a necessary step, it means our findings do not account for passenger demographics or casualty rates.

3. Multi-Vehicle Incident Weighting: Because our analysis was conducted at the driver level, a single collision involving two or more drivers results in multiple rows sharing the same crash report. This inherent hierarchical structure means that multi-vehicle crashes carry a proportionally heavier weight in our predictive models than single-vehicle crashes, which introduces a slight structural bias when analyzing overall primary contributory causes.

# 8.0 Suggestions for Further Studies
1. Cloud Computing Integration: Future iterations of this project should utilize cloud-based computing platforms (such as AWS EC2 instances or Google Colab Pro) and distributed data processing frameworks like PySpark. This would provide the necessary computational power to train complex Neural Networks on the full 100% dataset without memory bottlenecks.

2. Crash-Level Aggregation: To resolve the multi-vehicle weighting limitation, future studies could involve aggregating the dataset up to the Crash Level (grouping by CRASH_RECORD_ID). This would require advanced feature engineering to summarize the demographics of all drivers involved in a single incident, allowing for a pure 1:1 prediction of crash causes.

#### README.md 

