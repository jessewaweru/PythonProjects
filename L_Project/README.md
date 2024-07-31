# Introduction
The Datase I used is for the Job market! I specifically focused on Data Analyst roles, exploring problem statements such as Top-paying jobs, Top in-demand skills, and best optimal skills for Data analysts i.e. where high demand meets high salary. 
Furthermore, I decided to focus mostly with the roles being offered in the United states. The data was much more detailed and it was a great comparison to use to better the Data Job market.

Here are the Python code snippets I used to generate my various insights:
[Lead Project](L_Project)


# Background
I was interested in knowing how the job market for Data Analyst looks like in a more consise way. I decided to use this dataset that showcases insights such as job titles, salaries, locations, companies offering them,skills associated with each job posting and more. I got the dataset from a YouTube channel of a data analyst called Lukebarousse.

### Problem statements I answered using Python
1. What are the most demanded skills for the top 3 most popular data roles in the US?
2. What's the trend of in-demand skills for Data Analysts?

# Tools I used
The tools I used to generate my insights for the project include the following:
- **Python**
- **Visual Studio Code**: My ideal code editor for SQL queries
- **Git and GitHub:** Needed a version control to showcase the steps and changes  made as I progressed with my analysis. It's also ideal for sharing and collaboration purposes.

# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles in the US?

I decided to filter out the dataset to find out the most in demand positions for Data roles by count and I got the top three. 

Next I proceeded to further filter out the dataset using the skills that are highly demanded for the top 3 positions.
As someone aspiring for a data role, I wanted to educate myself further to know which skills are giong to be demanded most often by future employers.


View my notebook showcasing the steps I took:

[2_Skill_Demand.ipynb](L_Project\2_Skill_Demand.ipynb)

## You can visualise the data using:

```python
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style='whitegrid', palette= 'pastel')

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    #df_plot.plot(kind= 'barh', x= 'job_skills', y= 'skill_percent', ax=ax[i], title= job_title)
    sns.barplot(data= df_plot,x='skill_percent',y='job_skills', ax=ax[i], hue= 'skill_count', palette='dark:b_r')
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].legend().set_visible(False)
    ax[i].set_xlim(0,78)
    
    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v +1, n, f'{v:.1f}%', va='center')
   
    if job_title != 'Data Engineer':
        ax[i].set_xticks([])
    
            
    
fig.suptitle('Likelihood of Skills requested in the US Data Job Postings', fontsize= 15)

fig.tight_layout(h_pad=0.5)

plt.show()
```

### Result

![Visualization of Top in Demand skills for Top 3 Data Roles in the US](L_Project/images/SkillDemand.png)
*Bar graph visualizing the top in-demand skills for the top 3 Data Roles in 2023.*

### Insights

- Both Data Analyst and Data Scientists have Python and SQL as the most demanded skills for the role but they very between them with Data scientist requiring Python more over SQL i.e. over 72%.

- Data Engineer skills are more specialiszed compared to the two mentioned above with skills such as AWS, Azure and Spark preferred for the role. However, it still has Python and SQL as the most in demand skills.


## 2. What's the trend of in-demand skills for Data Analysts?

Next, I filtered the data to showcase the how popular the top 5 skills for Data Analysts are by comparing the job postings for each skill on a month by month basis for the year 2023 so that I could establish potential trends in the data.

### Visualize the Data

```python

sns.lineplot(data= df_plot, dashes= False, palette= 'tab10')
sns.set_theme(style= 'ticks')
sns.despine()


plt.title('Top Trending Skills for Data Analysts in the US')
plt.xlabel('Month 2023')
plt.ylabel('Likelihood of Job Posting(%)')
plt.legend(loc='upper right', bbox_to_anchor=(1.2, 1))
plt.show()

```

## Results

![Top Trending Skills for Data Analysts in the US](L_Project/images/SkillsTrends.png)
*Line graph visualizing the top trending skills for Data Analysts in 2023.*

## Insights

- SQL is still consistently the moment demanded skill for Data analyst followed by Excel which still remains a major requirement for employers. Tableau and Python are closely matched to each other with minor fluctuations relative to job postings.


## 3. How well do jobs and skills pay for Data roles?

View my notebook showcasing the steps I took:

[4_SalaryAnalysis.ipynb](L_Project/4_SalaryAnalysis.ipynb)

### Here is an overview of the code used to generate a boxplot showcasing the salary distribution of the top six Data jobs in the US.

``` python
sns.boxplot(data=df_us_6, x='salary_year_avg', y='job_title_short', order= role_order)
sns.set_theme(style='ticks')
sns.despine()

plt.title('Salary Distributions of Data Jobs in the US')
plt.xlabel('Yearly Average Salary($)')
plt.ylabel('')
plt.xlim(0, 600000) 
plt.show()

```

## Result

![Visualization of the Salary Distribution for Top 6 Data Roles in the US](L_Project/images/Salary_Analysis.png)
*Bar graph visualizing the Salary Distribution for Top 6 Data Roles in the US.*

## Insights

- Data analyst roles compared to the other roles have fewer outliers on the higher end indicating a level of consistency in pay while the other roles may vary slightly due to factors such as having more marketable and high-paying skills that can lead to an increased salary bump. The role that showcases this more than any is the Data Scientist role.

- The median salary also increases with seniority and is progressing step by step from Data Analyst to Data Engineer to Data Scientist.