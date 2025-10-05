# EXPERIMENTAL SETUP

To run the recommendation models presented in the paper (i.e., six state-of-the-art Collaborative Filtering algorithms, namely **ItemKNN**, **UserKNN**, **BPR**, **SVD**, **VAECF**, and **NEUMF**), we used the Cornac framework, which generated the recommendations for each user and it generates consistently formatted lists that can be fed to CONFIGRE, P-Fair, and CP-Fair. In addition, datasets were randomly separated into a test set (20%) and a train set (80%).

We have performed a grid search of the hyper-parameters for each recommendation model in the two datasets. For each user, we generated the *top-1000* recommendations (denoted in the paper as the top-𝑛) to then re-rank the *top-𝑘* (set up to 10) through the proposed CONFIGRE algorithm. To evaluate recommendation effectiveness, we measure the ranking quality of the lists by measuring the Normalized Discounted Cumulative Gain (NDCG)

# Datasets Overview

This repository contains four enriched datasets with geographical metadata for analysis in various domains. Each dataset is provided as a CSV file with detailed attributes relevant to its specific context.

## 1. Movies Dataset (`movies.csv`)
- **Filename**: `movies.csv`
- **Description**: The items of the MovieLens-1M dataset, with geographical production data.
- **Contents**: Contains 3,600 movies.
- **Geographical Data**: Movies are associated with countries of production (62 countries) and continents (6 continents).
- **Special Attributes**: Each movie is linked to an IMDB ID, which connects to country data via the OMDB API (http://www.omdbapi.com/).
- **Notes**: Some movies are produced in multiple countries; continent derivation is included.

## 2. Books Dataset (`books.csv`)
- **Filename**: `books.csv`
- **Description**: The items of the Book-Crossing dataset, along with geographical metadata.
- **Contents**: 12,314 books.
- **Geographical Data**: Books are associated with 11 countries and 4 continents.
- **Special Attributes**: Uses ISBN codes for each book to retrieve the production continent via the Global Register of Publishers (https://grp.isbn-international.org/search/piid_cineca_solr).

## 3. Courses Dataset (`courses.csv`)
- **Filename**: `courses.csv`
- **Description**: Contains courses from the educational sector with detailed geographic data of providers.
- **Contents**: Includes 11,454 courses.
- **Geographical Data**: Courses and users are from 71 countries and 6 continents.
- **Special Attributes**: Records geographic provenance of users and time zones of teachers to infer continental affiliations.

## 4. Songs Dataset (`songs.csv`)
- **Filename**: `songs.csv`
- **Description**: The DataSongs dataset, which includes song ratings and artist origin data.
- **Contents**: Contains 1,777,981 ratings, ranging from 1 to 5, by 30,759 users for 16,380 songs.
- **Geographical Data**: Songs are associated with 54 countries and 6 continents.
- **Special Attributes**: Each song includes data on the country and continent of the artist's origin.

### General Notes
- Each CSV file is structured with headers reflecting the descriptions provided.
- Users are advised to handle data responsibly, especially when linking to external APIs or resources.

# CITATION
If you use our source datasets, and experiments for your research or development, please cite the following paper


# CONTACT
If you have any questions, do not hesitate to contact us by david.contreras@salle.url.edu or egomezy109@gmail.com, we will be happy to assist.

