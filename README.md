# CSCI-226-Advanced-Database-Systems
## Final Project (Fall 2023)

## Teammates:
- Kranti Walke
- Raksha Jagadish 
- Vaideki Muralitharan




## Table of Contents:
1.	Introduction	

- 1.1 Methodology

- 1.2 Domain Description	

2.	Dataset Details	

- 2.1 Sources for original dataset	

- 2.2 IMDb dataset files	

3.	Database Design	
4.	Prepare the IMDB Data to build the database.	

- 4.1 Feature Pre-processing	

5.	Database Schema	

- 5.1 Build MySQL database	

- 5.2 Below are the final created tables in our database:	

6.	SQL Queries
7.	Normal Forms	
8.	Visualizations	
9.	Analytics/Analysis	
10.	All Dataset links.	



# 1. Introduction
In this project, we embark on a journey to construct a MySQL database leveraging the Internet Movie Database (IMDb) dataset. Comprising seven compressed tab-separated-value (*.tsv) files, this dataset is regularly updated, though our project utilizes the snapshot from November 29, 2019. The project aims to:

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
## 4.1 Feature Pre-processing
The Feature Pre-processing of IMDB data is done using python. The IMDB_Feature_Pre-processing.py reads in the 7 data files and does the feature preprocessing of the IMDb data. After which, the desired set of tables are output as tab-separate-value (tsv) files.
![image](https://github.com/KrantiWalke/CSCI-226-Advanced-Database-Systems/assets/72568005/097dcb10-b3cd-47e4-97cb-9e16b2a8f613)

## <a name="Database_Tools/Technologies"></a> Database Tools/Technologies

MySQL Workbench: 
- A comprehensive tool for MySQL database modeling.

Jupyter Notebook:
- Extract, Transform, Load (ETL) with Python
- Python for Data Visualization
