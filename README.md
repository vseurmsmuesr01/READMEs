# README File for Student Dropout Prediction Project 
**IndividualAssignment2_HUDK4054_YueSummerWu**

## README File Creator 
- **Name:** Summer (Yue) Wu
- **Email:** sw3891@tc.columbia.edu
- **Phone Number:** 646-667-8113
- **ORCID ID:** 0009-0001-1198-2308
- **Affiliation:** Teachers College, Columbia University 

## Project Overview 
- **Title:** Student Dropout Prediction
- **Objective:** This project represents a group effort for our midterm assignment, aimed at leveraging machine learning techniques to forecast the likelihood of student dropouts. Our mission was to pinpoint students who are potentially at risk of discontinuing their studies by analyzing a range of predictive factors. The culmination of our efforts is represented through a binary outcome, where ‘1’ signifies a prediction of dropout, and ‘0’ indicates otherwise. Central to our project was the ambition to meticulously evaluate a multitude of variables to accurately forecast dropout instances, with the F2 score serving as our benchmark for model selection. The preparatory phase involved an extensive process of data consolidation, purification, and feature development, setting the stage for the experimental phase. In this phase, we explored seven distinct modeling techniques, ultimately identifying the LightGBM model as the most effective tool for predicting student dropouts.
- **Team Members:**
  - Summer (Yue) Wu, sw3891@tc.columbia.edu
  - Viola (Qingyi) Tan, vt2390@tc.columbia.edu
  - Maggie (Simeng) Zhao, sz3163@tc.columbia.edu
  - Carmen (Yanfei) Chen, yc4282@tc.columbia.edu
  - Bryan (Yuxuan) Wu, yw3858@tc.columbia.edu
  - Theresa (Yajun) Zhao, tz2579@tc.columbia.edu
- **Course:** HUDK4050-Educational Data Maning
- **Instructor:** Dr. JD Jayaraman, jj2797@tc.columbia.edu
- **Institution:** Teachers College, Columbia University
- **Research Period:** 10/24/2023 - 11/21/2023

## Data Overview 
In this project, we utilized three comprehensive datasets to facilitate the prediction of student dropouts, namely Financial Aid Data, Student Progress Data, and Student Static Data. Each of them offers unique insights into different aspects of the student profile. 
|Data|Description| 
|:----|:-----------|
|Financial Aid Data|Data about the financial assistance received by students, categorized by various types of financial aid.|
|Student Static Data|Data that do not change over time, such as demographics and academic background.|
|Student Progress Data|Data that reflect students’ academic activity, or progress, for each term enrolled.|
|DropoutTrainLabels|Training data indicating the dropout status of students.|
|TestIDs|IDs of students for whom dropout predictions are required.|

### Financial Aid Data 
This Excel dataset encompasses an array of financial aid information for students spanning from 2012 to 2017. It is structured to provide a multi-dimensional view of financial aid distribution through various lenses including: 
- Demograhics such as marital status.
- Adjusted income information including adjusted gross income and parent adjusted gross income.
- Parents' highest degree.
- Housing status, on campus, off campus, or with parents.
- Amount of loans received from 2012 to 2017.
- Amount of scholarship received from 2012 to 2017.
- Amount of federal work study received from 2012 to 2017.

### Student Static Data 
The Student Static Data consist of a comprehensive dataset gathered once for each entering cohort, spanning from Fall 2011 to Spring 2016, across eleven distinct CSV files. Each file encompasses a variety of information including:
- Demographics, such as age, gender, and race/ethnicity.
- Address information for geo-coding and Census data matching (Note: to maintain confidentiality, address data will be encrypted upon transmission and deleted after geo-coding. See the Frontier Set Data Sharing Agreement for further details).
- Educational background, including high school GPA, high school credential and year, and previous college enrollment and degrees.
- Student’s academic preparation status.
- Previous dual high school enrollment or summer program participation prior to first term of enrollment.
- Student’s first registration date.
- Student’s transfer status, and number of credits transferring in.
- Amount of known loan debt the student has accumulated at time of entry to the institution.

### Student Progress Data 
These data provide the ability to examine students’ academic progress over time. Collected for every term from Fall 2011 to Summer 2017, these data (18 CSV files) include information such as:
- Course enrollments/transcript data: All courses attempted, grade and number of credits received, and delivery method.
- Educational intent or objective, and type of degree sought.
- Certificates or degrees with CIP code for credential earned.

## Prerequisites
- **Python:** Python 3.6 or a more recent version is required to ensure compatibility with the utilized syntax and libraries.
- **Jupyter Notebook:** This project utilizes Jupyter Notebook, which can be accessed via Google Colab for those without a local setup. Alternatively, the notebook is available for use if you have configured the Jupyter environment on your local machine.
- **Python Packages:**
  ```Python
  import pandas as pd
  import numpy as np
  import matplotlib.pyplot as plt
  import seaborn as sns
  from sklearn.model_selection import train_test_split
  from sklearn.tree import DecisionTreeClassifier
  from sklearn.ensemble import RandomForestClassifier, BaggingClassifier, AdaBoostClassifier, GradientBoostingClassifier
  from sklearn.metrics import fbeta_score
  ```

## Data Access
- **Liscence:** The datasets provided for the "HUDK 4050 Student Dropout Prediction Challenge" on Kaggle are made available for the specific purpose of participation in the competition without specific liscence. Participants are encouraged to engage with the dataset under the competition rules of:
  - **Apply Yourself:** Participants are encouraged to use the dataset for learning, exploration, and applying machine learning techniques to solve the challenge.
  - **Have Fun:** The competition aims to foster a community of learning and innovation, promoting an enjoyable experience for all.
