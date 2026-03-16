<h1 align="center">Overview</h1>

## 📑 Table of Contents

* [📊 Overview](#overview)
* [🛠️ Tools Leveraged](#️-tools-leveraged)
* [🧹 Data Preparation & Cleanup](#-data-preparation--cleanup)

### 📊 Analysis

* [1️⃣ Most In-Demand Skills for Top Data Roles](#1️⃣-what-are-the-most-in-demand-skills-for-the-top-3-data-roles)
* [2️⃣ Skill Trends for Data Engineers in India](#2️⃣-how-are-in-demand-skills-trending-for-data-engineers-in-india)
* [3️⃣ Salary Distribution by Job Title (US)](#3️⃣-how-does-salary-vary-by-job-title-us)
* [4️⃣ Skills vs Salary for Data Engineers](#4️⃣-how-do-skills-impact-data-engineers-salaries)
* [5️⃣ Most Optimal Skills for Data Engineers](#5️⃣-what-are-the-most-optimal-skills-to-learn-for-data-engineers)

### 📊 Visualization Extensions

* [🎨 Technology Category Visualization](#-visualizing-different-technology-categories)

### 📘 Project Takeaways

* [🧠 What I Learned](#-what-i-learned)
* [💡 Key Insights](#-key-insights)
* [⚠️ Challenges I Faced](#️-challenges-i-faced)
* [🚀 Conclusion](#-conclusion)

<br>

# 📊 Data Analyst Job Market Analysis

Welcome to my analysis of the **data job market**, with a focus on **data analyst roles**. This project was created to better understand the evolving job landscape and identify the skills that lead to the best opportunities in data analytics.

The goal of this project is to analyze **top-paying roles and the most in-demand skills** to help aspiring and current data analysts make informed career decisions.

## 📂 Dataset

The dataset used in this project comes from [Luke Barousse's Python Course](https://lukebarousse.com/python), which provides detailed information about:

- Job titles
- Salaries
- Job locations
- Required skills

This dataset serves as the foundation for the analysis.

## 🔍 Project Focus

Using **Python for data analysis**, this project explores several key questions about the data job market:

- What are the **most in-demand skills** for data analysts?
- Which skills are associated with the **highest salaries**?
- What are the **salary trends** in data analytics roles?
- Which skills offer the **best combination of demand and salary**?

Through a series of Python scripts and data analysis techniques, this project uncovers insights into the **intersection of skills demand and compensation** within the data analytics field.


# 🛠️ Tools Leveraged

For this deep dive into the **data analyst job market**, I used several powerful tools and technologies to perform analysis, visualization, and project management.

### 🐍 Python

The backbone of this project. Python was used to clean, analyze, and extract insights from the dataset.

**Key Python Libraries Used:**

* **Pandas** – Used for data cleaning, manipulation, and analysis.
* **Matplotlib** – Used to create fundamental data visualizations.
* **Seaborn** – Used for more advanced and visually appealing statistical plots.

### 📓 Jupyter Notebook

Used to run Python scripts in an interactive environment, making it easy to combine **code, analysis, and explanations** in one place.

### 💻 Visual Studio Code

Served as the primary code editor for writing and managing Python scripts throughout the project.

### 🔧 Git & GitHub

Used for **version control and project sharing**, allowing the project to be tracked, organized, and easily shared with others.

## 🧹 Data Preparation & Cleanup

This section outlines the steps taken to prepare the dataset for analysis, ensuring the data is accurate, consistent, and ready for exploration.

### 📥 Importing & Cleaning the Data

The process begins by importing the necessary Python libraries and loading the dataset.
Initial data cleaning steps are then performed to improve data quality and ensure the dataset is suitable for analysis.

Key preparation steps include:

* Importing required Python libraries
* Loading the dataset into the analysis environment
* Inspecting the dataset structure and data types
* Handling missing or inconsistent values
* Preparing the data for further analysis and visualization


```python
# Importing Libraries
import pandas as pd
from datasets import load_dataset
import matplotlib.pyplot as plt
import ast

# Loading the dataset
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()

# Sorting the Dataframe
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
# converting job_skills from string to list
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else [])
```

### 🌎 Filtering Jobs by Country

To ensure the analysis remains relevant to the target job market, the dataset was filtered by **job location**.

Although the dataset is primarily **U.S.-focused**, a small number of listings also include other countries such as **India**. For consistency and more meaningful insights, the analysis narrows


```python
df_IN = df[df['job_country'] == 'India']
df_US = df[df['job_country'] == 'United States']
```

# 📊 The Analysis

Each **Jupyter Notebook** in this project investigates a specific aspect of the data job market. The goal is to answer key questions about **skills demand, salary trends, and role popularity** within the data industry.

Below is the approach used to explore each research question.

---

## 1️⃣ What Are the Most In-Demand Skills for the Top 3 Data Roles?

To identify the most in-demand skills, I first determined the **three most common data-related job roles** in the dataset. After identifying these roles, I analyzed the skills associated with each position and extracted the **top five most frequently requested skills**.

This analysis helps highlight:

* The **most popular job titles** in the data field
* The **core skills employers expect** for each role
* Which skills aspiring data professionals should focus on depending on the **career path they want to pursue**

By comparing skill demand across these roles, we gain a clearer understanding of the **technical competencies that dominate the job market**.

📓 **View the full notebook here : ➡️**
[2_Skill_Demand_Analysis.ipynb](2_Skill_Demand_Analysis.ipynb).

---

### 📈 Data Visualization

To better understand the demand for skills across different roles, visualizations were created to compare the **frequency of required skills** for each of the top data job titles. These visuals make it easier to quickly identify which skills appear most often across the market.

### Visualize Data

```python
# final plotting
fig, ax = plt.subplots(len(job_titles), 1, figsize=(10,7))


for i, job_title in enumerate(job_titles):
    df_plot = df_perc[df_perc['job_title_short'] == job_title].head(8)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='plasma_r')
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].get_legend().remove()
    ax[i].set_xlim(0, 75)
    # remove the x-axis tick labels for better readability
    if i != len(job_titles) - 1:
        ax[i].set_xticks([])

    # label the percentage on the bars
    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1, n, f'{v:.0f}%', va='center')

fig.suptitle('Likelihood of Skills Requested in India', fontsize=20, fontweight='bold')
fig.tight_layout(h_pad=.8)
plt.show()
```

### Results
![Likelihood of Skills Requested in Job Postings (India)](project_images\Likelihood_of_Skills_Requested_in_India.png)

*Bar graph visualizing the salary for the top 3 data roles in India and their top 5 skills associated with each.*

### 🔍 Insights
- **Python and SQL dominate the data job market in India.**  
  Python is the most requested skill for **Data Scientists (70%)**, while SQL leads for both **Data Engineers (68%)** and **Data Analysts (52%)**, highlighting that programming and database querying are foundational skills across all data roles.

- **Data Engineering roles require stronger big data and cloud skills.**  
  Technologies like **Spark (38%)**, **AWS (37%)**, and **Azure (36%)** appear prominently for Data Engineers, showing that infrastructure, distributed computing, and cloud platforms are critical in this role.

- **Business intelligence tools are more important for Data Analysts.**  
  Skills such as **Excel (35%)**, **Tableau (27%)**, and **Power BI (21%)** are common for Data Analysts, indicating that visualization, reporting, and business-focused analysis tools are key requirements for this role.



 ## 2️⃣ How Are In-Demand Skills Trending for Data Engineers in India?

To analyze **skill trends for Data Engineers in India in 2023**, I filtered the dataset to include only **Data Engineer job postings located in India**. The skills were then grouped by the **month the job was posted**, allowing me to track how demand for specific skills changed throughout the year.

From this analysis, I identified the **top five most frequently requested skills each month**, helping reveal how skill demand evolved across 2023.

This approach helps answer questions such as:

* Which **data engineering skills remained consistently in demand**
* Which skills **increased or decreased in popularity**
* How the **data engineering skill landscape changed over time**

📓 **View the full notebook here:**
[3_Skills_Trend_Analysis.ipynb](3_Skills_Trend_Analysis.ipynb)

---

### 📈 Data Visualization

```python
from matplotlib.ticker import PercentFormatter

# theme first
sns.set_theme(style='white')

plt.figure(figsize=(10,7))

df_plot = DA_IN_percent.iloc[:, :5]

sns.lineplot(
    data=df_plot,
    dashes=False,
    palette="tab10",
    linewidth=2.5,
    markers=True
)

plt.title('Trending Top Skills for Data Engineers in India', fontsize=18, weight='bold')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('')

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))
sns.despine()

# annotate the plot with the top 5 skills
for i in range(5):
    plt.text(11.2, df_plot.iloc[-1, i], df_plot.columns[i], fontsize=10)

plt.legend().remove()

plt.tight_layout()
plt.show()
```

The visualization above tracks how the **top skills for Data Engineers in India changed month-to-month during 2023**, making it easier to observe trends and shifts in employer demand.

---

### 📊 Results

![Trending Top Skills for Data Engineers in India](project_images\Trending_Top_Skills_for_Data_Analysts_in_india.png)

*Line chart visualizing the trending top skills for Data Engineers in India throughout 2023.*
### 🔍 Insights
- **SQL remains the most consistently demanded skill for Data Engineers.**  
  Throughout the year, SQL maintains the highest likelihood in job postings, gradually increasing and reaching its peak toward the end of the year, reinforcing its role as a core skill for data engineering.

- **Python shows a steady upward trend in demand.**  
  Although slightly fluctuating in the middle of the year, Python demand increases significantly from September onward, indicating growing importance for automation, data processing, and pipeline development.

- **Cloud and big data tools show moderate but stable demand.**  
  Skills like **AWS, Azure, and Spark** stay within a similar range across the year, suggesting they are important complementary technologies rather than rapidly changing trend skills.

## 3️⃣ How Does Salary Vary by Job Title (U.S.)?

To understand how salaries differ across roles, I analyzed **data-related job postings located in the United States** and compared their **median yearly salaries**.

The analysis focuses on common data roles such as:

* Data Scientist
* Data Engineer
* Data Analyst

By examining the **salary distributions** for these roles, we can better understand which positions tend to offer higher compensation and how salaries vary across different job titles within the data field.

📓 **View the full notebook here:**
[4_Salary_Model_Analysis.ipynb](4_Salary_Model_Analysis.ipynb)

---

### 📈 Data Visualization

```python
# final plotting
import matplotlib.ticker as mticker
from numpy import place
fig, ax = plt.subplots(figsize=(12,7))
sns.set_theme(style='whitegrid')
sns.boxplot(data=job_top_5,x='salary_year_avg',y='job_title_short',order=job_ordered,color='skyblue')

# lets format the plot
plt.title('What is the salary distribution for Data Jobs? (US)',fontsize=15,fontweight='bold')
plt.xlabel('Median Salary ($USD)')
plt.ylabel('')
plt.xlim(0,340000)
plt.gca().xaxis.set_major_formatter(mticker.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))


# remove extra borders
for spine in ['top','right']:
    plt.gca().spines[spine].set_visible(False)


plt.tight_layout()
plt.show()
```

The box plot below visualizes the **salary distribution across the top data job roles**, making it easier to compare median salaries, salary ranges, and potential outliers between roles.

---

### 📊 Results

![Salary Distributions of Data Jobs in the US](project_images\Salary_Distributions_of_Data_Jobs_in_the_US.png)

*Box plot showing the salary distribution for the top six data job titles in the United States.*

### 🔍 Insights
- **Senior roles command the highest salaries.**  
  Senior Data Scientists and Senior Data Engineers show the highest median salary ranges, typically around **$140K–$170K**, reflecting the premium placed on experience and advanced expertise.

- **Data Analysts earn the lowest median salaries among data roles.**  
  Compared to other positions, Data Analysts have a significantly lower median salary, generally around **$80K–$100K**, highlighting the entry-level nature of many analyst roles.

- **Wide salary spread indicates strong growth potential.**  
  All roles show numerous high-end outliers reaching **$250K–$330K**, suggesting that specialized skills, seniority, and company size can significantly increase compensation in data careers.

## 4️⃣ How Do Skills Impact Data Engineers' Salaries?

To better understand how specific skills influence salaries, I narrowed the analysis to focus exclusively on **Data Engineer roles in the United States**.

The analysis compares two key perspectives:

* **Highest-paid skills** — Skills associated with the highest median salaries
* **Most in-demand skills** — Skills that appear most frequently in job postings

By comparing these two categories, we can identify which skills are both **valuable in the job market** and **highly compensated**, helping data professionals prioritize the most impactful skills to learn.

---

### 📈 Data Visualization

```python
# lets finally plot this
import matplotlib.ticker as mticker
fig, ax = plt.subplots(2,1,figsize=(10,7))

# 1 most demanding skills
sns.barplot(data=df_DE_US_demand.sort_values(by='median',ascending=False),x='median',y=df_DE_US_demand.index,hue='median',ax=ax[0],palette='cividis_r')

# formatting
ax[0].set_title('Which Skills Are Most Demanded for Data Engineers? (US)',fontsize=15)
ax[0].set_xlabel('')
ax[0].set_ylabel('')
ax[0].legend().remove()
ax[0].set_xlim(0,210000)
ax[0].xaxis.set_major_formatter(mticker.FuncFormatter(lambda x, pos: f'${x/1000:.0f}K'))

# 2 Highest paying skills
sns.barplot(data=df_DE_US_pay,x='median',y=df_DE_US_pay.index,hue='median',ax=ax[1],palette='cividis_r')

# formatting
ax[1].set_title('Which Skills Pay Highest for Data Engineers? (US)',fontsize=15)
ax[1].set_xlabel('')
ax[1].set_ylabel('')
ax[1].legend().remove()
ax[1].set_xlim(0,210000)
ax[1].xaxis.set_major_formatter(mticker.FuncFormatter(lambda x, pos: f'${x/1000:.0f}K'))

plt.tight_layout()
plt.plot()


plt.show()
```

These visualizations highlight the difference between **skills that command the highest salaries** and those that are **most frequently requested by employers**.

---

### 📊 Results

![The Most In-Demand & Highest Paid Skills for Data Engineers in the US](project_images\Highest_Paid_and_Most_In_Demand_Skills_for_Data_Engineers_in_the_US.png)

*Two bar charts illustrating the most in-demand skills and the highest-paid skills for Data Engineers in the U.S.*
### 🔍 Insights
- **Core data engineering tools dominate job demand.**  
  Skills such as **SQL, Python, AWS, Spark, and Azure** appear as the most requested in job postings, showing that database management, programming, and cloud platforms are fundamental requirements for Data Engineers.

- **Specialized technologies tend to command higher salaries.**  
  Tools like **MongoDB, Solidity, Node.js, and Rust** appear among the highest-paying skills, suggesting that niche or advanced technical expertise can significantly increase earning potential.

- **High demand does not always equal the highest pay.**  
  While widely used tools like **SQL and Python** are highly demanded, the highest salaries are often associated with more specialized or less common technologies, indicating a premium for scarce skills.

## 5️⃣ What Are the Most Optimal Skills to Learn for Data Engineers?

To determine the **most optimal skills to learn**, I focused on identifying skills that are both **high in demand** and **associated with higher salaries** for **Data Engineers**.

To achieve this, I calculated:

* The **percentage of job postings requiring each skill** (skill demand)
* The **median salary associated with each skill**

Combining these two metrics makes it easier to identify skills that offer the **best balance between market demand and compensation**, helping data professionals prioritize which skills may provide the greatest career value.

📓 **View the full notebook here:**
[6_Optimal_Skills_Analysis.ipynb](6_Optimal_Skills_Analysis.ipynb)

---

### 📈 Data Visualization

```python
from adjustText import adjust_text
from matplotlib.patches import ArrowStyle

# now finally we can plot the scatter plot
plt.scatter(skill_high_demand['skill_percent'],skill_high_demand['median_salary'])

# now getting current axes and formatting it accordingly
ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y , pos: f'${int(y/1000)}K'))

# adding the lables
texts = []
for i, txt in enumerate(skill_high_demand.index):
    texts.append(plt.text(skill_high_demand['skill_percent'].iloc[i],skill_high_demand['median_salary'].iloc[i],''+ txt))

# adjusting the arrows
adjust_text(texts, arrowprops=dict(arrowstyle='->', color='blue'))
```

The scatter plot compares **skill demand** against **median salary**, making it easy to identify skills that fall into the **high-demand and high-paying quadrant**.

---

### 📊 Results

![Most Optimal Skills for Data Engineers in the US](project_images\Most_Optimal_Skills_for_Data_Engineers_in_the_US.png)

*A scatter plot visualizing the most optimal skills (high demand and high paying) for Data Engineers in the United States.*

### 🔍 Insights
- **SQL and Python dominate job demand but offer moderate salaries.**  
  SQL (~72%) and Python (~69%) appear in the highest percentage of job postings, making them essential baseline skills for Data Engineers, though their median salaries are slightly lower compared to some specialized tools.

- **Streaming and big data technologies offer strong salary potential.**  
  Skills like **Kafka, Spark, and Scala** show relatively high median salaries (around $137K–$145K) despite appearing in fewer job postings, indicating strong value for big data and real-time processing expertise.

- **Balanced skills provide the best opportunity.**  
  Technologies such as **AWS, Snowflake, and Spark** offer a strong balance between demand and salary, making them highly strategic skills for data engineers looking to maximize both employability and compensation.

    ### 🎨 Visualizing Different Technology Categories

To gain deeper insights into the most optimal skills, the visualization was enhanced by **grouping skills based on their technology category** (for example, *Programming: Python*).

By adding **color labels for each technology group**, the chart makes it easier to see which categories of tools—such as programming languages, databases, or cloud technologies—tend to offer the **best combination of high demand and high salary**.

---

#### 📈 Data Visualization

```python plt.figure(figsize=(12, 8)) 
sns.scatterplot(
    data=df_DA_skills_demand,
    x='skill_percent',
    y='median_salary',
    hue='technology',


)
sns.despine()
sns.set_theme(style='darkgrid',palette='deep')

# Prepare texts for adjustText
texts = []
for i, txt in enumerate(skill_high_demand.index):
    texts.append(plt.text(skill_high_demand['skill_percent'].iloc[i], skill_high_demand['median_salary'].iloc[i], txt))

# Adjust text to avoid overlap
adjust_text(texts, arrowprops=dict(arrowstyle='->', color='blue'))

# Set axis labels, title, and legend
plt.xlabel('Percent of Data Engineer Jobs',fontweight='bold')
plt.ylabel('Median Yearly Salary($USD)',fontweight='bold')
plt.title('What are Most Valuable Skills for Data Engineers? (US)',fontweight='bold',fontsize=20)
plt.legend(title='Tech Category')

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K'))
ax.xaxis.set_major_formatter(PercentFormatter(decimals=0))

# Adjust layout and display plot 
plt.tight_layout()
plt.show()
```

This visualization highlights how different **technology categories** compare in terms of **salary potential and market demand**.

---

#### 📊 Results

![Most Optimal Skills for Data Engineers in the US with Coloring by Tech Categories](project_images\Most_Optimal_Skills_for_Data_Engineers_in_the_US_with_Coloring_by_Technology.png)

*A scatter plot showing the most optimal skills (high demand and high paying) for Data Engineers in the U.S., with colors representing different technology categories.*

### 🔍 Insights
- **Programming and cloud skills dominate job demand.**  
  Skills like **SQL (72%)**, **Python (69%)**, and **AWS (45%)** appear in the highest percentage of Data Engineer job postings, highlighting their importance as foundational technologies in modern data infrastructure.

- **Streaming and big data tools offer higher salary potential.**  
  Technologies such as **Kafka, Scala, Airflow, and Spark** are associated with some of the highest median salaries (~$137K–$145K), indicating that expertise in distributed systems and data pipelines is highly valued.

- **Specialized technologies balance demand and compensation.**  
  Tools like **Snowflake, Redshift, and Databricks** sit in the middle range for both demand and salary, making them valuable complementary skills for Data Engineers looking to strengthen their cloud data stack.


<br>
<br>

## 🧠 What I Learned

Throughout this project, I gained a deeper understanding of the **data engineering job market** while strengthening my technical skills in **Python-based data analysis and visualization**. Below are some of the key takeaways from this project:

* **Advanced Python Usage**
  I strengthened my ability to use libraries such as **Pandas** for data manipulation and **Seaborn** and **Matplotlib** for data visualization. These tools enabled me to efficiently explore datasets and extract meaningful insights.

* **Importance of Data Cleaning**
  I learned that **thorough data cleaning and preparation** are essential before performing any analysis. Handling missing values, inconsistencies, and incorrect data types ensures that the insights derived from the dataset are reliable.

* **Strategic Skill Analysis**
  This project highlighted the importance of **aligning technical skills with market demand**. Understanding the relationship between **skill demand, salary levels, and job availability** allows professionals to make more strategic career decisions in the tech industry.

---

## 💡 Key Insights

This analysis revealed several important insights about the **data engineering job market**:

* **Skill Demand and Salary Relationship**
  There is a strong connection between **specialized technical skills and higher salaries**. Skills such as **Python, cloud technologies, and advanced data tools** tend to command higher compensation.

* **Changing Market Trends**
  Skill demand evolves over time, reflecting the **rapidly changing nature of the data industry**. Staying updated with emerging technologies is critical for long-term career growth.

* **Economic Value of Skills**
  Identifying skills that are both **highly demanded and well compensated** helps data professionals prioritize what to learn next to maximize career opportunities.

---

## ⚠️ Challenges I Faced

Like many real-world data projects, this analysis came with several challenges that required careful problem-solving:

* **Data Inconsistencies**
  Some job postings contained missing or inconsistent values, requiring careful **data cleaning and preprocessing** to ensure reliable results.

* **Complex Data Visualization**
  Creating clear and meaningful visualizations from complex datasets required experimenting with different chart types and visualization techniques.

* **Balancing Breadth and Depth**
  Deciding how deeply to analyze certain aspects of the dataset while still maintaining a broad overview of the job market required thoughtful planning.

---

# 🚀 Conclusion

This project provided valuable insights into the **Data  Jobs market**, highlighting the key skills and trends that shape this rapidly evolving field. The analysis not only strengthened my technical abilities but also improved my understanding of how **market demand and compensation are linked to specific technical skills**.

As the data industry continues to evolve, **continuous learning and ongoing market analysis** will remain essential for professionals looking to stay competitive. This project serves as a strong foundation for further exploration and deeper analysis of trends within the data ecosystem.
