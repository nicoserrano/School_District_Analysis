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

Before going into the actual analysis of the data with the NaNs for 9th graders at Thomas H.S., I expected some slight but not significant changes in the results. NaN (Not a Number) errors can be tricky. Even though they can be used to perform additions and averages, they might be a problem when trying to multiply or divide. In this case, I knew they were not going to affect my approach as they were just going to be dismissed when trying to calculate the average math and reading scores for each grade and school. Again, before going through everything I expected no major differences but we will se what happened in the results section. 

## Results

- How is the district summary affected?

*Old District Summary:*
![Screen Shot 2021-06-06 at 6 45 09 PM](https://user-images.githubusercontent.com/83378141/120942511-62199e80-c6f7-11eb-9449-9b4cda443db9.png)

*New District Summary:*
![Screen Shot 2021-06-06 at 6 43 08 PM](https://user-images.githubusercontent.com/83378141/120942472-27b00180-c6f7-11eb-81a3-908381092b00.png)

As we can observe, there is a slight difference in the results for the district summary. The academic dishonesty of 9th graders at Thomas High School made the average go up by a little. Nevertheless, once I replaced their results with NaNs it can be seen that the average scores, passing percentages and overall passing percentages went down by no more than 0.3. In conclusion, as the district summary is such a broad analysis it was not affected significantly. 

- How is the school summary affected? 

*Old School Summary:*
![Screen Shot 2021-06-06 at 7 16 54 PM](https://user-images.githubusercontent.com/83378141/120943334-41a01300-c6fc-11eb-8090-23d3cdfd5cf8.png)

*New School Summary:*
![Screen Shot 2021-06-06 at 7 17 42 PM](https://user-images.githubusercontent.com/83378141/120943341-449b0380-c6fc-11eb-8ed6-5dbd61a39725.png)