- **Restrictions:**
  - **Competition-Specific Use:** The dataset is intended solely for use within the scope of the competition. Any use of the data outside of this context should respect any additional licensing information provided by the competition organizers or Kaggle.
  - **No Redistribution:** Participants are typically prohibited from redistributing the data directly. Sharing insights, models, and code through Kaggle Notebooks is encouraged, but direct sharing of the dataset files is restricted.
  - **Compliance with Kaggle's Terms of Service:** All participants must adhere to Kaggle's Terms of Service, which outline acceptable use cases and behaviors on the platform.
- **Accessing the datasets:**
  - Navigate to the Competition Page: Visit the [competition's Kaggle page](https://www.kaggle.com/competitions/hudk-4050-student-dropout-prediction-challenge-f23/data).
  - Kaggle Account: You must have a Kaggle account to proceed. If you do not have one, sign up for free at Kaggle.
  - Accept the Competition Rules: Before downloading the dataset, you may be prompted to accept the competition's rules.
  - Download the Dataset: Click on the "Data" tab on the competition page to find and download the dataset files. The data might be provided in multiple files or split between training and test sets.

## Data Preprocessing 
- **Merging datasets**
  - Standardized variable names across the three data types to ensure consistency.
  - Merged datasets within each category.
  - Integrated the three distinct datasets into a single, comprehensive dataset.
- **Reduce features**
  - Droped features with one unique value.
  - Dropped features with 100% null values.
  - Dropped irrelevant features.
- **Data imputation**
  - Imputed labeled missing values (-1). 
  - Imputed non-labeled missing values (NaN). 
  - Imputed data labeled as "not applicable" (-2).
- **Feature engineering**
  - Dummy-coded categorical variables
  - Created new features related to Financial Aid Data and GPA.

## Modelling  
Every machine learning model has its own set of benefits and strengths that make them suitable for different tasks. Some models are Decision Trees, Random Forest, KNN, Neural Networks, Gradient Boosting, etc. To identify the optimal model, we splitted the training data into train and test subsets, and trained seven different models, with the majority being ensemble models. The performance of each model was assessed using the F2(F-beta) metric as the evaluation criterion.
|Rank|Model|F2 Score|
:----:|:----:|:-------:|
1|LightGBM|0.9428|
2|Gradient Boosting|0.9387|
3|XGBoost|0.9385|
4|Neural Networks|0.9349|
5|Random Forest|0.9328|
6|Ada Boosting|0.9319|
7|Bagging|0.9306|

## Evaluation of Test Data
Upon comparing the F2 scores of the trained models, it was evident that LightGBM exhibited the best performance, achieving a score of 0.9428. When applying this trained model to predict the test data (the CSV file named "TestIDs", the obtained score was 0.9269.

## Data Dictionary 
### Financial Aid Data 
|Variable Name|Value Label|Definition|
|:-----------:|:----------|:---------|
|ID with leading|Format: Alphanumeric; maximum length 75|Assigned by the institution, StudentID is the unique identifier used to identify a student. StudentID is required on all files containing student information. StudentID is to be consistent across all files and all years for each student. StudentID is treated as sensitive information: It will be encrypted in the database and only shown to authorized users—approved Coffey Data Team members and Frontier Set Site data providers approved by the Frontier Set Site to have access to the Frontier Set DMS--to identify problem records in uploaded files. <br> <br>Notes:<br>1. Leading and trailing empty spaces are ignored.<br>2. StudentID is case sensitive; “StudentOne” and “studentone” are treated as two different values.<br>3. StudentID is required for each student.|
|cohort|2011-12<br>2012-13<br>2013-14<br>2014-15<br>2015-16<br>2016-17<br> <br>Format: YYYY-YY|Include all undergraduate students who attempted at least one course in a given term, for the first time at your institution. Students may be first-time ever in college or new transfer students into your institution and may be enrolled at any program level, including credential-seeking; college remedial, developmental, or college-preparatory; adult basic skills (ESL, ABE, or ASE/GED); and non-credit vocational students. For non-credit vocational students, only include those who enrolled in courses that could lead to an occupational certificate, industry certificate, or other type of credential of economic value, as well as those students who are simultaneously enrolled in credit-bearing courses.<br> <br>Also include:<br> * Past dual enrollment students who took a course or courses at your institution while simultaneously attending high school. <br>* Fall entry students who enrolled in summer work prior to first term of enrollment with credential-seeking status. Examples of summer work include, but are not limited to, summer bridge programs or developmental/remedial coursework. <br> <br>Exclude students who are: <br> *Non-credit vocational students enrolled in purely personal enrichment courses; <br> *Current dual enrollment students or those taking a course or courses at your institution while simultaneously attending high school. <br> <br> Report data for cohorts of first-time students for each term (including summer) in a given academic year, starting with the fall term of the 2011-12 academic year.<br> <br>Cohort must be assigned for each student.|
|cohort term|1 = Term 1 <br> 2 = Term 2 <br> 3 = Term 3 <br> 4 = Term 4 <br> 5 = Term 5 <br> 6 = Term 6 <br> 7 = Term 7 <br> <br>Format: Numeric|Cohort term of entry: Term student first enrolled in at least one course. See definition of cohort.<br> <br>CohortTerm must be assigned for each student.<br> <br> Term 1 = Fall term<br>Term 2 = Late fall or winter short/inter-sessions <br>Term 3 = Spring term for institutions on semester schedule; winter term for those on trimesters or quarters <br>Term 4 = Spring term for trimester/quarter institutions<br>Term 5 = Late winter or spring short/inter-sessions <br>Term 6 = Summer I <br>Term 7 = Summer II|
|Marital Status|Format: Alphanumeric, 50|Students' state of being single, married, separated, divorced, or widowed|
|Adjusted Gross Income|Format: Numeric|Students' individual income|
|Parent Adjusted Gross Income|Format: Numeric|Income from students' parents|
|Father's Highest Grade Level|Format: Alphanumeric, 50|Father's highest degree|
|Mother's Highest Grade Level|Format: Alphanumeric, 50|Mather's highest degree|
|Housing|Format: Alphanumeric, 50|Students' state of living on campus, off campus, or with parents|
|2012 Loan|Format: Numeric|Amount of loans students received in 2012|
|2012 Scholarship|Format: Numeric|Amount of scholarship students received in 2012|
|2012 Grant|Format: Numeric|Amount of grant students received in 2012|
|2012 Work/Study|Format: Numeric|Amount of Work/Study students received in 2012|
|2013 Loan|Format: Numeric|Amount of loans students received in 2013|
|2013 Scholarship|Format: Numeric|Amount of scholarship students received in 2013|
|2013 Grant|Format: Numeric|Amount of grant students received in 2013|
|2013 Work/Study|Format: Numeric|Amount of Work/Study students received in 2013|
|2014 Loan|Format: Numeric|Amount of loans students received in 2014|
|2014 Scholarship|Format: Numeric|Amount of scholarship students received in 2014|
|2014 Grant|Format: Numeric|Amount of grant students received in 2014|
|2014 Work/Study|Format: Numeric|Amount of Work/Study students received in 2014|
|2015 Loan|Format: Numeric|Amount of loans students received in 2015|
|2015 Scholarship|Format: Numeric|Amount of scholarship students received in 2015|
|2015 Grant|Format: Numeric|Amount of grant students received in 2015|
|2015 Work/Study|Format: Numeric|Amount of Work/Study students received in 2015|
|2016 Loan|Format: Numeric|Amount of loans students received in 2016|
|2016 Scholarship|Format: Numeric|Amount of scholarship students received in 2016|
|2016 Grant|Format: Numeric|Amount of grant students received in 2016|
|2016 Work/Study|Format: Numeric|Amount of Work/Study students received in 2016|
|2017 Loan|Format: Numeric|Amount of loans students received in 2017|
|2017 Scholarship|Format: Numeric|Amount of scholarship students received in 2017|
|2017 Grant|Format: Numeric|Amount of grant students received in 2017|
|2017 Work/Study|Format: Numeric|Amount of Work/Study students received in 2017|

### Student Static Data 
|Variable Name|Value Label|Definition|
|:-----------:|:----------|:---------|
|StudentID|Format: Alphanumeric; maximum length 75|Assigned by the institution, StudentID is the unique identifier used to identify a student. StudentID is required on all files containing student information. StudentID is to be consistent across all files and all years for each student. StudentID is treated as sensitive information: It will be encrypted in the database and only shown to authorized users—approved Coffey Data Team members and Frontier Set Site data providers approved by the Frontier Set Site to have access to the Frontier Set DMS--to identify problem records in uploaded files. <br> <br>Notes:<br>1. Leading and trailing empty spaces are ignored.<br>2. StudentID is case sensitive; “StudentOne” and “studentone” are treated as two different values.<br>3. StudentID is required for each student.|
|Cohort|2011-12<br>2012-13<br>2013-14<br>2014-15<br>2015-16<br>2016-17<br> <br>Format: YYYY-YY|Include all undergraduate students who attempted at least one course in a given term, for the first time at your institution. Students may be first-time ever in college or new transfer students into your institution and may be enrolled at any program level, including credential-seeking; college remedial, developmental, or college-preparatory; adult basic skills (ESL, ABE, or ASE/GED); and non-credit vocational students. For non-credit vocational students, only include those who enrolled in courses that could lead to an occupational certificate, industry certificate, or other type of credential of economic value, as well as those students who are simultaneously enrolled in credit-bearing courses.<br> <br>Also include:<br> * Past dual enrollment students who took a course or courses at your institution while simultaneously attending high school. <br>* Fall entry students who enrolled in summer work prior to first term of enrollment with credential-seeking status. Examples of summer work include, but are not limited to, summer bridge programs or developmental/remedial coursework. <br> <br>Exclude students who are: <br> *Non-credit vocational students enrolled in purely personal enrichment courses; <br> *Current dual enrollment students or those taking a course or courses at your institution while simultaneously attending high school. <br> <br> Report data for cohorts of first-time students for each term (including summer) in a given academic year, starting with the fall term of the 2011-12 academic year.<br> <br>Cohort must be assigned for each student.|
|Cohort Term|1 = Term 1 <br> 2 = Term 2 <br> 3 = Term 3 <br> 4 = Term 4 <br> 5 = Term 5 <br> 6 = Term 6 <br> 7 = Term 7 <br> <br>Format: Numeric|Cohort term of entry: Term student first enrolled in at least one course. See definition of cohort.<br> <br>CohortTerm must be assigned for each student.<br> <br> Term 1 = Fall term<br>Term 2 = Late fall or winter short/inter-sessions <br>Term 3 = Spring term for institutions on semester schedule; winter term for those on trimesters or quarters <br>Term 4 = Spring term for trimester/quarter institutions<br>Term 5 = Late winter or spring short/inter-sessions <br>Term 6 = Summer I <br>Term 7 = Summer II|
|Campus|If you are not a data provider for a system or institution with campuses, leave this field blank. <br> <br> If you are a data provider for a system or institution with campuses, please contact your Data Coordinator for valid UNITID values.<br> <br> Format: Alpha, 10|Campus or Institution Indicator: For data providers at the system level, or institutions with campuses, populate “Campus” with institution or campus US Department of Education UNITID. Please contact your Data Coordinator for valid UNITID values. The UNITID should reflect the institution or campus where the student initially enrolled.<br> <br>For data providers submitting data for systems that contain merged and consolidated institutions, report student data with the actual institution attended. That is, if Institution A and Institution B merged in 2014 to become Institution C, report student data with Institution A for 2011 through 2013, and the same for Institution B. Beginning in 2014, all students still enrolled from the 2011 through 2013 cohorts and new 2014 cohort students are to be reported with Institution C.|
|Address1|Format: Alphanumeric, 50|Student's permanent address at time of first enrollment: Street number and name.<br> <br>This is the student’s home or permanent address (usually a parent’s address), not a local address where the student lives during the academic year.<br> <br> Note: leave blank for international students.|
|Address2|Format: Alphanumeric, 50|Student's permanent address at time of first enrollment: Apartment, floor, suite, building number, or more specific or supplemental address information. <br> <br>Note: leave blank for international students.|
|City|Format: Alphanumeric, 25|Student's permanent address at time of first enrollment: City.<br> <br> Note: leave blank for international students.|
|State|Format: Alphanumeric; 2|Student's permanent address at time of first enrollment: State-U.S. Postal code abbreviation. <br> <br>Note: leave blank for international students.|
|Zip|Format: Alphanumeric; XXXXX|Student's permanent address at time of first enrollment: 5-digit zip code. <br> <br>Note: leave blank for international students.|
|RegistrationDate|Format: YYYYMMDD|Student's first registration date: Date of the first registration for the student's first enrollment at the institution.|
|Gender|1 = Male<br>2 = Female<br>3 = Other<br>-1 = Missing<br> <br>Format: Numeric|Gender of the student.<br> <br>Code 3 = Other, for example, transgender or intersex students.|
|BirthYear|Continuous<br>-1 = Missing<br> <br>Format: YYYY; Numeric|Student's year of birth|
|BirthMonth|01 to 12<br>-1 = Missing<br> <br>Format: MM; Numeric|Student’s month of birth.|
|Hispanic|0 = No <br> 1 = Yes <br> -1 = Missing<br> <br>Format: Numeric|Student is of Hispanic origin. If a student is a non-resident alien, code this and all race variables as 0. If race/ethnicity is unknown, code this and all race variables as -1.
|AmericanIndian|0 = No <br> 1 = Yes <br> -1 = Missing<br> <br>Format: Numeric|Student identifies with the American Indian/Alaskan Native race category. If a student is a non-resident alien, code this and all race variables as 0. If race/ethnicity is unknown, code this and all race/ethnicity variables as -1.|
|Asian|0 = No <br> 1 = Yes <br> -1 = Missing<br> <br>Format: Numeric|Student identifies with the Asian race category. If a student is a non-resident alien, code this and all race variables as 0. If race/ethnicity is unknown, code this and all race variables as -1.|
|Black|0 = No <br> 1 = Yes <br> -1 = Missing<br> <br>Format: Numeric|Student identifies with the Black/African American race category. If a student is a non-resident alien, code this and all race variables as 0. If race/ethnicity is unknown, code this and all race variables as -1.|
|NativeHawaiian|0 = No <br> 1 = Yes <br> -1 = Missing<br> <br>Format: Numeric|Student identifies with the Native Hawaiian/Other Pacific Islander race category. If a student is a non-resident alien, code this and all race variables as 0. If race/ethnicity is unknown, code this and all race variables as -1.|
|White|0 = No <br> 1 = Yes <br> -1 = Missing<br> <br>Format: Numeric|Student identifies with the White race category. If a student is a non-resident alien, code this and all race variables as 0. If race/ethnicity is unknown, code this and all race variables as -1.|
|TwoOrMoreRace|0 = No <br> 1 = Yes <br> -1 = Missing<br> <br>Format: Numeric|Student identifies with two or more racial/ethnic groups, but the detail of the groups is unknown. If a student is a non-resident alien, code this and all race variables as 0. If race/ethnicity is unknown, code this and all race/ethnicity variables as -1.|
|HSDip|0 = None <br>1 = High School Diploma <br>2 = GED <br>3 = Adult high school diploma <br>4 = All other<br>-1 = Missing<br> <br>Format: Numeric|Student's high school completion status. Student has a high school diploma or recognized equivalent, a GED (a document certifying the successful completion of a prescribed secondary school program of studies, or the attainment of satisfactory scores on the GED or another state-specified examination), or an adult high school diploma. <br> <br>If HS completion status is unknown, code as -1 = Missing.|
|HSDipYr|-1 = Missing <br>-2 = Does not apply<br> <br>Format: YYYY; Numeric|Year student received high school diploma, GED, or other high school completion/certification|
|HSGPAUnwtd|Continuous <br> -1 = Missing<br> <br>Format: X.XX; Numeric|Student’s unweighted high school grade point average, on a 4.0 scale.<br> <br>NOTE: Report the unweighted GPA, i.e., do not include weights for advanced placement, honors, or other types of advanced classes in students’ GPAs.|
|HSGPAWtd|Continuous <br>-1 = Missing<br> <br>Format: X.XX; Numeric|Student’s weighted high school grade point average, on a 4.0 scale.<br> <br>NOTE: Report the weighted GPA, i.e., include weights for advanced placement, honors, or other types of advanced classes in students’ GPAs.|
|FirstGen|0 = No, student is not known to be a first generation student<br>1 = Yes, student is known to be a first generation student <br> -1 = Missing<br> <br>Format: Numeric|Student whose parents’ highest education level is some college but no degree or below (e.g. some college, no degree; vocational/technical training; high school diploma or equivalent; did not complete high school). Students’ whose parents have associate’s degrees or higher are not considered first generation.<br> <br>Code as -1 = Missing if first generation status is unknown.|
|DualHSSummerEnroll|<br>0 = Not past dual enrollment nor summer enrollee<br>1 = Past dual enrollment, not summer enrollee<br>2 = Past summer enrollee, not past dual enrollment<br>3 = Past dual enrollment and summer enrollee<br>-1 = Missing<br> <br>Format: Numeric|Student was a previous dual/concurrent high school enrollment student prior to first term enrolled with credential-seeking status, and/or enrolled in summer work prior first term of enrollment with credential-seeking status. Examples of summer work include, but are not limited to, summer bridge programs or developmental/remedial coursework.|
EnrollmentStatus|<br>1 = Entering freshman student<br>2 = Entering transfer student<br>-1 = Missing<br> <br>Format: Numeric|Entering freshman students are those entering the Frontier Set institution for the first time, without known previous postsecondary experience. Include students who have prior dual enrollment experience or credit (including AP or IB) as entering freshman.<br> <br>Entering transfer students are those who enter the Frontier Set institution for the first time, but have previous postsecondary experience; transfer students may transfer with or without credit.|
|NumColCredAttemptTransfer|Continuous<br>0 = Valid zero (transfer student, no credits attempted to be transferred)<br>-1 = Missing (transfer student, the number of credits attempted for transfer is unknown)<br>-2 = Does not apply (not a transfer student)<br> <br>Format: Numeric|Number of prior college credits student attempted to transfer: Number of college credits student attempted to transfer in from attendance at another postsecondary institution prior to attending this institution. Report the total number of college credits that student attempted to transfer, whether or not your institution recognizes the credits. <br> <br>Do not include credits earned by completion of AP, IB or similar high school coursework.<br> <br>If the student is known to be a transfer student, but no credits attempted to transfer, code as 0.<br> <br>If the student is known to be a transfer student, but the number of credits attempted for transfer is unknown, code as -1 = Missing.<br> <br>If the student is not known to be a transfer student, code as -2 = Does not apply.|
|NumColCredAcceptTransfer|Continuous<br>0 = Valid zero (transfer student, no credits transferred)<br>-1 = Missing (transfer student, the number of credits accepted is unknown)<br>-2 = Does not apply (not a transfer student)<br> <br>Format: Numeric|Number of prior college credits: Number of college credits student attempted to transfer from another postsecondary institution that your institution recognized/accepted. Do not include credits earned by completion of AP, IB or similar high school coursework.<br> <br>If the student is known to be a transfer student, but credits were not accepted by your institution and transferred in, code as 0.<br> <br>If the student is known to be a transfer student, but the number of credits accepted by your institution and transferred is unknown, code as -1 = Missing.<br> <br>If the student is not known to be a transfer student, code as -2 = Does not apply.|
|CumLoanAtEntry|Continuous<br>0 = Valid zero (Known transfer student, no previous cumulative loan amount)<br>-1 = Missing (Known transfer student, previous cumulative loan amount unknown)<br>-2 = Known not to be a transfer student, does not apply<br> <br>Format: Numeric|If available from administrative records, the amount of known debt the student had accumulated at time of entry to the institution. This includes the sum of all accumulated federal loans (Perkins loans, Federal Direct loans, federal health professions loans, and Direct PLUS loans to parents), state loans, institutional loans, and other private (alternative) loans (education loans from commercial lenders that are not government guaranteed and carry market interest rates based on credit scores).<br> <br>This is an optional data element; please provide it if you are able, from administrative records only.|
|HighDeg|0 = None<br>1 = Certificate (undergraduate)<br>2 = Associate's Degree<br>3 = Bachelor's Degree<br>4 = Higher than Bachelor's degree<br>5 = Any other<br>-1 = Missing<br> <br>Format: Numeric|Highest previous postsecondary degree/certificate student holds. If the student holds a degree(s) or certificate(s) from any type of previous postsecondary institution, indicate the level of the highest award attained. If the student does not have a known degree or credential, enter 0.|
|MathPlacement|0 = Student is college ready<br>1 = Student is not college ready<br>-1 = Missing<br> <br>Format: Numeric|Student was determined to be college ready in math upon entry. Based on institution's standard math placement policies (e.g. placement determined by test scores, HS GPA, HS course taking and/or other institutional criteria).<br> <br>-1 = Missing is only used if the placement value is unknown, not if the student was exempt from placement testing, or tested at college level.|
|EngPlacement|0 = Student is college ready<br>1 = Student is not college ready<br>-1 = Missing<br> <br>Format: Numeric|Student was determined to be college ready in math upon entry. Based on institution's standard English placement policies (e.g. placement determined by test scores, HS GPA, HS course taking and/or other institutional criteria).<br> <br>-1 = Missing is only used if the placement value is unknown, not if the student was exempt from placement testing, or tested at college level.|
|GatewayMathStatus|0 = Gateway math course is not required of student at time of entry<br>1 = Gateway math course is required of student at time of entry<br>-1 = Missing<br> <br>Format: Numeric|Indicates whether the student is required to complete a gateway math course at time of first enrollment. Some students may be exempt from gateway math coursework, for example, those transferring from another institution where they completed the requirement, or students fulfilling the requirement by successful completion of AP, IB or similar high school coursework. Also, some majors/program areas may not require a gateway math course. Note: the course may be required to be completed during any term of enrollment and does not necessarily have to be completed in first term.|
|GatewayEnglishStatus|0 = Gateway English course is not required of student at time of entry<br>1 = GGateway English course is required of student at time of entry<br>-1 = Missing<br> <br>Format: Numeric|Indicates whether the student is required to complete a gateway English course at time of first enrollment. Some students may be exempt from gateway math coursework, for example, those transferring from another institution where they completed the requirement, or students fulfilling the requirement by successful completion of AP, IB or similar high school coursework. Also, some majors/program areas may not require a gateway English course. Note that the course may be required to be completed during any term of enrollment and does not necessarily have to be completed in first term.|

### Student Progress Data 
|Variable Name|Value Label|Definition|
|:-----------:|:----------|:---------|
|StudentID|Format: Alphanumeric; maximum length 75|Assigned by the institution, StudentID is the unique identifier used to identify a student. StudentID is required on all files containing student information. StudentID is to be consistent across all files and all years for each student. StudentID is treated as sensitive information: It will be encrypted in the database and only shown to authorized users—approved Coffey Data Team members and Frontier Set Site data providers approved by the Frontier Set Site to have access to the Frontier Set DMS--to identify problem records in uploaded files. <br> <br>Notes:<br>1. Leading and trailing empty spaces are ignored.<br>2. StudentID is case sensitive; “StudentOne” and “studentone” are treated as two different values.<br>3. StudentID is required for each student.|
|Cohort|2011-12<br>2012-13<br>2013-14<br>2014-15<br>2015-16<br>2016-17<br> <br>Format: YYYY-YY|Include all undergraduate students who attempted at least one course in a given term, for the first time at your institution. Students may be first-time ever in college or new transfer students into your institution and may be enrolled at any program level, including credential-seeking; college remedial, developmental, or college-preparatory; adult basic skills (ESL, ABE, or ASE/GED); and non-credit vocational students. For non-credit vocational students, only include those who enrolled in courses that could lead to an occupational certificate, industry certificate, or other type of credential of economic value, as well as those students who are simultaneously enrolled in credit-bearing courses.<br> <br>Also include:<br> * Past dual enrollment students who took a course or courses at your institution while simultaneously attending high school. <br>* Fall entry students who enrolled in summer work prior to first term of enrollment with credential-seeking status. Examples of summer work include, but are not limited to, summer bridge programs or developmental/remedial coursework. <br> <br>Exclude students who are: <br> *Non-credit vocational students enrolled in purely personal enrichment courses; <br> *Current dual enrollment students or those taking a course or courses at your institution while simultaneously attending high school. <br> <br> Report data for cohorts of first-time students for each term (including summer) in a given academic year, starting with the fall term of the 2011-12 academic year.<br> <br>Cohort must be assigned for each student.|
|Cohort Term|1 = Term 1 <br> 2 = Term 2 <br> 3 = Term 3 <br> 4 = Term 4 <br> 5 = Term 5 <br> 6 = Term 6 <br> 7 = Term 7 <br> <br>Format: Numeric|Cohort term of entry: Term student first enrolled in at least one course. See definition of cohort.<br> <br>CohortTerm must be assigned for each student.<br> <br> Term 1 = Fall term<br>Term 2 = Late fall or winter short/inter-sessions <br>Term 3 = Spring term for institutions on semester schedule; winter term for those on trimesters or quarters <br>Term 4 = Spring term for trimester/quarter institutions<br>Term 5 = Late winter or spring short/inter-sessions <br>Term 6 = Summer I <br>Term 7 = Summer II|
|Term|1 = Term 1 <br>2 = Term 2 <br>3 = Term 3 <br>4 = Term 4 <br>5 = Term 5 <br>6 = Term 6 <br>7 = Term 7<br> <br> Format: Numeric|Academic term the data reflect. Term must be assigned for each student.<br> <br> As determined by the Term Grid: Term 1 = Fall term<br>Term 2 = Late fall or winter short/inter-sessions <br>Term 3 = Spring term for institutions on semester schedule; winter term for those on trimesters or quarters <br>Term 4 = Spring term for trimester/quarter institutions<br>Term 5 = Late winter or spring short/inter-sessions <br>Term 6 = Summer I <br>Term 7 = Summer II
|AcademicYear|2011-12<br>2012-13<br>2013-14<br>2014-15<br>2015-16<br>2016-17<br> <br> Format: YYYY-YY|Academic year the data reflect. AcademicYear must be assigned for each student.
|CompleteDevMath|0 = Referred/placed, did not complete dev math coursework in this term<br>1 = Referred/placed, completed dev math coursework in this term<br>-1 = Missing<br>-2 = Does not apply, student not referred/placed in developmental math<br> <br> Format: Numeric|For students who were referred/placed into developmental math, report whether the student completed final developmental math requirement(s) during the term. The student need not have completed all of the requirements during this term, just the final requirement. Code as -2 if the student was not referred to or did not place into developmental math. <br> <br> If a student has previously been referred/placed, he/she should only be coded as “1” for the term file in which the student completes his/her final developmental education requirement. After he/she completes the final requirement, code the student as “0” in all future progress files.|
|CompleteDevEnglish|0 = Referred/placed, did not complete developmental English coursework during the current term<br>1 = Referred/placed, completed developmental English coursework during the current term<br>-1 = Missing<br>-2 =Does not apply, student not referred/placed in developmental English<br> <br> Format: Numeric|For students who were referred/placed into developmental English, report whether the student completed final developmental English requirement(s) during the term. The student need not have completed all of the requirements during this term, just the final requirement. Code as -2 if the student was not referred to or did not place into developmental English. <br> <br> If a student has previously been referred/placed, he/she should only be coded as “1” for the term file in which the student completes his/her final developmental education requirement. After he/she completes the final requirement, code the student as “0” in all future progress files.|
|Major1|See list of CIP Codes <br> 00.0000 = Undeclared<br> <br> -1 = Missing<br> <br> Format: Alpha; XX.XXXX|CIP (Classification of Instructional Programs) code of student's first major, as defined by the U.S. Department of Education. Provide the codes used by this institution. See “CIPCodes2010_25Feb2011.XLS” on the Frontier Set DMS for list of 2010 CIP Codes (www.IPNData.org, Documents). Or, go to http://nces.ed.gov/ipeds/cipcode/Default.aspx?y=55 for details and information about CIP codes, and a list of codes.|
|Major2|See list of CIP Codes <br> 00.0000 = Undeclared<br> <br> -1 = Missing<br> <br> Format: Alpha; XX.XXXX|CIP (Classification of Instructional Programs) code of student's second major, as defined by the U.S. Department of Education. Provide the codes used by this institution. See “CIPCodes2010_25Feb2011.XLS” on the Frontier Set DMS for list of 2010 CIP Codes (www.IPNData.org, Documents). Or, go to http://nces.ed.gov/ipeds/cipcode/Default.aspx?y=55 for details and information about CIP codes, and a list of codes.|
|Complete1|0 = None<br>1 = Certificate: less than 1 year, less than the AA level<br>2 = Certificate/Professional diploma: 1 to 2 years, less than the AA level<br>3 = Certificate: 2 to 4 years, less than the BA level<br>4 = AA<br>5 = AS<br>6 = AAS<br>7 = BA<br>8 = BS<br>9 = Post-BA certificate<br>10 = Master's degree<br>11 = Other undergraduate award<br>12 = Other graduate award<br> <br> Format: Numeric|Highest award received by the student during the current term at the Frontier Set institution, if any. If no award earned during current term, enter 0. <br> <br> Note: Code positive values only for the term the credential was awarded. Code 0 (none) in terms where no award was conferred.|
|Complete2|0 = None<br>1 = Certificate: less than 1 year, less than the AA level<br>2 = Certificate/Professional diploma: 1 to 2 years, less than the AA level<br>3 = Certificate: 2 to 4 years, less than the BA level<br>4 = AA<br>5 = AS<br>6 = AAS<br>7 = BA<br>8 = BS<br>9 = Post-BA certificate<br>10 = Master's degree<br>11 = Other undergraduate award<br>12 = Other graduate award<br> <br> Format: Numeric|If the student received more than one award in the given term, this is the second highest award received by the student during the term at the Frontier Set institution. If none, enter 0.<br> <br> Note: Code positive values only for the term the credential was awarded. Code 0 (none) in terms where no award was conferred.|
|CompleteCIP1|Continuous<br> <br> -1 = Missing<br>-2 = Does not apply<br> <br> Format: Alpha, XX.XXXX|Provide the codes used by this institution. See “CIPCodes2010_25Feb2011.XLS” on the Frontier Set DMS for lists of the 2010 CIP Codes (www.IPNData.org, Documents). Or, go to http://nces.ed.gov/ipeds/cipcode/Default.aspx?y=55 for details and information about CIP codes, and a list of codes.<br> <br> For students with a double major, or receiving multiple awards in a term, code the CIP code associated with Complete1 here.<br> <br> In the unusual case where the student’s field of award is unknown, code as -1 = Missing.<br> <br> If the student did not receive an award during the term, code as -2 = Does not apply.|
|CompleteCIP2|Continuous<br> <br> -1 = Missing<br>-2 = Does not apply<br> <br> Format: Alpha, XX.XXXX|CIP (Classification of Instructional Programs) code of the field in which the student received his or her second highest award, as defined by the U.S. Department of Education. Provide the codes used by this institution. See “CIPCodes2010_25Feb2011.XLS” on the Frontier Set DMS for lists of the 2010 CIP Codes (www.IPNData.org, Documents). Or, go to http://nces.ed.gov/ipeds/cipcode/Default.aspx?y=55 for details and information about CIP codes, and a list of codes.<br> <br> For students with a double major, or receiving multiple awards in a term, code the CIP code associated with Complete2 here.<br> <br> In the unusual case where the student’s field of award is unknown, code as -1 = Missing.<br> <br> If the student has just one major, code as -2 = Does not apply.|
|TransferIntent|0 = Intent unknown<br>1 = No intent to transfer<br>2 = Intent to transfer<br>-1 = Missing<br>-2 = Not collected this term<br> <br> Format: Numeric|Student's educational objective.<br> <br> Institutions able to report term-by-term should do so.<br> <br> Code 0 = Intent unknown if the student stated that his/her intention is not known. Code -1 = missing if the institution does not have the information.<br> <br> Institutions collecting student intent once a year, report on the initial entry term, and on the subsequent applicable term file when intent is asked again. Report -2 = Not collected this term during all other terms.<br> <br> Institutions collecting student intent only upon student entry, report on the corresponding term file at time of entry. Report -2 = Not collected this term during all other terms.|
|DegreeTypeSought|1 = Non-degree<br>2 = Less than 1-year certificate, less than AA<br>3 = 1-2 year certificate, less than AA<br>4 = 2-4 year certificate, less than BA<br>5 = Associate’s degree<br>6 = Bachelor's degree<br>-1 = Missing<br> <br>Format: Numeric|Degree that the student is currently seeking.|
|TermGPA|Continuous<br>-1 – Missing<br> <br>Format: Numeric, X.XX|Student’s grade point average earned for the current term. Based on credits used toward student’s credential and reported on a 4-point scale.<br> <br>Count pass/fail classes, Ds, and retakes in the manner used for student's credential.<br> <br>Include transferred-in courses if they are included in student's GPA for credential.|
|CumGPA|Continuous<br>-1 - Missing<br> <br>Format: Numeric, X.XX|Student’s cumulative grade point average earned for all terms, up to and including the current term. Based on credits used toward student’s credential and reported on a 4-point scale.<br> <br>Count pass/fail classes, Ds, and retakes in the manner used for student's credential.<br> <br>Include transferred-in courses if they are included in student's GPA for credential.|

## Contributing 
As we navigate the complexities of data analytics, we've encountered challenges that underscore the pivotal role of data cleaning and feature engineering in predictive modeling. Recognizing these challenges, we invite contributions from the community to enhance our project's data wrangling processes, exploratory data analysis (EDA), imputation strategies, and feature engineering. Here are the potential areas for improvement:

- **Data Merging:** We've identified that retaining only data from the final semester may lead to information loss. Alternative methods for merging data could provide a more holistic view of student performance over time.
- **Exploratory Data Analysis (EDA):** Our EDA phase, particularly the interpretation of heatmaps, highlighted areas of confusion. Insights into better leveraging these analyses for data cleaning and understanding would be invaluable.
- **Imputation of Missing Data:** Our approach to handling missing data, especially for sensitive columns like race, needs refinement. We are looking for more sophisticated imputation methods and thoughtful consideration of how to address these gaps.
- **Feature Engineering:** There is always room for engineering more features. Innovative ideas for new features that could improve the prediction models are highly encouraged.

Your contributions can make a real difference in refining our codes, improving our project's predictive capabilities, and providing new insights into data analytics. We're excited to see the diverse ideas and expertise our community brings to this endeavor.

## Final Thoughts 
1. **Which metadata standard did you choose and why?**\
   
   Data Documentation Initiative (DDI) was chosen for this README file for several reasons, incluidng but not limited to:
  - DDI allows for detailed documentation of datasets, including study design, data collection methods, questionnaires, and data files.
  - DDI covers the entire lifecycle of data, from planning and collection to preservation and reuse. This holistic approach ensures that data is well-managed and accessible over the long term.
  - By adhering to a widely recognized standard, DDI facilitates data sharing and interoperability between different systems and platforms. 
2. **Which template/software did you use?**
  - This README file was written by following the content guidelines recommended by Cornell University. 
  - In writing the README, GitHub was used as the platform of choice due to its user-friendly interface, its widespread use in the coding and data science communities, and the abundance of examples it hosts. 
3. **What was the most challenging part of creating a ReadME file?**
  - Deciding what tool to use to write the README file took me some time. There are so many options in terms of application and online tools, so I navigated through them and finally decided to use GitHub.
  - Determining the appropriate level of detail for the README was a complex task. In particular, delineating our data preprocessing steps required striking a delicate balance. This phase involves numerous processes, and it was challenging to describe them in a way that was both thorough and succinct.
  - As this was a Kaggle competition project, the licensing of the data was unclear. Efforts to trace the data back to the original collector for clarification on licensing were unsuccessful.
  - These datasets were accompanied by an extensive data dictionary handbook. However, since attaching the handbook directly was not feasible, I had to integrate all the pertinent information into this file manually.
  - Learning Markdown was a new experience, requiring me to frequently consult various resources for syntax guidance.

## References 
Coffey Consulting. (2017, Janurary). 2011-2017 cohorts financial aid and fafsa data. Retrieved February 19th, 2024 from https://www.kaggle.com/competitions/hudk-4050-student-dropout-prediction-challenge-f23/data <br>
Coffey Consulting. (2017, Janurary). Student progress data. Retrieved February 19th, 2024 from https://www.kaggle.com/competitions/hudk-4050-student-dropout-prediction-challenge-f23/data <br>
Coffey Consulting. (2017, Janurary). Student static data. Retrieved February 19th, 2024 from https://www.kaggle.com/competitions/hudk-4050-student-dropout-prediction-challenge-f23/data <br>
Cornell Data Service (n.d.). *Guide to Writing “Readme” Style Metadata*. Cornell University. https://data.research.cornell.edu/data-management/sharing/readme/#1-recommended-content
