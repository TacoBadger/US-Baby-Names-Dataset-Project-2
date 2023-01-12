# US Baby Names Dataset (Project 2)
![](https://github.com/TacoBadger/US-Baby-Names-Dataset/blob/main/Assets/banner.png?raw=true)

## Introduction
In this project, I will work with the most popular baby names in the US. The dataset is a public dataset made available through Kaggle, click the link below to see to see the database.

-  [US Baby Names](https://www.kaggle.com/datasets/kaggle/us-baby-names)

In this project, I will start playing around with SQL to get access to data, clean the data and analyze the data. The logic behind SQL is very similar to any other tools used for data analysis. I will use [DB Browser for SQLite](https://sqlitebrowser.org/). This is a visual, open source technology used to create, design, and edit database files compatible with SQLite. This platform allows users and developers to create databases, search, and edit data via a spreadsheet-like interface.


## Author
- [@TacoBadger](https://github.com/TacoBadger)

## Methods
- [Questions](#questions)
- [Definitions](#important-definitions)
- [Import the dataset](#import-the-dataset)
- [Show the dataset](#show-the-dataset)
- [Counting](#counting)
- [Key Findings](#key-findings)
- [What is Next?](#what-is-next)

## Questions

So here the few questions I want to figure out with this dataset:
- What are the most popular names overall by year in the dataset?
- What is the top ten names for females and males?
- What is the top names per state in the last 3 years in the dataset?

## Definitions

Here are a few defintions before we get started.

**Structured Query Language** (SQL) is a standardized programming language that is used to manage relational databases and perform various operations on the data in them. 

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

## Import the dataset

I downloaded the [dataset](https://www.kaggle.com/datasets/kaggle/us-baby-names) it is a zip file. I made a new folder called "US Baby Name Analysis". Going forward, I will save all my csv files there. 

The zip file cointains two csv files:
-  NationalNames.csv
-  StateNames.csv

I uploaded the files in DB Browser and named it accordingly; national_names_baby and state_names_baby. I also created a table with the right fields. You can follow this here [tutorial](https://www.youtube.com/watch?v=TOqI-KiTBKU) if you are stuck.


I also named the file national_names_baby and state_names_baby which are the terms I will use in this script. The data types, I will work with are as follows:
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

The *SELECT * command will return all the tables in the dataset.*

Now we will look and filter through the columns that we want to work with.

You can also check the rows for nulls. 

You can always change the limit to any number, so you can get a better overview.


## Show the dataset



You define what you want to see after the SELECT. If you want to see all tables, simply type a  *.

In the example below I have decided I wanted to see 2 tables and constrain the results to 10 rows.

```bash
SELECT * FROM national_names_baby LIMIT 10

SELECT * FROM state_names_baby LIMIT 10
```
The result will be as follows:

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
     |

## Counting

Let's define the function COUNT and DISTINCT before using them:
- COUNT(ALL expression) evaluates expression for each row in a group, and returns the number of nonnull values.
- COUNT(DISTINCT expression) evaluates expression for each row in a group, and returns the number of unique, nonnull values.

Now we will use the dataset state_names_baby to count how many genders there are and how many different states there are. We will use the following query:

```bash
# to check and count how many genders and state
SELECT count(distinct Gender), count(distinct State) FROM state_names_baby
```

| Count(distinct Gender)      | Count(distinct State) |
|-------------------	        |------------------	|
| 2                          	| 51                |

The next thing I want to figure out is how many different male and female names do we have? for that I just need to type in the query below to get the result.

```bash
SELECT Gender, sum(Count) FROM state_names_baby group by Gender
```

| Gender                      | Sum(Count) |
|-------------------	        |------------------	|
| F                         	| 143770075                |
| M                         	| 155113251                |


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

Let's start with: What are the most popular names overall and which year? From here I wanted to create a temporary table for my visualizations too. So first we need to filter out the data that we need before making the temporary table.

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

![](https://user-images.githubusercontent.com/11693256/172169884-82c12bef-938d-4f1f-a38a-6f85fddbf2b2.png)

We have a new table for filtering and sorting. This is where we used a new function ROWNUM() and partition and you will also noticed that the command has 2 selects. This is called a sub query.

A **subqery** is a query that is nested inside a larger query just like in RStudio where it is also called nested.

Which is a great example of sub queries and inside it are different kind of functions.

## Key Findings
Tableau Visualizations are used to summarize the key findings, we aim for you to understand the viz within 5 seconds.

- What are the most popular names overall in the dataset?

![](https://github.com/TacoBadger/US-Baby-Names-Dataset/blob/main/Assets/Most%20Popular%20Names%20Overall%20by%20Year.png?raw=true)

- What is the top five names for females?

![](https://github.com/TacoBadger/US-Baby-Names-Dataset/blob/main/Assets/10%20Most%20Popular%20Names%20for%20Females%20Overall.png?raw=true)

- What is the top five names for males?

![](https://github.com/TacoBadger/US-Baby-Names-Dataset/blob/main/Assets/10%20Most%20Popular%20Names%20for%20Males%20Overall.png?raw=true)

- What is the top three names per state in the dataset?

![](https://github.com/TacoBadger/US-Baby-Names-Dataset/blob/main/Assets/Top%20Names%20per%20State%20in%20the%20last%203%20Years.png?raw=true)


## What is next?
We are now finished with our second dataset practice with SQL. Now we can get a better overview of what we could do better on this dataset we worked with.

- I could have still improved more on the datastory telling by removing some of the clutter and not that relevant information on my documentation. Basically just add all important notes, keywords, visuals and keypointers for our target audience.
- I could have still improved in my data visualization even if using a different platform for it, in our practice we used Tableau Public. A good practice to always keep in mind is to make your visual very easy to understand that the target audience can understand it within 5 seconds.

Always take note of this specific considerations to help you identify potential distractions, this applies to me and also to you starting in data analytics. 
- **Not all data are equally important**. Use your space and audience’s attention wisely by getting rid of noncritical data or components.
- **When detail isn’t needed, summarize**. You should be familiar with the detail, but that doesn’t mean your audience needs to be. Consider whether summarizing is appropriate.
- **Ask yourself: would eliminating this change anything?** No? Take it out! Resist the temptation to keep things because they are cute or because you worked hard to create them; if they don’t support the message, they don’t serve the purpose of communication.
- **Push necessary, but non‐message‐impacting items to the background**. Use your knowledge of pre attentive attributes to de‐emphasize. Light grey works well for this.

- I could also have improved my data documenation and visuals by not over complicating it, sometimes 2 variables in a data visualization can be the most powerful thing in the world.

On the next project we will still work with SQL but let us improve more on our datastory telling and tableau visuals this time. See you on our next project!
