# The Analysis
Each Jupyter notebook for this project aimed at investigating specific aspects of the data job market. Here’s how I approached each question:
## 1. What are the most demanded skills for the top 3 most popular data roles?
To identify the most in-demand skills across the three most popular data roles, I first filtered the dataset to focus on the most common positions. Then, I extracted the top five skills associated with each of these roles. This analysis highlights the key job titles and their most relevant skills, helping me understand which competencies to prioritize based on the role I aim to pursue.
View my notebook with detailed steps here: [2_Skill_Demand](3_Project/2_Skill_Demand.ipynb)
### Visualize Data
```
fig, ax = plt.subplots(len(job_titles), 1)


for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

plt.show()
```
### Results
![Visualisation of Top Skills for Data Analyst in France](3_Project/images/skill_demand_data_roles.png)
Bar chart illustrating the salaries for the top three data roles, along with the five key skills associated with each of them.
### Insights:
- SQL is a core skill across all three roles, ranking at or near the top every time, making it essential regardless of the data career path.
- Data Engineers stand out with more technical and infrastructure-focused requirements, including tools like Spark and cloud platforms (AWS, Azure), showing a stronger emphasis on big data and system architecture.
- Python is key for Data Scientists and Data Engineers, while Data Analysts rely more on business intelligence tools like Power BI, Tableau, and Excel, reflecting a more business-oriented role.
