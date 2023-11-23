# CSCI-226-Advanced-Database-Systems
## Final Project (Fall 2023)

## Contributors:
- Kranti Walke
- Raksha Jagadish 
- Vaideki Muralitharan




## Table of Contents:
[1. Introduction](#1.Introduction)	

      - 1.1 Methodology
      - 1.2 Domain Description	

2.	Dataset Details	

      - 2.1 Sources for original dataset	
      - 2.2 IMDb dataset files	

3.	Database Design	
4.	Prepare the IMDB Data to build the database.
5.	Database Schema	

      - 5.1 Build MySQL database	
      - 5.2 Final created tables in our database:
      - 5.3 Table includes required columns, indexes, Foreign Keys, Triggers
      - 5.4 All the Stored procedures created

6.	SQL Queries
7.	Normal Forms	
8.	Visualizations	
9.	Analytics/Analysis	
10.	All Dataset links.	



## 1. Introduction
In this project, we embark on a journey to construct a MySQL database leveraging the Internet Movie Database (IMDb) dataset. Comprising seven compressed tab-separated-value (*.tsv) files, this dataset is regularly updated, though our project utilizes the snapshot from October 14, 2023. The project aims to:

1. Acquire proficiency in MySQL, a prominent database management system.
2. Understand fundamental database design principles, including Entity-Relationship diagrams, logical schema creation, and the concept of database normalization.
3. Develop skills in database querying, both through direct MySQL use and indirectly via Python.
4. Employ Python for the visualization of IMDb data.

## 1.1 Methodology:

- Analyzing the IMDb dataset to grasp its structure and content.
- Designing a relational database to effectively store the IMDb data.
- Developing an Entity-Relationship (ER) diagram to model our database.
- Applying feature engineering techniques and restructuring the IMDb data using Python.
- Establishing the MySQL database.
- Populating the database with the dataset.
- Implementing SQL schema including:
- 
      - Tables creation           
      - Key Definitions per tables
      - Referential Integrity Constraints per table
      - Triggers for each table
      - Stored Procedures for each table
      - Loading the dataset into tables
- Include the Functional Dependencies and any Multi-Valued Dependencies for your database and state whether they are free from violations for:
- 
      - 3rd Normal form 
      - Boyce-Codd Normal Form 
      - 4th Normal Form.
- Engaging in various SQL queries, from basic to complex, to interrogate the IMDb data.
- Conducting in-depth data exploration and visualization using Python.
- Interesting insights within data using supporting queries.

Throughout this project, we adhere to established SQL style conventions as outlined in the SQL Style Guide, favoring underscores in attribute names over camel case, aligning with the naming conventions in the IMDb data files.

## 1.2 Domain Description

The domain for the IMDb Non-Commercial Datasets is the entertainment industry, specifically the world of movies and television. IMDb (Internet Movie Database) is a widely recognized online database of films, television series, and the people involved in creating and starring in them. It serves as a comprehensive resource for information about movies, TV shows, cast and crew, user ratings, and more.

- Serves as an online repository that compiles information pertaining to the entertainment industry.
- We can find information about movies, TV shows, actors, user ratings, and other aspects of the film and television industry.
- The IMDb Non-Commercial Datasets offer a well-organized collection of data that are available for public use without commercial purposes.
- Have a wide range of details about movies and TV shows, making it a one-stop hub for all things related to the big and small screen.

IMDb's data is derived from:
-movie studios, production companies, user contributions, official press releases, and publicly available information.

# 2.	Dataset Details	
## 2.1 Sources for original dataset
IMDb Non-Commercial Datasets: https://developer.imdb.com/non-commercial-datasets/

Data Location: https://datasets.imdbws.com/

## 2.2 IMDb dataset files
IMDb data files :
- title.akas.tsv.gz:  (8 x 37476209)  Contains alternative titles, regions, languages, and attributes for IMDb titles.
- title.basics.tsv.gz: (9 x 10234938)  Provides fundamental details about IMDb titles, including type, primary title, and genres.
- title.crew.tsv.gz:  (3 x 10234938) Includes director and writer information for IMDb titles.
- title.episode.tsv.gz:  (4 x 7800118) Contains data about TV series episodes, including season and episode numbers.
- title.principals.tsv.gz: (6 x 58593659) Offers information about people involved in titles, their roles, and characters played.
- title.ratings.tsv.gz: (3 x 1359060) Provides user ratings and vote counts for IMDb titles.
- name.basics.tsv.gz:  (6 x 12923131) Contains details about individuals in the entertainment industry, including their 

Attributes  :

**title.akas.tsv.gz - Contains the following information for titles:**
- titleId (string) - a tconst, an alphanumeric unique identifier of the title
- ordering (integer) – a number to uniquely identify rows for a given title Id
- title (string) – the localized title
- region (string) - the region for this version of the title
- language (string) - the language of the title
- types (array) - Enumerated set of attributes for this alternative title. One or more of the following: "alternative", "dvd", "festival", "tv", "video", "working", "original", "imdbDisplay". New values may be added in the future without warning
- attributes (array) - Additional terms to describe this alternative title, not enumerated
- isOriginalTitle (boolean) – 0: not original title; 1: original title

**title.basics.tsv.gz - Contains the following information for titles:**
- tconst (string) - alphanumeric unique identifier of the title
- titleType (string) – the type / format of the title (e.g. movie, short, tvseries, tvepisode, video, etc)
- primaryTitle (string) – the more popular title / the title used by the filmmakers on promotional materials at the point of release
- originalTitle (string) - original title, in the original language
- isAdult (boolean) - 0: non-adult title; 1: adult title
- startYear (YYYY) – represents the release year of a title. In the case of TV Series, it is the series start year
- endYear (YYYY) – TV Series end year. " \N" for all other title types
- runtimeMinutes – primary runtime of the title, in minutes
- genres (string array) – includes up to three genres associated with the title

**title.crew.tsv.gz – Contains the director and writer information for all the titles in IMDb. Fields include:**
- tconst (string) - alphanumeric unique identifier of the title
- directors (array of nconsts) - director(s) of the given title
- writers (array of nconsts) – writer(s) of the given title 

**title.episode.tsv.gz – Contains the tv episode information. Fields include:**
- tconst (string) - alphanumeric identifier of episode
- parentTconst (string) - alphanumeric identifier of the parent TV Series
- seasonNumber (integer) – season number the episode belongs to
- episodeNumber (integer) – episode number of the tconst in the TV series

**title.principals.tsv.gz – Contains the principal cast/crew for titles.:**
- tconst (string) - alphanumeric unique identifier of the title
- ordering (integer) – a number to uniquely identify rows for given titleId
- nconst (string) - alphanumeric unique identifier of the name/person
- category (string) - the category of job that person was in
- job (string) - the specific job title if applicable, else '\N'
- characters (string) - the name of the character played if applicable, else '\N'

**title.ratings.tsv.gz – Contains the IMDB rating and votes information for titles**
- tconst (string) - alphanumeric unique identifier of the title
- averageRating – weighted average of all the individual user ratings
- numVotes - number of votes the title has received

**name.basics.tsv.gz – Contains the following information for names:**
- nconst (string) - alphanumeric unique identifier of the name of person
- primaryName (string) – name by which the person is most often credited
- birthYear – in YYYY format
- deathYear – in YYYY format if applicable, else '\N'
- primaryProfession (array of strings) – the top-3 professions of the person
- knownForTitles (array of tconsts) – titles for a person

# 3.	Database Design 
# 4.	Prepare the IMDB Data to build the database.
Feature Pre-processing

The Feature Pre-processing of IMDB data is done using python. The IMDB_Feature_Pre-processing.py reads in the 7 data files and does the feature preprocessing of the IMDb data. After which, the desired set of tables are output as tab-separate-value (tsv) files.
![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/097dcb10-b3cd-47e4-97cb-9e16b2a8f613)

# 5.	Database Schema
### 5.1 Build MySQL database
To build the IMDB MySQL database we followed the below steps:

### 5.1.1	Install MySQL workbench: 
https://dev.mysql.com/doc/workbench/en/wb-installing-windows.html
### 5.1.2	Creating a new MySQL connection: 
https://dev.mysql.com/doc/workbench/en/wb-getting-started-tutorial-create-connection.html
### 5.1.3	Create IMDb database in MySQL
a)	Create a schema and set INFILE ACCESS:
- Using imdb_TableCreation.sql
  
 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/db1417fb-73c3-41b0-9414-0f919f55362e)

