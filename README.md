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

![Screen Shot 2021-06-07 at 10 13 42 PM](https://user-images.githubusercontent.com/83378141/121111986-c6af2900-c7dd-11eb-80a8-cb71dd79d3e9.png)

*Old School Summary:*
![Screen Shot 2021-06-06 at 7 16 54 PM](https://user-images.githubusercontent.com/83378141/120943334-41a01300-c6fc-11eb-8090-23d3cdfd5cf8.png)

*New School Summary:*
![Screen Shot 2021-06-06 at 7 17 42 PM](https://user-images.githubusercontent.com/83378141/120943341-449b0380-c6fc-11eb-8ed6-5dbd61a39725.png)

As it can be seen, the NaN generated a significant increase in the passing percentages for math, reading, and overall. This was due to the fact that 9th graders at Thomas High School had a considerably high amount of students who didn't pass the math or reading exams. Even though there was academic dishonesty, 9th graders were making that percentage of students who passed remain very low in the 60s %. After their scores got replaced with NaN, and therefore dismissed in the analysis, the percentage of passing students increased up to the 90s % as the rest of the school performed mostly above the passing grade of 70. 

- How does replacing the ninth graders’ math and reading scores affect Thomas High School’s performance relative to the other schools?

![Screen Shot 2021-06-07 at 10 42 29 PM](https://user-images.githubusercontent.com/83378141/121114472-bdc05680-c7e1-11eb-8900-e7078791e5dc.png)

In comparison to other schools, after replacing the 9th graders with NaNs Thomas High School's results became a lot better. The average scores were still pretty similar, but the passing percentages were at the top. These are the top 5 schools of the district:

![Screen Shot 2021-06-07 at 10 44 11 PM](https://user-images.githubusercontent.com/83378141/121114578-f102e580-c7e1-11eb-82e3-8028ac7de509.png)

As we can see above, it reached the 2nd place out of the 15 schools in the district with a overall passing percentage of 90.63%. This meant that 90.6% of the entire high school (excluding 9th graders because of academic dishonesty) had a score above 70 for both math and reading. 

- How does replacing the ninth-grade scores affect the following:
  - Math and reading scores by grade

![Screen Shot 2021-06-07 at 11 28 01 PM](https://user-images.githubusercontent.com/83378141/121118599-20b4ec00-c7e8-11eb-8789-0b37b119357f.png)
![Screen Shot 2021-06-07 at 11 28 11 PM](https://user-images.githubusercontent.com/83378141/121118606-23afdc80-c7e8-11eb-8fb4-7a66f0f850c8.png)

First we have the math average scores per grade followed by the reading scores per grade for each school. In this case, the NaNs did not affect our results at all, they were just displayed as an error for ninth graders at Thomas High School. The rest of the data remained intact. 

  - Scores by school spending

![Screen Shot 2021-06-07 at 11 33 11 PM](https://user-images.githubusercontent.com/83378141/121119005-d8e29480-c7e8-11eb-9043-1537982d8cf6.png)

These are the results categorized by the budget per student, meaning the money that the school is theoretically investing on each student. In this situation, the NaNs do not affect the results at all. This is due to the fact that there are a couple of other schools that are categorized in this same per student budget, not affecting the average scores and passing percentages considerably. The per student budget was a calculation made by dividing the school budget by the number of students in it. Thomas High School still has 1,635 students and a $1,043,130 budget making them be part of the third per student budget interval with $638 dollars. 

  - Scores by school size

![Screen Shot 2021-06-07 at 11 33 22 PM](https://user-images.githubusercontent.com/83378141/121120386-7343d780-c7eb-11eb-8269-1f03239ce7af.png)

Again, Thomas High School kept on having 1,635 students which makes them a medium sized along with other 4 more schools. By replacing the ninth graders scores with NaNs the data is almost untouched. There is no significant changes in the results for this category.

  - Scores by school type

![Screen Shot 2021-06-07 at 11 33 33 PM](https://user-images.githubusercontent.com/83378141/121121699-13026500-c7ee-11eb-8b96-10b4bf73c7d7.png)

And last but not least, the results for the school type did not change at all. This was due to the fact that Thomas High School was categorized in the Charter school type along other 7 schools. Their ninth graders were just a small group relative to all the students in Charter schools, making the overall results stay untouched. 

## Summary





