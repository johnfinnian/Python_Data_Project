# Overview

Welcome to my analysis of the data job market, focusing on data analyst roles. This project was created out of a desire to navigate and
understand the job market more effectively. It delves into the top-paying and in-demand skills to help find optimal job opportunities for
data analysts.

The data sourced from Luke Barousse's Python Course which provides a foundation for my analysis, containing detailed information on
job titles, salaries, locations, and essential skills. Through a series of Python scripts, I explore key questions such as the most demanded
skills, salary trends, and the intersection of demand and salary in data analytics.

# The Questions

Below are the questions I want to answer in my project:

1. What are the skills most in demand for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for data analysts to learn? (High Demand AND High Paying)


# Tools I Used

For my deep dive into the data analyst job market, I harnessed the power of several key tools:

- Python: The backbone of my analysis, allowing me to analyze the data and find critical insights.I also used the following Python
libraries:
o Pandas Library: This was used to analyze the data.
- Matplotlib Library: I visualized the data.
Seaborn Library: Helped me create more advanced visuals.

- Jupyter Notebooks: The tool I used to run my Python scripts which let me easily include my notes and analysis.
- Visual Studio Code: My go-to for executing my
ing my Python scripts.

- Git & GitHub: Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.


# Data Preparation and Cleanup

This section outlines the steps taken to prepare the data for analysis, ensuring accuracy and usability.

## Import & Clean Up Data

I started by importing necessary libraries and loading the dataset, followed by initial data cleaning tasks to ensure
data quality.


# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skils i should pay attention to depending on the role I'm targeting.

View my notebook with details steps here:
[2_Skill_Demand.ipynb](3_Project\2_Skill_Demand.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skills_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
  
plt.show()

```
### Results

![Visualization of Top Skills for Data Nerds](images\skill_demand_all_data_roles.png)


### Insights
- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists(72%) and Data Engineers(65%).
- SQL is the most requested skill for Data Analyst and Data Scientists, with it in over half the job postings for both roles. For Data Engineers, python is the most sought-after skill, appearing in 68% of job postings.
- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).


## 2. How are in-demand skills trending for Data Analysis?

```
sns.lineplot(data=df_plot, dashes=False, palette='tab10' )

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()

```

### Results

![Trending Top Skills for Data Analysts in the US](skill_trend_DA.png)

*Bar graph visualizing the trending top skills for data analysts in the US in 2023.*

### Insights:
- SQL remains the most consistently demanded skill throughout the year, although it shows a gradual decrease in demand. 

- Excel experienced a significant increase in demand starting around September, surpassing both Python and Tableau show relatively stable demand throughout the year with soome fluctuations but remain essential skills for data analysts.
- Power BI, while less demanded compared to the others, shows a slight upward trend towards the year's end.

## 3. How will do jobs and skills pay for Data Analysts?

### Salary Analysis for Data Nerds in US

### Visualize Data

```python
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)

sns.set_theme(style='ticks')
plt.title('Salary Distribution in the United States')
plt.xlabel('Yearly Salary ($USD)')
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}k'))
plt.xlim(0, 600000)
plt.show()

```

### Results

![Salary Distributions of Data Jobs in the US](salary_boxplot.png)
*Box plot visualizing the salary distributions for the top 6 data job titles.*

### Insights

- There is a significant variations in salary ranges across different job_titles. Senior Data Scientist positions tend to have the highest salary potential, with uo to $600k, indicating the high value placed on advanced data skills and experience in the industry.

- Senior Data Engineer and Senior Data Scientist roles show a considerable number of outliers on higher end of the salary spectrum, suggesting that exceptional skills or circumstances can lead Analyst roles demonstrate more consistency in salary, with fewer outliers.

- The median salaries increase with the seniority and specialization of the roles. Senior roles(Senior Data Scientist, Senior Data Engineer) not only have higher median slaries but also larger differences in typical salaries, reflecting greater variance in compensation as responsibilities increase.


### Highest Paid & Most Demanded Skills for Data Analysts

### Visualize Data


```python