b)	Use the schema to create a table in the database: 
- Using imdb_TableCreation.sql
- Includes:
      – Key Definitions
      – Referential Integrity Constraints
  
- Example: Movie dataset
 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/d8c5e9d0-4c2f-49cc-8495-b2687ee2f097)

c)	Create a trigger for each table operation: imdb_TriggereCreation.sql
 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/ee378623-de6c-4fd1-b8b0-a67d6ec8f250)

d)	Load the dataset in table: 
- Using imdb_LoadDataset.sql
 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/05668bd4-c7cc-4d8b-949b-94e88390a37a)


e)	Create Stored Procedures for certain operations like Add New Movie or Get Movie Details: 
- Using imdb_StoredProceduresCreation.sql
 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/830fbeff-8db4-4e8f-8bf9-1836d82c13c7)

## 5.2 Below are the final created tables in our database:
 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/1b3096ad-0a4a-4774-999b-e2adaf03fe8b)

## 5.3 Each table includes required columns, indexes, Foreign Keys, Triggers:
 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/27ff5980-ef20-4e26-a04a-7a723ad1e4c6)

## 5.4 All the Stored procedures created
- Using imdb_StoredProceduresCreation.sql
  
![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/b31f0570-0dae-432c-9a5c-f5a6dfb47a91) ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/25cbe354-c40e-4317-9aa1-33841b135acd)


# 6.	SQL Queries:

After creating and loading data into the database, we can now pose queries to it. In the file imdb_sqlQueries.sql we consider more than 40 questions and answer them by querying the IMDb database. 

