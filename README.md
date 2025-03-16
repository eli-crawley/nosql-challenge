# MongoDB Food Establishments Analysis
## Project Overview
This project allows you to analyze food establishment data stored in MongoDB. It provides insights such as finding establishments with specific ratings, hygiene scores, or local authority areas. The main tasks include querying MongoDB using the pymongo library and performing analysis using Python and Pandas.

## Prerequisites
To run this project, you will need:

* MongoDB: Make sure you have MongoDB installed and running on your local machine or a remote server.
* Python 3: Python 3.x installed on your system.
* Required Python Libraries:
    * pymongo: MongoDB client for Python.
    * pandas: Data analysis library.

## Setup Instructions
1. Clone the Repository (if applicable): Clone this repository to your local machine:

```
git clone <repository_url>
cd <repository_directory>
```

2. MongoDB Database Setup: Ensure you have MongoDB running. 

3. Database Import: Import your JSON data (establishments.json) into MongoDB using the following command:

```
mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json
```

4. Run the Python Scripts: After setting up MongoDB and installing the necessary dependencies, you can run the Python scripts for querying and analysis.

## Functions and Queries
1. Insert New Restaurant - 
Adds a new restaurant document to the establishments collection.
Provides fields like BusinessName, BusinessType, PostCode, and RatingValue.
2. Find Establishments by Rating - 
Query establishments based on specific rating values.
For example, find establishments with a rating value of 5.
3. Aggregation for Hygiene Score of 0 - 
Finds how many establishments in each Local Authority area have a hygiene score of 0.
Sorts the results from the highest to lowest count.
Example MongoDB Aggregation Pipeline:

```
pipeline = [
    {"$match": {"scores.Hygiene": 0}},
    {"$group": {"_id": "$LocalAuthorityName", "count": {"$sum": 1}}},
    {"$sort": {"count": -1}}
]
```

4. Find Establishments Near "Penang Flavours" - 
Finds the top 5 establishments with a RatingValue of 5 near a specific latitude and longitude.
Filters establishments within a 0.01 degree range and sorts them by hygiene score.
5. Convert Results to Pandas DataFrame - 
The MongoDB query results are converted to a Pandas DataFrame for further analysis and visualization.
Example:

```
df = pd.DataFrame(results_list)
print(df.head(5))
```
MongoDB Queries Used
1. Find Documents by Rating Value
MongoDB Query: find({"RatingValue": 5})
2. Group and Count by Local Authority Name
MongoDB Aggregation Pipeline to find establishments with hygiene score 0, grouped by LocalAuthorityName and sorted by count.
3. Proximity Search for Establishments
MongoDB Query: Using latitude and longitude filtering within a given range (e.g., 0.01 degrees).

## References
* UK Food Standards AgencyLinks to an external site. (2022). UK food hygiene rating data API. https://ratings.food.gov.uk/open-data/en-GB. Contains public sector information licensed under the Open Government Licence v3.0Links to an external site.
Accessed Sept 9, 2022 and Sept 12, 2022 with the establishment settings as follows: longitude=51.5072, latitude=-0.1276, maxdistancelimit=4567, pagesize=10000, sortoptionkey=distance, pagenumber=(1,2,3,4,5,6,7,8).

