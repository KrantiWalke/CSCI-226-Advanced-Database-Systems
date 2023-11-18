# CSCI-226-Advanced-Database-Systems
## Final Project (Fall 2023)

## Teammates:
### Kranti Walke
### Raksha Jagadish 
### Vaideki Muralitharan




## Table of Contents:
+ [Data_Domain_-_IMDb_(Internet_Movie_Database)](#Data Domain - IMDb (Internet Movie Database)) </br>
+ [Sources_for_Datasets](#Sources for Datasets) </br>
+ [Database_Tools/Technologies](#Database Tools/Technologies) </br>

## <a name="Data_Domain_-_IMDb_(Internet_Movie_Database)"></a> Data Domain - IMDb (Internet Movie Database)

Serves as an online repository that compiles information pertaining to the entertainment industry.
We can find information about movies, TV shows, actors, user ratings, and other aspects of the film and television industry.
The IMDb Non-Commercial Datasets, 
- offer a well-organized collection of data  that are available for public use without commercial purposes.
Have a wide range of details about movies and TV shows, making it a one-stop hub for all things related to the big and small screen.
IMDb's data is derived from:
- movie studios, production companies, user contributions, official press releases, and publicly available information.



 
## <a name="Sources_for_Datasets"></a> Sources for Datasets

IMDb Non-Commercial Datasets: https://developer.imdb.com/non-commercial-datasets/

Data Location: https://datasets.imdbws.com/

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

## <a name="Database_Tools/Technologies"></a> Database Tools/Technologies

MySQL Workbench: 
- A comprehensive tool for MySQL database modeling.

Jupyter Notebook:
- Extract, Transform, Load (ETL) with Python
- Python for Data Visualization
