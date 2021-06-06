# School_District_Analysis
#### Analysis on School District SAT scores using pandas library. 

## Overview 

In this project I will be helping the State's Board of Education analyze data on student funding and SAT scores. The goal will be to uncover trends on student's performance and funding in order to reallocate the budget appropriately. 

## Resources
- Data sources:
  - schools_complete.csv
  - students_complete.csv
- Software:
  - Python 3.6.1
  - Jupyter Notebook
  - Pandas and NumPy Libraries

## Analysis

The first thing I needed to do was clean the data. This process consisted of two steps. First, I noticed that some of the students had professional prefixes and suffixes. So, I fixed it using the `replace()` method as follows:
```
prefixes_suffixes = ["Dr. ", "Mr. ","Ms. ", "Mrs. ", "Miss ", " MD", " DDS", " DVM", " PhD"]

for word in prefixes_suffixes:
    student_data_df["student_name"] = student_data_df["student_name"].str.replace(word,"")
```

And second, I noticed the data evidenced academic dishonesty in the results of 9th graders at Thomas High School. Thus, I replaced their math and reading scores with NaNs while keeping the rest of the data intact. I will be addressing later on how this changes affected the overall analysis. 
```
student_data_df.loc[(student_data_df["grade"] == "9th") & (student_data_df["school_name"] == "Thomas High School"),["reading_score"]] = np.nan

student_data_df.loc[(student_data_df["grade"] == "9th") & (student_data_df["school_name"] == "Thomas High School"),["math_score"]] = np.nan
```

## Results