fig, ax = plt.subplots(2, 1)


# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, ax=ax[0], hue='median', palette='dark:b_r')

# Top 10 Most In-Demand Skills for Data Analysts
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, ax=ax[1], hue='median', palette='light:b')

plt.show()

```

### Results
in-demand skills for data analysts in the US:

![The Highest Paid & Most In-Demand Skills for Data Analyst in the US](images\US_highest_paying_and_in_demand_skills.png)
*Two separate bar graphs visualizing the highest paid skills and most in-demand skills for data analysts in the US.*


### Insights:

- The top graph shows specialized technical skills like 'dply', 'Bitbucket', and 'Gitlab' are associated with higher salaries, some reaching up to $200k, suggsting that advanced techinical proficiency can increase earning potential.

- The botton graph highlights that foundational skills like 'Excel', 'PowerPoint', and 'SQL' are the most in-demand, even though they may not offer the highest slaries. The demostrates the importance of these core skills for employablility in data analysis roles.

- There's a clear distinction between the skills that are highest paid and those that are most in-demand. Data analysts aiming to maximize their career potential should consider developing a diverse skill set that includes both high-paying specialized skills and widely demanded foundational skills.


## 4. What is the most optimal skills to learn for Data Analysts?

### Visualize Data

```python
from adjustText import adjust_text
import matplotlib.pyplot as plt

plt.scatter(df_DA_skills_high_demand['skill_percent'], df_DA_skills_high_demand['median_salary'])
plt.show()

```

### Results

![Most Optimal Skills for Data Analysts in the US](images\US_Most_Optimal_Skills_for_Data_Analysts.png)
*A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in the US.*

### Insights:
- The scatter plot shows that most of the 'programming' skills (colored blue) tend to cluster at higher salary levels compared to other categories, indicating that programing expertise might offer greater salary benefits within the data analytics field.

- Analyst tools (colored green), including Tableau and Power BI, are prevent in job postings and offer comptitive salaries, showing that visualization and data analysis software are crucial for current data roles. This category not only has good salaries but is also versatile across different types of data tasks.

- The database skills (colored orange), such as Oracle and SQL Server, are associated with some of the highest salaries among data analysts tools.
This indicates a significant demand and valuation for data management and manipulation expertise in the industry.


# Insights

This project provided several general insights into the data job market for analysts:

- Skill Demand and Salary Correlation: There is a clear correlation between the demand for specific skills and the salaries these
skills command. Advanced and specialized skills like Python and Oracle often lead to higher salaries.
- Market Trends: There are changing trends in skill demand, highlighting the dynamic nature of the data job market. Keeping up with
these trends is essential for career growth in data analytics.
- Economic Value of Skills: Understanding which skills are both in-demand and well-compensated can guide data analysts in
prioritizing learning to maximize their economic returns.


# Challenges I Faced

This project was not without its challenges, but it provided good learning opportunities:

 - Data Inconsistencies: Handling missing or inconsistent data entries requires careful consideration and thorough data cleaning and preprocessing techniques to ensure the integrity of the analysis.

 - Complex Data Visualization: Designing effective visual representations of complex datasets was challenging, but crucial for conveying insights clearly and compellingly.

 - Balancing Breadth and Depth:Deciding how deeply to dive into each analysis while maintaining a broad overview of the data landscape required constant balancing to ensure comprehensive coverage without getting lost in details.
 

# Conclusion

This exploration into the data analyst job market has been incredibly informative, highlighting the critical skills and trends that shape this evolving field. The insights I got enhance my understanding and provide actionable guidance for anyone looking to advance their career in data analytics. As the market continues to change, ongoing analysis will be essential to stay ahead in data analytics. This project is a good foundation for future explorations and underscores the importance of continuous learning and adaptation in the data field.
