# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills i should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here:
[2_Skill_Demand.ipynb](3_Project\2_Skill_Count.ipynb)

```python
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style="whitegrid")

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc["job_title_short"] == job_title].head(5)
    sns.barplot(
        data=df_plot,
        x="skill_perc",
        y="job_skills",
        ax=ax[i],
        hue="skill_count",
        palette="dark:b_r",
        legend=False,
    )
    ax[i].set_title(job_title)
    ax[i].set_ylabel("")
    ax[i].set_xlabel("")
    ax[i].set_xlim(0, 78)
    
    for n, v in enumerate(df_plot["skill_perc"]):
        ax[i].text(v + 1, n, f"{v:.0f}%", va="center")
        
    if i != len(job_titles) - 1:    
        ax[i].set_xticks([])

fig.suptitle(
    "Likehood of Skill Being Required for Top 3 Job Titles in the US", fontsize=13
)
fig.tight_layout(h_pad=0.5)
plt.show()
```

### Results

![Visualization of Top Skills](/3_Project/images/skill_demand_all_data_roles.png)

### Insights

- SQL is the most in-demand skill across all three job titles. It has the highest likelihood of being required for all three positions (Data Analyst: 41%, Data Engineer: 68%, Data Scientist: 51%). This highlights the fundamental importance of SQL for data professions in general.

- Python is another highly sought-after skill. It's essential for Data Scientists (72%) and Data Engineers (65%), and also relevant for Data Analysts (27%). Python's versatility makes it a valuable tool for data manipulation, analysis, and machine learning.

- Skills required for Data Analysts and Data Scientists show some overlap. Both roles might require expertise in SQL, Python, and statistics (represented by SAS in the graph). However, Data Scientists tend to have a higher likelihood of needing these skills.

- Data Engineers and Data Scientists show the most overlap in skill requirements. Both roles heavily rely on Python and SQL, along with cloud platforms like AWS and Azure. However, Data Engineers have a higher likelihood of needing expertise in technologies like Spark for large-scale data processing.