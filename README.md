# Movies-ETL

## Overview

The content streaming platform 'Amazing Prime' is sponsoring a hackathon for creating a movie popularity prediction model. As a data analyist, I have been tasked with providing a clean dataset for the hackathon participants to use. In this project repository, I have included the files storing the detailed ETL (Extract, Transform, & Load) process that I undertook for this project, as well as the automated pipeline I created to preform the ETL process with increased efficiency in the future. Below is a brief description of the contents for each jupyter notebook and relevant resources in the repository.

__*Resources/"wikipedia_movies.json", "movies_metadata.csv", "ratings.csv"*__ <br>

I sourced the dataset for the movie prediction hackathon from 3 main data files. First, I got data from a JSON file containing movies data scraped from Wikipedia. Then, I sourced a dataset called 'MovieLens' from Kaggle, which scraped data from the GroupLens website. From this dataset, I incorporated the 'movies_metadata' and 'ratings' CSV files in my ETL process.

__*Movies-ETL.ipynb*__ <br>

I extracted the three data sources above into pandas dataframes and performed exploratory analysis to discover any inconsistencies or corruption within the data. After I sussed out any bad data and data provided in an inconsistent form, I implemented a variety of solutions including parsing text data with RegEx and converting data to a consistent type for relevant columns. I then merged the Wikipedia data with the Kaggle movie data. After some additional data cleaning steps and column reorganization of the merged dataset, I turned to the ratings data. I transformed the ratings data to provide grouped counts for each rating provided, grouped by movie. I then created another dataframe merging the transformed ratings data with the merged Wikipedia and Kaggle data. After completing all data extraction and transformations, I loaded the merged movies dataframe and the raw ratings data into a SQL database.

__*ETL_function_test.ipynb*__ <br>

This file contains the first step to creating an automated ETL process for the movie data. I created a function, *extract_load_transform()*, that takes in the three data files as arguments and returns them as pandas dataframes.

__*ETL_clean_wiki_movies.ipynb*__ <br>

This file contains the function, *clean_movie()*, that cleans each movie data entry row in the Wikipedia data by sorting alternate titles and further consolidating the data by renaming redundant columns. The file also adds functionality to the *extract_transform_load()* function by implementing necessary code to clean the Wikipedia movie data.

__*ETL_clean_kaggle_data.ipynb*__ <br>

This file adds functionality to the *extract_transform_load()* function by incorporating code to clean the Kaggle data. The additional code also merges the Kaggle data with the Wikipedia data. It was determined on accounts of redundancy, between the Kaggle and Wikipedia data, that the Kaggle data was more consistent and preferrable in most cases. Where necessary, the code drops redundant Wikipedia data columns and fills in any missing data entries in Kaggle with Wikipedia data, where some values exist, to retain information wherever possible. The columns of the new movies dataframe are then reorganized and renamed, where necessary. Added code in the function also automates transforming the ratings data and merges it with the movies dataframe as a new movies dataframe with ratings data. 

__*ETL_create_database.ipynb*__ <br>

This file adds the final piece of code to the *extract_transform_load* function to complete the automated ETL data pipeline. Functionality is added the the *extract_transform_load* function to load the merged movies data frame and the raw ratings data into a SQL database. The function is then executed to confirm results consistent with expectations. The automated pipeline performed as expected, successfully completing all data extraction and transformation tasks, as well as loading the final data products into a functioning, accessible SQL database. I queried the loaded datasets for the total row counts to confirm the pipeline had completed the ETL process as expected. The count queries performed, along with their resulting output, are evidenced below. The automated pipeline performed successfully.


__*movies_query.png*__
![query](Resources/movies_query.png)

__*ratings_query.png*__
![query](Resources/ratings_query.png)