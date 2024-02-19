# README File for Student Dropout Prediction Project 
**IndividualAssignment2_HUDK4052_YueSummerWu**

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

### Financial Aid Data 
This Excel dataset encompasses an array of financial aid information for students spanning from 2012 to 2017. It is structured to provide a multi-dimensional view of financial aid distribution through various lenses including: 
- Demograhics such as marital status.
- Adjusted income information including adjusted gross income and parent adjusted gross income.
- Parents' highest degree
- Housing status, on campus, off campus, or with parents
- Amount of loans received from 2012 to 2017
- Amount of scholarship received from 2012 to 2017
- Amount of federal work study received from 2012 to 2017

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

## Data Dictionary 
### Financial Aid Data 
|Variable Name|Value Label|Definition|
|:------------|:----------|:---------|
|ID with leading|Format: Alphanumeric; maximum length 75|Assigned by the institution, StudentID is the unique identifier used to identify a student. StudentID is required on all files containing student information. StudentID is to be consistent across all files and all years for each student. StudentID is treated as sensitive information: It will be encrypted in the database and only shown to authorized users—approved Coffey Data Team members and Frontier Set Site data providers approved by the Frontier Set Site to have access to the Frontier Set DMS--to identify problem records in uploaded files.|
|cohort|2011-12<br>2012-13<br>2013-14<br>2014-15<br>2015-16<br>2016-17<br> <br>Format: YYYY-YY|Include all undergraduate students who attempted at least one course in a given term, for the first time at your institution. Students may be first-time ever in college or new transfer students into your institution and may be enrolled at any program level, including credential-seeking; college remedial, developmental, or college-preparatory; adult basic skills (ESL, ABE, or ASE/GED); and non-credit vocational students. For non-credit vocational students, only include those who enrolled in courses that could lead to an occupational certificate, industry certificate, or other type of credential of economic value, as well as those students who are simultaneously enrolled in credit-bearing courses.<br> <br>Also include:<br> * Past dual enrollment students who took a course or courses at your institution while simultaneously attending high school. <br>* Fall entry students who enrolled in summer work prior to first term of enrollment with credential-seeking status. Examples of summer work include, but are not limited to, summer bridge programs or developmental/remedial coursework. <br> <br>Exclude students who are: <br> *Non-credit vocational students enrolled in purely personal enrichment courses; <br> *Current dual enrollment students or those taking a course or courses at your institution while simultaneously attending high school. <br> <br> Report data for cohorts of first-time students for each term (including summer) in a given academic year, starting with the fall term of the 2011-12 academic year.<br> <br>Cohort must be assigned for each student.|
|cohortterm|1 = Term 1 <br> 2 = Term 2 <br> 3 = Term 3 <br> 4 = Term 4 <br> 5 = Term 5 <br> 6 = Term 6 <br> 7 = Term 7 <br> <br>Format: Numeric|Cohort term of entry: Term student first enrolled in at least one course. See definition of cohort.<br> <br>CohortTerm must be assigned for each student.<br> <br> Term 1 = Fall term<br>Term 2 = Late fall or winter short/inter-sessions <br>Term 3 = Spring term for institutions on semester schedule; winter term for those on trimesters or quarters <br>Term 4 = Spring term for trimester/quarter institutions<br>Term 5 = Late winter or spring short/inter-sessions <br>Term 6 = Summer I <br>Term 7 = Summer II
### Student Static Data 
### Student Progress Data 