Some Good queries from imdb_sqlQueries.sql :
[1]	How many movies are made in each genre each year?

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/e8cae552-e270-496c-81d1-526f577a12df)

[2]	What genres are there? How many movies are there in each genre?

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/a563cf26-567f-441b-a7db-e92cb2571d0f)

[3]	What is a typical runtime for movies in each genre?

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/ce214eaf-9eb3-4e0b-8366-ba15c9260ac1)

[4]	No. of movies directed by the director and in which genre alphabetically by name and highest count as per genre?

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/d6546bab-03e3-42ef-8915-b7d816191b1f)

[5]	Top 10 movies on basis of region

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/ec1d34c8-1678-4b44-8313-f6a545bda35a)

[6]	First 50 entries WriterName according to their series and their genres.

![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/182e8deb-19fb-468b-b1ce-484e48c64c55)
 
[7]	Count of movies in each genre, according to the highest first HAVING movies greater than 20000.

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/2fa02319-fe55-469c-832e-197c99434cb7)

[8]	Series with More Episodes Than the Average Number of Episodes Per Series:

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/3a372064-d65c-4930-810c-12f6e05c82ac)

[9]	Writers with More than Average Number of Votes for Their Movies:

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/59b541ae-56c8-41d5-965c-a1950fe913b0)

[10]	Directors Who Have Worked in Both Movies and Series:

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/3537f742-7f71-4f27-9aa4-cc47134498c5)

[11]	Movies with Most Diverse Genres:

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/8f627ace-ffed-4c56-b802-94201f8e1827)

[12]	Writers Who Have Worked in Both Highest and Lowest Rated Movies:

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/c33945bf-a4c1-440d-a208-925c542d9866)

[13]	Find the average runtime of movies for each genre:

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/2c0e177d-3d54-48a3-9d2a-906c2e8ca6c3)

[14]	Find directors who have directed more than 5 movies:

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/b9cbebe0-ca5a-43d9-bab4-a0b56d5733b6)

[15]	Find actors who have acted in both movies and series:

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/c9a50b14-6bc2-4719-a4b2-fd48ca0f0e82)

[16]	Determine the average number of votes for movies by release year:

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/5a34ef67-699b-447c-b16a-f7b9f38804cf)

[17]	List series with a higher average rating than the average rating of all series:

 ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/ae59dac5-2274-4d36-9652-dc6164bfc5bf)

 
# 7.	Normal Forms

# 8.	Visualizations
We have saved some of the queries in CSV files in a folder named QueryResultedCSV

![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/46b40ab6-b06a-49e5-8864-43a8223a67ca)

We read these csv files using pandas library in python. 

In the notebook Visualizations.ipynb we used the query results from the IMDb database to explore and visualize the IMDb dataset using pandas and matplotlib. 

This notebook is by no means a thorough exploration of the IMDb dataset. Its purpose is to visualize the retrieved data with the pandas package. 

1)	No. of movies directed by the director and in which genre alphabetically by name and highest count as per genre?

![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/d8adf07f-1668-4561-96d3-7c0b484bb8d4)

2)	Top 10 movies on basis of region

![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/b4c886c3-ea7a-42a1-a091-f9a5b677c7f7)

3)	First 50 entries WriterName according to their series and their genres.

   ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/8da336e2-75bf-44e3-9305-4a45e5c74e50) ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/afcdd670-e175-4ca0-84a5-e29b8c952e6c)

4)	Count of movies in each genre, according to the highest first HAVING movies greater than 20000.

![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/1c695425-be2c-4904-bed3-4a052cd75372) ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/9147397e-80c7-46b3-a862-20f51168f5d3)

5)	Count the occurrences of each genre per writer

![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/8354c071-a031-4c4a-a385-ece72c3ea875)

6)	Find the total number of movies released each year:

- a.	Total Movies Released by Decade

![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/78663330-93c5-4ad1-ac83-9649773ca0cc)

- b.	Trend of Movie Releases Over Decades

![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/2bd2baa2-df12-4eb6-a54e-a6d7e7561176)

7)	List series along with their genres

![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/05619d11-104b-4919-ad64-096a65cc3280) ![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/196331d2-5ee1-421f-9ccc-9dcece004d97)

8)	 Genre Distribution (series along with their genres)

![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/bbe3506a-87d3-4f27-ab08-622ed6143027)

9)	 What is a typical runtime for movies in each genre?

![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/4d0c6586-6aba-4d7a-93b7-48e4456404d2)

10)	What genres are there? How many movies are there in each genre?

![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/915944ef-0739-407f-8047-d97f675e9564)

11)	How many movies are made in each genre each year?

![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/a75b3056-936b-4d42-90be-d073e3a171b5)




# 9.	Analytics/Analysis


# 10.	 All Dataset links.

https://drive.google.com/drive/folders/1enQdPtuilduCgRHh5nHBHcLGXgpNPEPL?usp=sharing





















## <a name="Database_Tools/Technologies"></a> Database Tools/Technologies

MySQL Workbench: 
- A comprehensive tool for MySQL database modeling.

Jupyter Notebook:
- Extract, Transform, Load (ETL) with Python
- Python for Data Visualization
