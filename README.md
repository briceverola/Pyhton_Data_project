# The Analysis
Each Jupyter notebook for this project aimed at investigating specific aspects of the data job market. Here’s how I approached each question:
## 1. What are the most demanded skills for the top 3 most popular data roles?
To identify the most in-demand skills across the three most popular data roles, I first filtered the dataset to focus on the most common positions. Then, I extracted the top five skills associated with each of these roles. This analysis highlights the key job titles and their most relevant skills, helping me understand which competencies to prioritize based on the role I aim to pursue.

View my notebook with detailed steps here: [2_Skill_Demand](3_Project/2_Skill_Demand.ipynb)
#### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)


for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

plt.show()
```
#### Results
![Visualisation of Top Skills for Data Analyst in France](3_Project/images/skill_demand_data_roles.png)

Bar chart illustrating the salaries for the top three data roles, along with the five key skills associated with each of them.
#### Insights:
- SQL is a core skill across all three roles, ranking at or near the top every time, making it essential regardless of the data career path.
- Data Engineers stand out with more technical and infrastructure-focused requirements, including tools like Spark and cloud platforms (AWS, Azure), showing a stronger emphasis on big data and system architecture.
- Python is key for Data Scientists and Data Engineers, while Data Analysts rely more on business intelligence tools like Power BI, Tableau, and Excel, reflecting a more business-oriented role.

## 2. How are in-demand skills trending for Data Analysts?

To analyze how skills evolved throughout 2023 for Data Analysts, I filtered the dataset to include only relevant roles and grouped the required skills by the posting month. This allowed me to identify the top five skills for each month, highlighting how their popularity changed over the year.

View my notebook with detailed steps here: [3_Skills_Trend](3_Project/3_Skills_Trend.ipynb).

#### Visualize Data

```python
df_plot = df_DA_FR_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, legend=False, palette='tab10')

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()
```
#### Results
![Trending top skills for DA in france over time](3_Project/images/skill_trend_DA.png)
*Bar graph visualizing the trending top skills for data analysts in France in 2023.*

#### Insights
- SQL remains the most consistently in-demand skill across all months, maintaining a high level throughout the year with noticeable peaks in summer and early autumn. This confirms its central role in Data Analyst positions in France.
- Python follows a similar pattern but with slightly more variation, reaching a strong peak in summer. This suggests an increased demand for more advanced analytical and technical skills during that period.
- BI tools (Power BI and Tableau) show moderate but stable demand, with occasional increases during mid-year. This indicates they are regularly required but less dominant compared to core technical skills like SQL and Python.
- Excel remains relatively stable at a lower level, suggesting it is a baseline skill expected across roles rather than a key differentiator in the job market.

## 3. How well do jobs and skills pay for Data Analysts?
To identify the highest-paying roles and skills, I focus on major European data markets (United Kingdom, Germany, France, and the Netherlands) and analyze median salaries to ensure robust comparisons.  

But first I examine the salary distribution of common data roles such as Data Analyst, Data Engineer, and Data Scientist to understand overall compensation differences.  
This provides a foundation for identifying which roles and skills offer the highest earning potential.

View my notebook with detailed steps here: [4_Salary_Analysis](3_Project/4_Salary_Analysis.ipynb)

#### Visualiza Data

```python
sns.boxplot(data=df_EU_top6, x='salary_year_avg', y='job_title_short', order=job_order)

ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
``` 
#### Results
![salary distibution for data roles](3_Project/images/salary_distribution_data.png)

*Box plot visualizing the salary distributions for the top 6 data job titles.*

#### Insights

- There is a clear difference in salary levels across data roles in Europe, with senior positions such as Senior Data Engineer and Senior Data Scientist offering the highest median salaries. This reflects the strong value placed on experience and advanced technical expertise.
- Technical roles such as Data Engineer, Machine Learning Engineer, and Data Scientist show higher salary ranges and greater variability compared to Data Analyst roles. This indicates that more specialized and technical positions tend to offer both higher pay and a wider range of compensation.
- Senior roles exhibit a larger spread in salaries, with several high-end outliers, suggesting that compensation can vary significantly depending on experience, company, and responsibilities. In contrast, Data Analyst roles show more consistent and concentrated salary ranges, indicating less variability in compensation.

### Highest Paid & Most Demanded Skills for Data Analysts

Next, I narrow the analysis to Data Analyst roles across selected European countries (United Kingdom, Germany, France, and the Netherlands).  

#### Visualize Data

```python
fig, ax = plt.subplots(2, 1)  

# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue='median', ax=ax[0], palette='dark:b_r')

# Top 10 Most In-Demand Skills for Data Analysts
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='light:b')

plt.show()
```

#### Results 
![top skills and salary for data analyst](3_Project/images/skills_salary_analysis.png)

*Two separate bar graphs visualizing the highest paid skills and most in-demand skills for data analysts in top European countries.*

### Insights

- The top chart shows that more specialized and technical skills such as Terraform, Kafka, and MongoDB are associated with the highest salaries, suggesting that advanced infrastructure and data engineering-related skills can significantly increase earning potential for Data Analysts.
- The bottom chart highlights that foundational and widely used tools like Python, SQL, and Excel are the most in-demand skills. These skills are essential for employability, even if they are not always linked to the highest salaries.
- There is a clear gap between the highest-paying skills and the most in-demand ones. This suggests that Data Analysts can benefit from combining strong core skills (Python, SQL) with more specialized tools to maximize both job opportunities and salary potential.