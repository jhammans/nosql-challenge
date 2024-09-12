# UK Food Hygiene Rating Analysis

## Project Overview

This project analyzes food hygiene ratings of various establishments across the United Kingdom using data from the UK Food Standards Agency. The project was developed in collaboration with *Eat Safe, Love*, a food magazine, to help their editors, journalists, and food critics decide where to focus future articles based on food hygiene ratings.

The project is broken into three main parts:

1. **Database and Jupyter Notebook Set Up**  
   Set up the MongoDB database using the provided dataset and ensure the data is correctly loaded for analysis.
   
2. **Database Update and Data Cleaning**  
   Modify the database to meet the magazine's requirements, including adding a new restaurant, removing unwanted entries, and converting certain fields into proper formats.
   
3. **Exploratory Data Analysis**  
   Perform various queries and analyses on the data to answer specific questions from *Eat Safe, Love*, such as identifying top-rated restaurants, those with poor hygiene scores, and finding restaurants near a specific location.

---

## Project Structure

The project contains two Jupyter Notebooks:

1. **NoSQL_setup_starter.ipynb**  
   This notebook handles the database setup, data loading, and updates to the data.

2. **NoSQL_analysis_starter.ipynb**  
   This notebook performs the exploratory data analysis required by the magazine, focusing on answering specific questions about food hygiene scores and ratings.

---

## Data Source

The data is provided in the `establishments.json` file, which contains hygiene ratings and information on various establishments in the UK. The data is loaded into a MongoDB database named `uk_food`, with the collection named `establishments`.

---

## Setup Instructions

### Step 1: Clone the repository
```bash
git clone https://github.com/jhammans/nosql-challenge.git
cd nosql-challenge
```

### Step 2: Importing the Data

Before running the notebooks, you must import the data into MongoDB. Use the following command in your terminal to load the data:

```bash
mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json
```

### Step 3: Installing Dependencies

Make sure you have the required Python libraries installed. You can install them using `pip`:

```bash
pip install pymongo pandas
```

### Step 4: Running the Notebooks

- Open the `NoSQL_setup_starter.ipynb` notebook to set up the MongoDB connection, load the data, and perform necessary updates.
- Open the `NoSQL_analysis_starter.ipynb` notebook to perform the exploratory data analysis.

---

## Database Modifications

The following modifications were made to the `establishments` collection based on the magazine's requirements:

1. **Add New Establishment**:  
   A new halal restaurant, *Penang Flavours*, located in Greenwich, was added to the database with the following details:

    ```json
    {
        "BusinessName": "Penang Flavours",
        "BusinessType": "Restaurant/Cafe/Canteen",
        "AddressLine1": "146A Plumstead Rd",
        "LocalAuthorityName": "Greenwich",
        "geocode": {
            "longitude": "0.08384000",
            "latitude": "51.49014200"
        },
        "NewRatingPending": True
    }
    ```

2. **Update BusinessTypeID**:  
   The `BusinessTypeID` for *Penang Flavours* was updated by querying for the appropriate `BusinessTypeID` for restaurants/cafes.

3. **Remove Establishments from Dover**:  
   All establishments in the "Dover" Local Authority were removed from the database.

4. **Convert Data Types**:  
   Some fields were stored as strings and were converted to the correct data types:
   - Latitude and longitude values were converted to decimals.
   - Rating values were converted to integers.

---

## Exploratory Data Analysis

Several key questions were answered to assist *Eat Safe, Love* in finding the best and worst establishments:

1. **Establishments with Hygiene Score Equal to 20**  
   Identify all establishments that have a hygiene score of 20.

2. **Top-Rated Establishments in London**  
   List all establishments in London with a RatingValue of 4 or higher.

3. **Nearest Top-Rated Establishments to Penang Flavours**  
   Find the top 5 establishments near *Penang Flavours* with a `RatingValue` of 5, sorted by lowest hygiene score.

4. **Local Authorities with the Worst Hygiene**  
   Determine how many establishments in each Local Authority have a hygiene score of 0, and sort the results from highest to lowest.

---

## Example Results

Here is an example of one of the analysis outputs, showing the top 5 Local Authorities with the most establishments having a hygiene score of 0:

| _id         | count |
|-------------|-------|
| Thanet      | 1130  |
| Greenwich   | 882   |
| Maidstone   | 713   |
| Newham      | 711   |
| Swale       | 686   |
