# Netflix-Content Catalog Analysis - Power BI Project
## Project Overview
This Power BI project is designed to analyze the Netflix catalog, focusing on geographical, genre, and content analysis. The goal is to demonstrate my proficiency in data analysis, data transformation, data modeling, and visualization using Power BI. This project is part of my portfolio to showcase my skills for a potential role in data analysis and data science.

## Dataset
The dataset used for this project is derived from Netflix and contains information about shows added to their catalog. The dataset includes the following columns:
- **show_id:** Unique identifier for each show.
- **type:** Indicates whether the content is a movie or a TV show.
- **title:** Title of the show.
- **director:** Director of the show.
- **cast:** Cast of the show.
- **country:** Countries where the show was added.
- **date_added:** Date when the show was added to the Netflix catalog.
- **release_year:** Year when the show was released.
- **rating:** Rating of the show.
- **duration:** Duration of the show.
- **listed_in:** Genres/categories of the show.
- **description:** Description of the show.

![netflix_data_rawdataset](https://github.com/ColeWSchulte/Netflix-Catalog-Analysis/assets/140651727/54a6d9d3-5eac-4a1c-acdc-128e72ace5ec)


## Project Steps
### 1. Data Import and Transformation
- **Import Data:** Loaded the raw data from a CSV file ('netflix_titles.csv') into Power BI.
- **Transform Data:**
  - **Split Columns:** Split the 'country' and 'listed_in' coulumns by delimter to handle multiple values
  - **Removed Columns:** Removed 'director', 'cast', and 'description' columns as they are not relevant to my report
  - **Unpivot Data:** Unpivoted columns to normalize the data for better analysis
  - **Data Cleaning:** Removed duplicates, handled missing values, renamed columns, and ensured data types were correctly set

### 2. Data Modeling
- **Fact Table:** Created a fact table 'FACT-netflix-catalog' with only 1 unique entry per 'show_id'
- **Dimension Tables:**
  - **'DIM-region':** Contains unique country id, name, and region
  - **'DIM-category':** Contains unique category id and name
  - **'DIM-addedDate':** Date table which contains date-related information for time-based analysis
- **Bridge Tables:**
  - **'BR-region':** Contains 'show_id' and the associated 'country_id'
  - **'BR-category':** Contains 'show_id' and the associated 'category_id'
- **Measures Table:** Created a Measures table to effectively store relevant measures
- **Relationships:** Established relationships between the fact, bridge, and dimension tables

![netflix_data model_structure](https://github.com/ColeWSchulte/Netflix-Catalog-Analysis/assets/140651727/76f4db93-6c22-445b-8805-91583b4f3271)


In the original dataset, each unique 'show_id' could be listed to multiple countries and categories. Because of this, I decided to utilize Bridge Tables to overcome the many-to-many relationships of  Region and Category. 

### 3. Data Analysis and Measures
- **Measures Created:**
  - **Average Measures:**
    - **Average Movie Duration:** Calculates the average movie duration in minutes
    - **Average TV Seasons:** Calculates the average number of TV Seasons 
  - **Count Measures:**
    - **Count of show_id - running total:** Calculates a running total of the count of 'show_id' and displays 0 if no values are found
      ![netflix_dax_runningTotal](https://github.com/ColeWSchulte/Netflix-Catalog-Analysis/assets/140651727/cea12454-6b35-4ae6-beca-646a3a172466)
    - **Total Content:** Calculates the count of all show_id and displays 0 if no values are found
      ![netflix_dax_totalcontent](https://github.com/ColeWSchulte/Netflix-Catalog-Analysis/assets/140651727/f7f0ba2f-f87c-46a7-96b3-2981051f5b93)
    - **Total Movies:** Calculates the count of all Movies and displays 0 if no values are found
    - **Total TV Shows:** Calculates the count of all TV Shows and displays 0 if no values are found
  - **Time Measures:**
    - **YearlyReleases** Calculates the count of content released based on the 'DIM-addedDate'[Year]
      ![netflix_dax_yearlyreleases](https://github.com/ColeWSchulte/Netflix-Catalog-Analysis/assets/140651727/440ddc1b-a8d6-47d0-b857-e62c69b5fbe3)
  - **Growth Measures:**
    - **YearlyGrowth:** Calculates the yearly growth by comparing CurrentYearReleases and PreviousYearReleases variables
      ![netflix_dax_yearlygrowth](https://github.com/ColeWSchulte/Netflix-Catalog-Analysis/assets/140651727/ea8a2663-e8a5-41dd-bcde-915165d26336)
    - **PositiveGrowth:** Evaluates if the 'YearlyGrowth" measure is greater than 0 for count and identification purposes
    - **CumulativeGrowth:** Calculates the total sum of positive yearly growth values over the dataset's period
      ![netflix_dax_cumulativegrowth](https://github.com/ColeWSchulte/Netflix-Catalog-Analysis/assets/140651727/bdca3966-abb6-4bde-b0d1-942034ea3b6f)
    - **RankByGrowth:** Ranks the DIM-region countries by the 'CumulativeGrowth' measure above
      ![netflix_dax_rankbygrowth](https://github.com/ColeWSchulte/Netflix-Catalog-Analysis/assets/140651727/87ee1583-0dcb-4839-973f-ffd02e528770)


### 4. Data Visualizations and Report
This report consists of several pages, each designed to provide insights into different aspects of the Netflix Catalog Data. Below is a detailed description of important features and purposes of each report page.
>[!Note]
>Due to limitations in the raw data, this report is analyzing the Netflix catalog from 2015-2021. Because of this, I themed the report as if I created this report in June of 2021.

- **Report Pages Created:**
  - **Overview:**
    - The purpose of this page was to give a high-level overview of the dataset
    - Slicers were added for all of the major filtering attributes (Content Type, Country, Genre, Year, Month)
    - Navigation buttons were added for all of the report pages
   ![netflix_report_overview](https://github.com/ColeWSchulte/Netflix-Catalog-Analysis/assets/140651727/208f954c-7301-4efa-9ea5-a4798156915b)
  - **Geographical Analysis:**
    - **Map Visualization:** Displays the number of content releases by country. The color of the hotspot indicates the volume of content released in in each country
    - **Content Releases of Top 5 Countries:** This chart shows the number of releases per year for the top 5 countries
    - **Production Investment for the Top 5 Growing Markets:** This chart displays the number of releases over time for the top 5 countries with increasing growth. This is to identify emerging markets and regions with growing production investment
  ![netflix_report_geographical](https://github.com/ColeWSchulte/Netflix-Catalog-Analysis/assets/140651727/a62162d9-3bcc-456e-b02e-7d8c95c9b329)
  - **Genre Analysis:**
    - **Top 10 Genres:** This chart is to show the distribution of releases and identify dominant genres
    - **Content Released for Top 10 Genres:** This chart displays the number of releases per genre over time to understand how preferences may change with time
    - **Production Investment for the Top 5 Growing Categories:** This chart displays the number of releases over time for the top 5 categories with increasing growth. This is to identify emerging markets and categories with growing production investment
  ![netflix_data_genre](https://github.com/ColeWSchulte/Netflix-Catalog-Analysis/assets/140651727/4ef9940f-cec6-4b36-8549-6ea0f8cbd865)
  - **Content Analysis:**
    - **Total Content by Rating Categories:** This chart is to show the distribution of content by their Maturity Rating
    - **Average Movie Duration by Year:** This chart is to show the average movie duration (minutes) to understand how movie length may change with time
    - **Average TV Seasons by Year:** This chart is to show the average TV Seasons to identify changes over time
    - **Total Content by Month and Type:** This chart break down the number of releases per month. This visualization can further be drilled down to week number & day of the week
    ![netflix_report_content](https://github.com/ColeWSchulte/Netflix-Catalog-Analysis/assets/140651727/e7851f90-21da-449e-9cbb-ad73b2229bb0)

## Future Improvements
While I am satisfied for what I was able to create, below are further modifications I would make if allocated more time:
- Optimize Report Pages and underlying DAX measures
  - Report Model could be further imporoved to allow for a more efficient and scalable model
- Improve Slicers/Filters on Reporting page
  - Syncing these visuals across pages and tailoring the report to a set target audience would allow for a more investigative and thorough findings
- Further Modifcations to Raw Data
  - The original dataset had a significant amount of discrepancies and errors, but I believe this could be further improved if I had access to the raw data source
  - Additionally I limited myself to only utlize PowerQuery for this cleanup as I wanted to spend more time with the tool, but it may have been more efficient to just edit the data in excel
- Add more statistical analysis themed visualization
  - With the raw data having so many discrepancies, I was hesitant to make predictive or more analytical visualizations that would skew findings

## Conclusion
This Power BI report provides a Descriptive analysis of the Netflix catalog, highlighting content, geographical, and genre analysis. The project demonstrates my ability to handle end-to-end data analysis tasks, from data import and transformation to modeling and visualization. This work showcases my skills in using Power BI to derive actionable insights from data, making it a valuable asset for a role in data analysis and data science.   



