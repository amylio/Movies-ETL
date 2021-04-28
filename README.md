# Movies-ETL

An exercise in performing an Extract, Transform, Load (ETL) process to create data pipelines using Python, Pandas and PostgreSQL using very large data files.

![image](https://github.com/amylio/Movies-ETL/blob/main/MOD8_Challenge_Submission/Resources/Images/ETL-monitoring.png)

## Overview

The purpose of this project was to create an automated pipeline that takes in new data, performs the appropriate transformations, and loads the data into existing tables that is connected to a database. The chosen topic is all about Movies from 1990 to 2018 and combining the information from 3 different resources.

## Process

Create an ETL pipeline using Jupyter Notebooks and PostgreSQL from raw data to SQL database.

* **Extract:** read data from multiple sources using Python. Data sourced from:
	* **Wikipedia:** (format: .json, file size: 6.2MB) 7,311 thousand movie titles that include information about the movies, budgets, box office returns, cast/crew, production and distribution.
	* **Kaggle:** - 2 files (format: .csv)
		* a metadata file from [The Movie Database](https://www.themoviedb.org/) containing movie details with 45.5 thousand entries. (File size: 34.4MB)
		* a dataset from [MovieLens](https://movielens.org/) containing over 26 million movie ratings/review. (File size: 709.6MB)

* **Transform:** Clean and structure data using Pandas and regular expressions (RegEx) to achieve desired form. (i.e. using RegEx to parse data and transform text into numbers.
	* Deleting bad data (corrupted or missing), removing duplicate rows, and consolidating columns.
	* Using RegEx to parse data and transform text into numbers.

* **Load:** Export transformed data into a database.

## Results

Ultimately, we were able to clean, merge the datasets and export the two new tables into PostgreSQL by using Python. The final results created a movies table with 6,052 rows. A 17% reduction from the original of 7,311 and a ratings table with 26,024,289 rows.

![movie](https://github.com/amylio/Movies-ETL/blob/main/MOD8_Challenge_Submission/Resources/movies_query.png)

![ratings](https://github.com/amylio/Movies-ETL/blob/main/MOD8_Challenge_Submission/Resources/ratings_query.png)

## Issues

Working with such large files presented issues along the way. For example in the module practice run, committing the repository to Github resulted in an error because the resource file from MovieLens was too large. Github has a strict 100MB limit. Attempts to resolve this issue using Git LFS and clear the cache were unsuccessful. I attempted to:
* git rm --cached to remove the large ratings.csv file
* git push rewritten, smaller commit

Each attempt resulted in `remote: error: File ratings.csv.zip is 169.99 MB; this exceeds GitHub's file size limit of 100.00 MB` regardless of the `git rm --cached` command.

Attempts to have the file tracked through `git lfs track "*.csv"` and have the file uploaded utilizing LFS also resulted in an error. 

Also, extracting and loading the ratings data (26 million rows) into the database took more than 3 hours to complete in the practice file and 2 hours to complete when executing [Deliverable 4 file](https://github.com/amylio/Movies-ETL/blob/main/MOD8_Challenge_Submission/ETL_create_database.ipynb).

**Practice File Results**

![timestamp](https://github.com/amylio/Movies-ETL/blob/main/MOD8_Challenge_Submission/Resources/Images/timestamp_ratings_TTL.png)

**Deliverable 4 File Results**

![timestampfinal](https://github.com/amylio/Movies-ETL/blob/main/MOD8_Challenge_Submission/Resources/Images/TimedResults-TTL.png)

## Summary

Overall, this was a very dense topic to learn and complete in one week. The process of reviewing the data and knowing what to "clean" was challenging, including cross comparison between the datasets, as well as, learning how to use RegEx to parse the text. I expect that to become an expert in ETL, especially RegEx outside of class would require extensive practice and application using real-life examples. I am hoping that with time, I can apply this learning to prepare large datasets for analysis.  

## Resources
* **Software:** Python 3.7.9, Anaconda 4.9.2, Jupyter Notebooks 6.1.4, PostgreSQL 4.28
* **Libraries:** Pandas, SQLAlchemy, NumPy
* **Troubleshooting:** [Deleting Cache](https://docs.github.com/en/github/managing-large-files/removing-files-from-a-repositorys-history), [Using Git LFS](https://git-lfs.github.com/)
* **Files:** [Wikipedia Json](https://github.com/amylio/Movies-ETL/blob/main/MOD8_Challenge_Submission/Resources/wikipedia-movies.json), [Movie Database Metadata](https://github.com/amylio/Movies-ETL/blob/main/MOD8_Challenge_Submission/Resources/movies_metadata.csv.zip), and [MovieLens Ratings](https://www.kaggle.com/rounakbanik/the-movies-dataset?select=ratings.csv)  

## Grading Feedback
"Congratulations on an outstanding homework assignment! You were able to deliver on writing an ETL function to read three different files. All three of these datasets were converted to DataFrames and properly formatted and displayed correctly!

Great job with your data extraction process, all TV shows are filtered out, extracted and the cleaned data type is converted to a DataFrame and displayed. As a side note well done successfully using a try-except block! This is a job well done! And you should be proud!

Now, I have to say how impressed I am with the extraction of the Kaggle metadata! You were able to not only clean the data but also, you merged datasets, the “movies” DataFrame is created and all four tasks are performed and all three tasks are completed during the extraction/transformation of the MovieLens rating data.  

Finally, you were able to successfully create the movie database, while simultaneously being able to drop the ratings table, and you moved the MovieLens rating to the SQL ratings table. Sweet job getting the ETA displayed!

Keep up the amazing work and this awesome flow you have been able to establish!"
