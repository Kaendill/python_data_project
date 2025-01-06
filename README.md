# Project Overview

### Objective:
The goal of this project is to analyze data analytics roles and skills, focusing on salary trends, in-demand expertise, and their alignment with industry requirements. By synthesizing insights, this project aims to guide professionals in optimizing their skill sets to enhance career prospects and earning potential.


# Questions Asked

Focusing on the UK (size and availabilty in the dataset)
1.  What are the Most In-demand skills for top 3 data roles?
2. How are these in-demand skills trending for Data Analysts?
3. How jobs and skills pay for Data Analyst roles?
4. What is(are) the  most Optimal skill(s) to learn for Data Analysis (Based on High Demand and High pay)?

# Tools Used

- Data Source : Insights were derived using datasets from Luke Barousse's Hugging Face repository, which consisted of columns such as `job_title`, `salary_year_avg`, `job_skills`, among others.
- Jupyter Notebook: Served as the platform for running Python scripts, visualizing outputs, and documenting insights seamlessly.
- Python Libraries for Data Analysis and Visualization, these include:
- `Pandas`: Used for data manipulation, cleaning, and analysis to handle datasets efficiently.
- `Matplotlib`: Employed to create a range of visualizations, including scatter plots, bar charts, and line graphs.
- `Seaborn`: Utilized for advanced, aesthetically pleasing plots such as boxplots and trend charts, enhancing data storytelling.

# Analysis
## 1. What are the most in-demand skills for the 3 most popular data jobs in Nigeria?

To achieve this, I filtered out the most popular data job roles from the dataset, for the particular country in focus, which is Nigeria, and then, obtained the top skills in demand for these roles.
This query highlights the most popular job titles and the top skills in demand for these job roles, for anyone focusing on any of these job roles, this query gives an insight into what skills emphasis should be placed on.


Take a look at my detailed notebook here: 
[2_skills_demand.ipynb](3_Project\2_skills_demand.ipynb)
## Visualize my data

``` python
plt.figure(figsize= (15,6))
fig, ax= plt.subplots(len(job_titles), 1)
sns.set_theme(style= 'ticks')
for i, job_title in enumerate(job_titles):
    df_plot = df_skill_perc[df_skill_perc['job_title_short'] == job_title].head(5)
    sns.barplot(df_plot, x='skills_percent', y= 'job_skills', hue= 'skills_count', palette='dark:r_r', ax=ax[i] )
    ax[i].set_ylabel('')
    ax[i].legend().set_visible(False)
    ax[i].set_title(job_title)
    ax[1].set_xlabel('')
    ax[i].set_xlim(0,70)

plt.show()
```    
### Results

![Visualization of in-demand skills for Top 3 data roles in The Uk]()
### Top Insights
- ``SQL`` and `Python` are critical across all roles, with `SQL` dominating for Data Analysts (43%) and Engineers (60%), while Python leads for Data Scientists (69%).
- `Excel`, `Power BI`, and `Tableau` are key for Data Analysts, highlighting the focus on data visualization and reporting.
- Cloud Skills (`AWS`, `Azure`) are vital for Data Engineers and Data Scientists, reflecting the demand for big data and cloud computing expertise.


## 2. How Are In-Demand Skills trending for Data Analysts?

### Visualize My Data

```python

plt.figure(figsize= (10,6))
sns.set_theme(style= 'ticks')
df_plot= DA_percent.iloc[:, :5]
sns.lineplot(df_plot, palette= 'tab10', dashes= False, markers= 'o')
sns.despine()

plt.legend().remove()
plt.title('Trends of Top Skills For Data Analyst Role In The UK', fontsize= 12, weight= 'bold')
plt.xlabel('2024')
plt.ylabel('Skill Percent Chances')

#to label the yaxis as percentage
from matplotlib.ticker import PercentFormatter
ax= plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(xmax= 100, decimals=0))

# to add labels to each line
for i in range(5):
    plt.text(10, df_plot.iloc[10, i], DA_percent.columns[i])

plt.show()

```
### Results

[Trend of Top skills For Data Analyst Job Role in The Uk]()

*line chart showing a graphic visualization of the trends of top skills for Data Analysts in 2024.*

### Insights
 - ``SQL`` and `Excel` remain consistently in demand, fluctuating between 40–45%, with ``SQL`` generally surpassing `Excel`. `Tableau` maintains a consistent but lower demand compared to other skills, suggesting limited but specialized use..

- `Power BI` shows a notable upward trend mid-year, peaking around July, indicating growing interest in business intelligence tools. `Python` sees a steady rise in demand toward the end of the year, likely due to increasing data automation and analysis needs.



## 3. How Well Do Jobs And Skills Pay For Data Analysts?

### Salary Distribution For Data Jobs In The Uk

#### Visualize Data

```python
sns.boxplot(top_6, x= 'salary_year_avg', y= 'job_title_short', order= job_order)
plt.title('Salary Distribution In The United Kingdom')
plt.xlabel('Yearly Salary ($USD)')
plt.ylabel('')
ax =plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos:  f'${int(x/1000)}K'))
plt.xlim(0,350000)
plt.show()

```
#### Results

[Salary Distribution For Top 5 Data Roles In The UK]()

*Box plot Showing The Distribution Of Salaries For Top 5 Data Roles In The UK*

