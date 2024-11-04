# Datasets Overview

This repository contains four enriched datasets with geographical metadata for analysis in various domains. Each dataset is provided as a CSV file with detailed attributes relevant to its specific context.

## How to

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
