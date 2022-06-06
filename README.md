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
