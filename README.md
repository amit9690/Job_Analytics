![image](https://github.com/amitporwal01/Job_Analytics_Instahyre_job_finder/assets/129444885/19b73efe-ff33-4af9-b3a5-007ab3c96a04)# Job_Analyst_Project
![Untitled design](https://github.com/amit9690/Job_Analytics_Instahyre_job_finder/assets/129444885/2764ed8d-4d9c-470e-9a2e-3d815cfc6dc5)

Unlocking the Power of Data: As a Job Analyst, I dive deep into the world of employment trends and insights.

My mission? To decode the job market's secrets, helping individuals find their dream careers and businesses make informed decisions. Join me on this data-driven journey, where numbers come to life, and opportunities are waiting to be discovered. Explore my projects, where I transform raw data into actionable insights, one job at a time. Let's shape the future of work together!



# Project Overview 👩🏻‍💻📋🎯 :

📌 Project Name: Job Analyst

👥 Team Members: Amit Porwal, Madhu Gupta, Shubhum Pathak

🎓 Mentored by: Manish Hemnani

🔧 skills required: Power BI, Python, Mysql, Visualization, BeautifulSoup, Selenium, EDA, Dashboard

📅 Project start Date: 30/08/2023

📅 Project end Date: 04/09/2023


# Project Description 📁:

"Job Analyst" is a comprehensive data analysis project that aims to provide valuable insights into job vacancies sourced from the Instahyre website, a prominent job portal. This project was conceived and executed by a team of dedicated individuals, including Amit Porwal, Madhu Gupta, and Shubhum Pathak, under the expert guidance of Manish Hemnani.

## Project Phases:

![Untitled design (2)](https://github.com/amit9690/Job_Analytics_Instahyre_job_finder/assets/129444885/0d548263-62fe-4e86-9099-64fd58b22b7f)



### 1. Data Scraping 🔍:

* Utilized Python libraries like BeautifulSoup and Selenium to programmatically access web pages and extract job data from the Instahyre website.
* Employed web scraping techniques to navigate through multiple web pages, interact with HTML elements, and capture relevant job information.
* Ensured data integrity by handling issues such as page loading delays, element identification, and handling dynamic web content using Selenium.

#### Step 1: Import Essential Libraries

In the initial phase of this project, I initiate by importing key Python libraries: BeautifulSoup, Selenium, Pandas, and Time.

* **BeautifulSoup:** This library enables me to parse HTML content from web pages effectively.

* **Selenium:** Selenium is a powerful tool for automating web browser interactions. It allows me to programmatically navigate the Instahyre website, interact with elements, and retrieve data.

* **Pandas:** Pandas is an essential data manipulation library. It provides data structures and functions to organize and manipulate the extracted data efficiently.

* **Time:** Time is used for adding time-related delays in the web scraping process, ensuring that web pages load properly before data extraction.

```
from bs4 import BeautifulSoup
from selenium import webdriver
import time
import pandas as pd

```
```
url = "https://www.instahyre.com/jobs-in-india"
#url = "https://www.instahyre.com/search-jobs?company_size=0&isLandingPage=true&job_type=0&location=Anywhere+in+India&search=true"
driver = webdriver.Chrome()
driver.get(url)
time.sleep(5)

```
#### Step 2: Data Extraction with Selenium

In the second step, I leverage the Selenium library to perform web scraping on the Instahyre website.

* I use Selenium to automate the process of accessing the web pages containing job data.

* Then, I locate and interact with the necessary HTML elements, such as job listings and job details, to extract the desired data.

* Selenium's capabilities in simulating user interactions, such as clicking buttons and filling forms, prove invaluable in navigating the site and retrieving data seamlessly.

```
data = []
a = 30
while (a>0):
    html = driver.page_source
    soup = BeautifulSoup(html, "html.parser")
    view_link_div = soup.find_all('div',class_='opportunity-action-links')

    for i in view_link_div:

        link = i.find('a',href=True)
        driver.get(link['href'])
        time.sleep(2)
        s_page = BeautifulSoup(driver.page_source,"html.parser")
        c_info = s_page.find('div',class_='company-info')
        
        company_name = s_page.find('h2',class_='company-name').text
        
        div_info = c_info.find_all('div')
        f_year = div_info[0].text
        n_employee = div_info[1].text
        
        location = s_page.find('div',class_ = 'job-locations').find_all('span')[0].text
        designation = s_page.find('div',class_='profile-info').find('h1').text
        hr_name = s_page.find('span',class_='rec-name').text
        
        try:
            skills =','.join([x.text for x in  s_page.find('ul',{'id':'job-skills-description'}).find_all('li')])
        except:
            print(str(a)+' / '+company_name)
            
        data.append([company_name,f_year,n_employee,location,designation,hr_name,skills])
        driver.execute_script('history.back()')
        time.sleep(1)
        
    
    driver.execute_script('$(".pagination li:last").click()')
    time.sleep(3)
    a-=1

```

#### Step 3: Data Wrangling and Export

The final step involves organizing and storing the extracted data in a structured manner.

* Using Pandas, I create a DataFrame, which is a tabular data structure, to hold the scraped data. This facilitates efficient data manipulation and analysis.

* I transfer the extracted job information into the DataFrame, ensuring that it's well-structured and ready for further processing.

* To make the data accessible and shareable, I export the DataFrame to a CSV (Comma-Separated Values) format. This format is commonly used for storing and exchanging structured data, making it suitable for analysis using various data analysis tools and languages.


```
df = pd.DataFrame(data , columns = ['name','estab_year','employees_count','location','designation','hr_name','skills'])
```
```
df.to_csv('C:\\Users\\User\\Desktop\\company.csv')
```

In summary, these three steps outline the process of extracting job data from the Instahyre website, transforming it into a structured format, and exporting it for analysis and exploration.


### <a name = 'project-overview'></a>2. Data Cleaning 🧹: 

* Performed data cleaning tasks to enhance data quality and consistency.
* Addressed missing values, duplicates, and outliers in the scraped data to prevent skewed analysis.
* Employed Pandas to handle data cleansing tasks such as removing redundant information, filling in missing data, and ensuring uniform data types.
* Conducted exploratory data analysis (EDA) to gain insights into data distribution and quality.


### 3. Data Preprocessing 🔧: 

* Leveraged Power Query functionality to extract data from other columns, creating new derived features.
* Data transformation, particularly the extraction of sector information from the designation column to enable deeper analysis based on industries.
* Combined and reshaped data from various sources to prepare it for modeling.

### 4. Data Modeling 📊 : 

This phase involved the creation of key tables to structure the data for effective analysis:

* Developing three central tables: jobs, company, and details, facilitating the organization of data for efficient querying and extraction of insights.
* Employing relational database concepts to establish connections between tables, enabling complex queries and comprehensive analysis.
* Leveraging SQL to create and manage these tables, ensuring data integrity and consistency.

**__I completed steps 2, 3, and 4 by using Power Query Feature in Power BI.__**

### 5. SQL Queries 📈: 

We utilized SQL queries for advanced data manipulation and retrieval:

* Constructing complex SQL queries to extract specific data subsets and perform aggregations.
* Implementing JOIN operations to merge data from multiple tables, facilitating comprehensive analysis.
* Utilizing SQL functions for data transformations and calculations, streamlining data processing tasks.


### 6. Power BI Dashboard 📄: 

Finally, we leveraged Power BI to create an interactive and visually informative dashboard:

* Developing Power BI worksheets to present data insights in a user-friendly format.
* Utilizing charts, graphs, and pivot tables to visualize trends and patterns.
* Incorporating slicers and filters for user interaction, enabling dynamic exploration of data.
* Ensuring real-time data updates through data connections, maintaining the dashboard's relevance.


#### Demo : 

![image](https://github.com/amitporwal01/Job_Analytics_Instahyre_job_finder/assets/129444885/14ed6684-cbbf-4ef9-a185-bc1a897613c1)




# Project Impact 📜🔧:

* **Better Career Choices:** Job seekers can make smarter career decisions by using data-driven insights, helping them find jobs that match their skills and interests.

* **Efficient Hiring for Employers:** Employers can improve their hiring processes, find top talent faster, and offer competitive compensation packages by leveraging the project's insights.

* **Informed Industry Decisions:** Industry analysts and businesses can gain valuable insights into employment trends, guiding them in making informed decisions about market strategies and workforce development.

* **Enhanced Business Strategy:** Businesses can develop data-driven strategies, identify emerging opportunities, and stay competitive in the job market.


# Acknowledgments 🙏:

We extend our sincere gratitude to Manish Hemnani for his invaluable mentorship and guidance throughout this project. His expertise significantly contributed to the project's success.


# Conclusion 🚀📈🔍:

* **Unlocking Job Market Insights:** "Job Analyst" demonstrates the power of data analysis in uncovering complex job market patterns. This project, a collaborative effort by Amit Porwal, Madhu Gupta, and Shubhum Pathak, highlights the importance of data-driven decision-making in the ever-changing job landscape.

* **Commitment to Excellence:** The project reflects the team's dedication to delivering excellence. It serves as a valuable resource for individuals seeking job insights and businesses aiming to stay competitive.

* **A Resource for All:** Whether you're a job seeker, employer, or industry analyst, "Job Analyst" offers a valuable tool to gain insights into job openings and market trends. It's a testament to the benefits of data-driven approaches in navigating the job market effectively.



#### [__For more interesting insights read the ppt file 📜__ ](https://bit.ly/3PsKIDU)



Thank You for visiting my project page.


























