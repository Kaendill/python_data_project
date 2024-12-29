# Analysis
## 1. What are the most in-demand skills for the 3 most popular data jobs in Nigeria?

to achieve this, I filtered out the most popular data job roles from the dataset, for the particular country in focus, which is Nigeria, and then, obtained the top skills in demand for these roles.
This query highlights the most popular job titles and the top skills in demand for these job roles, for anyone focusing on any of these job roles, this query gives an insight into what skills emphasis should be placed on.


Take a look at my detailed notebook here: 
[2_skills_demand.ipynb](3_Project/2_skills_demand.ipynb)


## Visualize my data

``` python
plt.figure(figsize= (15,6))
fig, ax= plt.subplots(len(job_titles), 1)
sns.set_theme(style= 'ticks')
for i, job_title in enumerate(job_titles):
    df_plot = df_skill_perc[df_skill_perc['job_title_short'] == job_title].head(5)
    sns.barplot(df_plot, x='skills_percent', y= 'job_skills', hue= 'skills_count', palette='dark:r_r', ax=ax[i])

plt.show()
```    
### Results

![Visualization of in-demand skills for top3 data roles in Nigeria](3_Project\image\skills_demand.png)

### Top Insights
- Though their importance varies, Python and SQL are central across roles and critical for all three roles.
- Data Analysts align with visualization tools (Tableau, Power BI).  Learn Excel, Tableau, and Power BI for reporting.
- Data Engineers focus on cloud and orchestration tools (AWS, Kafka, Airflow). Dive into cloud platforms and workflow automation.
- Data Scientists emphasize statistical and data modelling tools (R, SAS). Gain proficiency in R, statistical modelling, and machine learning.
