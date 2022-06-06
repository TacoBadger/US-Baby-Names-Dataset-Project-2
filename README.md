# US Baby Names Dataset
![](https://github.com/TacoBadger/US-Baby-Names-Dataset/blob/main/Assets/banner.png?raw=true)

## Analysis of the US Baby Names in Kaggle.
Worked with the dataset to find the Most Popular Names in the US. The dataset is a public dataset made available through Kaggle. Please do take note that this document is for practice purposes only and it does not include any marketing of the titles involved. 

Also we cannot upload the dataset manually because of the file size so we will link it below. 

-  [US Baby Names](https://www.kaggle.com/datasets/kaggle/us-baby-names)

## Author
- [@TacoBadger](https://github.com/TacoBadger)

## Methods
- [Motivation](#motivation)
- [Questions I want to answer](#questions-i-want-to-answer)
- [Important Definitions](#important-definitions)
- [Importing the dataset from Kaggle to see what tables we have in the dataset](#importing-the-dataset-from-kaggle-to-see-what-tables-we-have-in-the-dataset)
- [Cleaning the dataset and sorting it accordingly](#cleaning-the-dataset-and-sorting-it-accordingly)
- [List of Names, Year, Gender, State and Count](#list-of-names-year-gender-state-and-count)
- [Checking the data and getting an overview of the findings I need](#checking-the-data-and-getting-an-overview-of-the-findings-i-need)
- [The Use of all SQL Queries and Functions](#the-use-of-all-sql-queries-and-functions)
- [Let's do some basic analytics](#lets-do-some-basic-analytics)
- [Query Run Order](#query-run-order)
- [Sub Queries and Functions](#sub-queries-and-functions)
- [Key Findings](#key-findings)
- [Explore our Tableau Public](#explore-our-tableau-public)
- [Explore our Notebook](#explore-our-notebook)

## Motivation

I'll be using this script or dataset to practice my knowledge on Data Analysis using SQL Language, which should be a must tool for every data scientist - both for getting access to data, cleaning the data and analyzing the data. The logic behind SQL is very similar to any other tool or language that used for data analysis (excel) and for those that used to work with data, should be very intuitive.

But for this practice, I will be using the platform [DB Browser for SQLite](https://sqlitebrowser.org/). This is a visual, open source technology used to create, design, and edit database files compatible with SQLite. This technology allows users and developers to create databases, search, and edit data via a spreadsheet-like interface and it also accpets SQL commands, functions but not all of it, we will practice all the codes and functions that works in this platform with this documentation.

We will also be practicing our [Tableau](https://public.tableau.com/en-us/s/) skills with this dataset.

# Questions I want to answer

So here the few questions or problems I want to solve or figure out in this dataset.
- What are the most popular names overall by year in the dataset?
- What is the top five names for females and males?
- What is the top names per state in the last 3 years in the dataset?

## Important Definitions

**Structured Query Language** (SQL) is a standardized programming language that is used to manage relational databases and perform various operations on the data in them. In our case we are using SQL Lite which is just similar to SQL the only difference is:

**SQL** is a query language which is used by different SQL databases. It is not a database itself.

**SQLite** is a database management system itself which uses SQL.

Usually in performance and advances analytical functionalities too.
But we will use SQL language to write queries that would pull data from the DB, manipulate it, sort it, and extract it.
Most of the script would be into SQL Language. Other than that, there are some other very useful concepts/features that we will use:
- table creation
- Updating data in the DB
- functions like creating a temp table, returning data that we only need.

**Tableau Public** is a free platform to explore, create and publicly share data visualizations online. With the largest repository of data visualizations in the world to learn from, Tableau Public makes developing data skills easy.

Let's get started!

## Importing the dataset from Kaggle to see what tables we have in the dataset

I downloaded the [dataset](https://www.kaggle.com/datasets/kaggle/us-baby-names) usually it appears to be a zip file but you can just extract it in a new folder, I made a folder called "US Baby Name Analysis" and save all my csv files there. 

You can also try to just open the database in SQLite file included in the dataset, it would be the same dataset but I wanted to try importing the dataset so I don't need to figure it out sooner or later. It includes two csv file.
-  NationalNames.csv
-  StateNames.csv

I uploaded the file in DB Browser and named it accordingly national_names_baby and state_names_baby. I also created a table with the right fields. You can follow this [tutorial](https://www.youtube.com/watch?v=TOqI-KiTBKU) if you are stuck.

I also named the file national_names_baby and state_names_baby which are the terms I will use in this script.
- ID - Integer
- Name - Text
- Year - Integer
- Gender - Text
- Count - Integer
- State - Text

Double check to make sure you have the same fields too.

You can also view the data so you know what data it has.

```bash
SELECT * FROM national_names_baby

SELECT * FROM state_names_baby
```

*SELECT * commands to return everything in the dataset.*

## Cleaning the dataset and sorting it accordingly

Checking the rows for nulls and other variables. You can always change the limit to any number so you can get a better overview or look at a few rows. You can also filter it on the browse data tab.

In this example we look and filter through the columns that we want to work with.

You define what you want to see after the SELECT, * means all possible columns. You choose the table after the FROM, you add the conditions for the data you want to use for example we used LIMIT which only returns a few rows based on how many you want.

```bash
SELECT * FROM national_names_baby LIMIT 10

SELECT * FROM state_names_baby LIMIT 10
```
## List of Names, Year, Gender, State and Count

national_baby_names
| ID        	                | Name            	| Year            	| Gender           	| Count           	|
|-------------------	        |------------------	|-------------------|------------------	|------------------	|
| 1                          	| Mary              | 1880             	| F                 | 7065              |
| 2                  	        | Anna	            | 1880             	| F                 | 2604              |
| 3                           | Emma              | 1880            	| F                 | 2003              |
| 4                           | Elizabeth         | 1880            	| F                 | 1939              |
| 5                           | Minnie            | 1880            	| F                 | 1746              |
| 6                           | Margaret          | 1880            	| F                 | 1578              |
| 7                           | Ida               | 1880            	| F                 | 1472              |
| 8                           | Alice             | 1880            	| F                 | 1414              |
| 9                           | Bertha            | 1880            	| F                 | 1320              |
| 10                          | Sarah             | 1880            	| F                 | 1288              |

state_names_baby
| ID        	                | Name            	| Year            	| Gender           	| State           	| Count           	|
|-------------------	        |------------------	|-------------------|------------------	|------------------	|------------------	|
| 1                          	| Mary              | 1880             	| F                 | AK                | 14 |
| 2                  	        | Annie	            | 1880             	| F                 | AK                | 12 |
| 3                           | Anna              | 1880            	| F                 | AK                | 10 |
| 4                           | Margareth         | 1880            	| F                 | AK                | 8  |
| 5                           | Helen             | 1880            	| F                 | AK                | 7  |
| 6                           | Elsie             | 1880            	| F                 | AK                | 6  |
| 7                           | Lucy              | 1880            	| F                 | AK                | 6  |
| 8                           | Dorothy           | 1880            	| F                 | AK                | 5  |
| 9                           | Mary              | 1880            	| F                 | AK                | 12 |
| 10                          | Margaret          | 1880            	| F                 | AK                | 7  |

You can filter through the browse tab too.

![](https://github.com/TacoBadger/US-Baby-Names-Dataset/blob/main/Assets/Filtering%20NA.png?raw=true)

And you can also skim through the data when you remove the limit.  It doesn't have much null values and duplicates so it is already okay for cleaning and further filtering and sorting to find out the answers to the questions we need.

You can also have a summary of how many the rows for each dataset.Have a summary of the rows and the column names.

```bash
SELECT count(1) as rows, count(Id), count(Name), count(Year), count(Gender), count(Count)
FROM national_names_baby

SELECT count(1) as rows, count(Id), count(Name), count(Year), count(Gender), count(State), count(Count)
FROM state_names_baby
```
| Rows        	   | Count(ID)          | Count(Name)       | Count(Year)     	| Count(Year)      | Count(Gender)   | Count(State)    | Count(Count)     |
|------------------|------------------	|-------------------|------------------	|------------------|-----------------|-----------------|------------------|
| 1825433          | 1825433            | 1825433           | 1825433           | 1825433          | 1825433         | 1825433         | 1825433          |

| Rows        	   | Count(ID)          | Count(Name)       | Count(Year)     	| Count(Year)      | Count(Gender)   | Count(State)    | Count(Count)     |
|------------------|------------------	|-------------------|------------------	|------------------|-----------------|-----------------|------------------|
| 5647426          | 5647426            | 5647426           | 5647426           |5647426           | 5647426         | 5647426         | 5647426          |

## Checking the data and getting an overview of the findings I need

This is the most basic query. The only must parts of a qeury is the SELECT and the FROM. In this method, we will also use the function COUNT and DISTINCT:
- COUNT(ALL expression) evaluates expression for each row in a group, and returns the number of nonnull values.
- COUNT(DISTINCT expression) evaluates expression for each row in a group, and returns the number of unique, nonnull values.

How many genders and states in the dataset state_names_baby? We will only check this dataset because this has the most valuable data that we need. It has the ID, Name, Year, State, Gender and Count.

I also checked what are the states in the dataset state_names_baby.

```bash
# to check and count how many genders and state
SELECT count(distinct Gender), count(distinct State) FROM state_names_baby
```

| Count(distinct Gender)      | Count(distinct State) |
|-------------------	        |------------------	|
| 2                          	| 51                |

```bash
# to check the names of the state
SELECT distinct State FROM state_names_baby
```
And the code shows 51 states.

How many male names and how many female names? I'll be mainly using the state_names_baby dataset because it has more relevant data than the national_baby_names dataset.

```bash
SELECT Gender, sum(Count) FROM state_names_baby group by Gender
```

| Gender                      | Sum(Count) |
|-------------------	        |------------------	|
| F                         	| 143770075                |
| M                         	| 155113251                |

Wanted to how many rows for each state, name, gender and added a new column called births which is the sum of the count by each name. 

Here we used the command GROUP BY. 

The GROUP BY clause a selected group of rows into summary rows by values of one or more columns. The GROUP BY clause returns one row for each group.

```bash
SELECT state, name, gender, sum(count) as births FROM state_names_baby GROUP BY state, name, gender
```
And it returned a total of  304918 rows.

From here we got a good overview of what we need.

## Let's do some basic analytics

Here we are starting to look at the data at more aggregated level. Instead of looking on the raw data we will start to grouping it to different levels we want to examine. In this example, we will base it by State, Names and Gender and we are using state_names_baby dataset.

Here we will sort and filter the cleaned data to find out the answers to our questions. We will still use the same functions as earlier like SELECT, COUNT, LIMIT and ORDER BY/GROUP BY.
- A SELECT statement retrieves zero or more rows from one or more database tables or database views.
- The COUNT() function returns the number of rows that matches a specified criterion.
- The ORDER BY keyword is used to sort the result-set in ascending or descending order.
- The LIMIT command also limits the return of data in the DB Browser.

We will be also using CREATE TEMPORARY TABLE to save csv files to create for visualizations.
- TEMP TABLES are used to store data temporarily and they can perform CRUD (Create, Read, Update, and Delete), join, and some other operations like the persistent database tables. So you can just make a temp table and export it as a CSV file.

## The Use of all SQL Queries and Functions

Let's start with: What are the 3 most popular names overall and which year? From here I wanted to create a temporary table for my visualizations too. So first we need to filter out the data that we need before making the temporary table.

```bash
#filter it first
SELECT State, Name, Year, sum(Count) as Total
FROM state_names_baby
GROUP BY State, Name
```

This is the filtered and sorted data we need to answer our first question, we need to filter it more to find the top names for each states and which year. We will create a temporary table because we will use this for more filtering and sorting.

```bash
CREATE TEMPORARY TABLE all_years as
SELECT State, Name, Year, sum(Count) as Total
FROM state_names_baby
GROUP BY State, Name
```
You can view the data on the tab called Browse Data and a drop down column choose the temp.all_years.


![Photo](![image](https://user-images.githubusercontent.com/11693256/172169884-82c12bef-938d-4f1f-a38a-6f85fddbf2b2.png)
