# Crowdfunding-ETL_private

## Overview
We have been helping Britta from Independent Funding, a crowdfunding platform for funding independent projects or ventures, build a database to perform data analysis and create reports for company stakeholders as well as individuals who donate to projects.

## Resources
* Data Source: [backer_info.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/original_data/backer_info.csv), [campaign.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/exported_data/campaign.csv), [categories.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/exported_data/categories.csv), [contacts.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/exported_data/contacts.csv), [subcategories.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/exported_data/subcategories.csv)
* Software: Anaconda **2022.05**, Python **3.7.13**, Conda **22.9.0**, Jupyter Notebook **6.4.12**, Pandas **1.3.5**, PostgreSQL **15.1**, pgAdmin **6.15**

## Summary
We received one Excel file (containing campaign data in one sheet and contacts information in another) and a dataset (containing information about the backers who have pledged to the live projects) from Britta.

We used **Extract, Transform and Load (ETL)**  process that extracts, transforms, and loads data from multiple sources to a data warehouse or other unified data repository.

We started with first 2 steps: Extract and Transform. We created a new virtual environment using **Conda** package management system that runs the latest version of **Python 3.7** and contains all the Anaconda packages including **Jupyter Notebook** and named it PythonData. **Jupyter Notebook** is a powerful interactive computational environment that supports **Python** and is largely used for data analysis and visualization. We imported the data into Jupyter Notebook using [**os**](https://docs.python.org/3/library/os.html) module and read the data using [**pandas.ExcelFile**](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.ExcelFile.parse.html) function and loaded it into data frame using [**pandas.excel_read**](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_excel.html) function.  We used **Pandas**, a fast and powerful software library built on top of **Python**, to clean and manipulate the data.  

We created 4 new data frames from excel file using [**pandas.DataFrame**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) function and saved them as four csv files ([campaign.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/exported_data/campaign.csv), [categories.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/exported_data/categories.csv), [subcategories.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/exported_data/subcategories.csv), [contacts.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/exported_data/contacts.csv)) using [**pandas.to_csv**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) function with index flag set to False and encoding flag set to UTF8.

We read [backers_info.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/original_data/backer_info.csv) that was provided by Britta using [**pandas.read_csv**](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html) function and created a new data frame. We looped through data frame using [**pandas.iterrows**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.iterrows.html) function, converted each row into dictionary, iterated through each dictionary row, got the values for each row using list comprehension (a syntactic construct for creating a list based on existing lists) and added values to the list using Python's [**list.append**](https://docs.python.org/3/tutorial/datastructures.html) function. We created a new data frame using the list of values lists and saved the data as [backers_del1py.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/exported_data/backers_del1py.csv) file using [**pandas.to_csv**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) function with index flag set to False and encoding flag set to UTF8.

<img src="https://github.com/vkbt/Crowdfunding_ETL/blob/main/Resources/1_image_iterrows_append.png" width=100% height=100%>

We also wrote an additional code extracting raw data and adding it to a data frame using **regex** (patterns used to match character combinations in strings) and [**pandas.str.extract**](https://pandas.pydata.org/docs/reference/api/pandas.Series.str.extract.html) function and saved the data as [backers_del1re.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/exported_data/backers_del1re.csv) file using [**pandas.to_csv**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) function with index flag set to False and encoding flag set to UTF8.

<img src="https://github.com/vkbt/Crowdfunding_ETL/blob/main/Resources/2_regex_example.png" width=100% height=100%>

We checked data types of the the data frame using [**pandas.dtypes**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.dtypes.html) function. We used [**pandas.str.split**](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.split.html) function to split "name" column into two columns "first_name" and "last_name". 

<img src="https://github.com/vkbt/Crowdfunding_ETL/blob/main/Resources/3_pandas_str_split.png" width=100% height=100%>

We dropped "name" column using [**pandas.drop**](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.drop.html) function with parameter axis = 1 for columns and saved the data as [backers.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/exported_data/backers.csv) file using [**pandas.to_csv**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) function with index flag set to False and encoding flag set to UTF8.

Once we were finished with Extract and Transform steps, we began preparing for the next step in ETL process - Load. We downloaded and installed [**PostgreSQL**](https://www.postgresql.org) - an open source object-relational database system and [**pgAdmin**](https://www.pgadmin.org/) - an open source graphical management tool that serves as a development platform for PosgreSQL to help Britta create a crowdfunding database. We used [**Structured Query Language (SQL)**](https://en.wikipedia.org/wiki/SQL), a standard language for storing, manipulating and retrieving data in databases, to write and execute queries in pgAdmin.

We created an [**ERD**](https://app.quickdatabasediagrams.com/#/) (entity relationship diagram) flowchart that highlights different tables and their relationships. ERD flowchart is an important and useful tool that provides visual representation of the tables and gives a deeper understanding of the data and the database as a whole. We saved the database schema as a [crowdfunding_db_schema.sql](https://github.com/vkbt/Crowdfunding_ETL/blob/main/schema/crowdfunding_db_schema.sql).

<img src="https://github.com/vkbt/Crowdfunding_ETL/blob/main/schema/crowdfunding_db_relationships.png" width=50% height=50%>

We created a new Crowdfunding database in PostgreSQL, created tables by importing previously saved schema file [crowdfunding_db_schema.sql](https://github.com/vkbt/Crowdfunding_ETL/blob/main/schema/crowdfunding_db_schema.sql) and imported 5 csv data files. We performed a [data analysis](https://github.com/vkbt/Crowdfunding_ETL/blob/main/queries/crowdfunding_SQL_Analysis.sql) on the crowdfunding database by using SQL:

 - we retrieved the number of backers for live crowdfunding campaigns in campaign table using [**SELECT**](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-select/) statement, [**WHERE**](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-where/) and [**ORDER BY**](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-order-by/) clauses.

- we confirmed the accuracy of first query by running additional query on backers table by using [**SELECT**](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-select/) statement, [**COUNT**](https://www.postgresqltutorial.com/postgresql-aggregate-functions/postgresql-count-function/) function, [**GROUP BY**](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-group-by/) and [**ORDER BY**](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-order-by/) clauses

- we created a new table that has the first  name, last name, email address of each contact and the amount left to reach the goal for all "live" projects in descending order using [**SELECT INTO**](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-select-into/) statement, [**WHERE**](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-where/), [**INNER JOIN**](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-inner-join/) and [**ORDER BY**](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-order-by/) clauses and exported it into [email_contacts_remaining_goal_amount.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/exported_data/email_contacts_remaining_goal_amount.csv) file

- we created a new table for live campaigns, that contains the email address, first name, last name of each backer, company name and description, campaign id, end date and the remaining amount of campaign goal using  [**SELECT INTO**](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-select-into/) statement, [**WHERE**](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-where/), [**INNER JOIN**](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-inner-join/) and [**ORDER BY**](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-order-by/) clauses and exported it into [email_backers_remaining_goal_amount.csv](https://github.com/vkbt/Crowdfunding_ETL/blob/main/exported_data/email_backers_remaining_goal_amount.csv) file

<img src="https://github.com/vkbt/Crowdfunding_ETL/blob/main/Resources/4_SQL_query.png" width=100% height=100%>

## Challenge Overview

For this project we extracted, transformed and cleaned data using Python, Pandas and Jupyter notebooks. We created an ERD and a table schema. We built a new database in pgAdmin on the PostgreSQL server, loaded the data into a database. We performed a data analysis using SQL queries and exported the results into csv files.