### Insights
- Senior Data Scientists lead with the highest median salaries and widest range, reaching up to ~$300K. Senior positions (Data Scientist, Data Engineer, Data Analyst) generally have a broader salary range and higher outliers compared to non-senior roles.
- Entry-Level Roles: Data Analysts and Data Engineers have more compact salary ranges, typically peaking below ~$150K. Multiple high outliers are seen in senior engineering roles, indicating some very high-paying jobs in specific cases.


### Highest Paid and Most Demanded Skills For Data Analysts In Nigeria

#### Visualize Data

```python
fig, ax= plt.subplots(2,1)
sns.set_theme(style= 'ticks')

# Highest paid skills
sns.barplot(df_uk_top_skills, x= 'median', y= df_uk_top_skills.index, hue= 'median', palette= 'light:b', ax=ax[1])
ax[1].legend().remove()
ax[1].set_title('Top 10 Most In Demand Skills For Data Analyst')
ax[1].set_xlabel('Median Salary (USD)')
ax[1].set_ylabel('')
ax[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x,pos: f'${int(x/1000)}k'))

# Most in-demand skills
sns.barplot(df_uk_top_pay, x= 'median', y= df_uk_top_pay.index, ax=ax[0], hue= 'median', palette= 'dark:r_r')
ax[0].legend().remove()
ax[1].set_xlim(ax[0].get_xlim())
ax[0].set_title('Top 10 Highest Paid Skills For Data Analysts')
ax[0].set_xlabel('')
ax[0].set_ylabel('')
ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x,pos: f'${int(x/1000)}K'))

plt.tight_layout()
plt.show
```
#### Results

[Top Paying and In-demand skills For Data Analyst]()

*Bar Charts visualizing Top 10 Paid skills and Most In-Demand Skills For Data Analyst.*

### Insights
- Top Salaries: Advanced technical skills like `pandas`, `TensorFlow`, and `PyTorch` command the highest median salaries (~$150K+).
- Demand Focus: `Tableau`, ``SQL``, and `Azure` are the most in-demand skills, reflecting the need for analytics and cloud expertise.
- Gap: High-demand skills like `Tableau` and ``SQL`` offer lower salaries compared to specialized programming and database skills.

## 4. What are the most Optimal Skills For Data Analysts In The UK?

### Optimal skills for Data Analysts in The UK

#### Visualize Data

```python
sns.scatterplot(
    x= 'skills_percent',
    y= 'median_salary',
    hue= 'technology',
    data= df_plot
)

sns.despine()
sns.set_theme(style='ticks')
texts = []
plt.xlabel('Percentage of Data Analyst Jobs')
plt.ylabel('Median Salary ($USD)')
plt.title ('Most Optimal Skills For Data Analyst in The UK')
# for labelling...
for i,txt in enumerate(df_skill_high_demand.index):
    texts.append(plt.text(df_skill_high_demand['skills_percent'].iloc[i], df_skill_high_demand['median_salary'].iloc[i], txt ))

adjust_text(texts, arrowprops=dict(arrowstyle='->', color = 'grey', lw= 1))

ax= plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos : f'${int(y/1000)}K'))
from matplotlib.ticker import PercentFormatter
ax.xaxis.set_major_formatter(PercentFormatter(xmax= 100, decimals=0))

plt.tight_layout()
plt.show()
```

#### Results

[Optimal Skills For Data Analysts in The Uk](3_Project\image\Optimal skills.png)

*Scatterplot showing optimal skills for Data Analysts in the Uk*

### Insights
- `SQL` and `Excel` dominate, appearing in over 40% of data analyst job postings. These skills offer strong alignment with employer demands and median salaries near ~$100K, making them essential for aspiring analysts. 
- `Python` follows closely, featured in ~30% of roles with a median salary around ~$100K, emphasizing its importance for data manipulation and analysis.
- `SQL Server` and `Flow` are associated with the highest median salaries (~$120K–$130K) but appear in fewer than 10% of job postings. These skills may cater to specialized roles or industries.
`Tableau` offers a balance between demand (20%) and salary ($100K), making it a valuable visualization tool.
- By category, Databases are  High-paying and in-demand such as `SQL`, `SQL Server`, Programming such as `Python` remains crucial for technical analysis. Analyst Tools like `Tableau` and `Power BI` strike a balance between utility and earnings.

# What i learnt

- During the course of this project, i have gained experience in cleaning, processing, and analyzing datasets using `Python` libraries like `Pandas` and `matplotlib`, which i learned to create meaningful visualizations some of which include boxplots, bar charts, scatter plots along with `Seaborn` to interpret data trends.
- Also i Understood salary distributions, in-demand skills, and trends for data roles across different regions. And most importantly,  enhanced my ability to handle end-to-end data projects, from sourcing datasets to deriving actionable insights.

# Insights
- This project Identified the most in-demand skills (`SQL`, `Python`, `Power BI`) and their significance in different roles, highlighting the alignment between skillsets and salary expectations.
- It also revealed clear salary distributions and disparities across various the top 3 data roles like Data Analyst, Data Scientist, and Data Engineer, emphasizing the earning potential in senior positions and technical roles.

# Conclusion

This project highlights the salary trends, skill demands, and optimal career paths for data-related roles in the UK. By analyzing job postings and salary distributions, it provides actionable insights for aspiring professionals to align their skills with industry demands. The findings emphasize the importance of tools like `SQL`, `Python`, and `Excel`, along with data visualization and cloud platforms, for career growth and higher earning potential. 

Thank you!