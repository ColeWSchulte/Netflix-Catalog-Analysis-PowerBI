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
- **country:** Countries where the show was produced.
- **date_added:** Date when the show was added to the Netflix catalog.
- **release_year:** Year when the show was released.
- **rating:** Rating of the show.
- duration: Duration of the show.
- **listed_in:** Genres/categories of the show.
- **description:** Description of the show.

## Project Steps
### 1. Data Import and Transformation
**Tools Used:** Power Query in Power BI
- **Import Data:** Loaded the raw data from a CSV file ('netflix_titles.csv') into Power BI.
- **Transform Data:**
  - **Split Columns:** Split the 'country' and 'listed_in' coulumns by delimter to handle multiple values
  - **Removed Columns:** Removed 'director', 'cast', and 'description' columns as they are not relevant to my report
  - **Unpivot Data:** Unpivoted columns to normalize the data for better analysis
  - **Data Cleaning:** Removed duplicates, handled missing values, renamed columns, and ensured data types were correctly set

### 2. Data Modeling
**Tools Used:** Power BI Data Model
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

In the original dataset, each unique 'show_id' could be listed to multiple countries and categories. Because of this, I decided to utilize Bridge Tables to overcome the many-to-many relationships of  Region and Category. 


