# GTFS API
This note file is intended to document the ideas/process for creating a separate server that hosts an api to handle GTFS data requests from the mapnificent app.

I've created another repo to test out a NodeJS server that can connect to Cloud SQL using the mysql driver.

  - https://github.com/vishalbakshi/gtfsapi


## Version 1
Right now this is barebones as I want to setup a basic environment which does the following:
  - [x] Connects to a Google Cloud SQL database 
  - [x] Serves responses using Express
  - [x] Handles queries to the database and sends JSON responses

Reference: https://medium.com/@austinhale/building-a-node-api-with-express-and-google-cloud-sql-9bda260b040f

The test data for this database looks like:

| id | title | author | userId |
| -- | ----- | ------ | ------ |
| 1  |  title0 |author0 | 1 |
| 2  |  title1 |author1 | 1 |
| 3  |  title0 |author0 | 2 |
| 4  |  title1 |author1 | 2 |
| 5  |  title2 |author2 | 2 |
| 6  |  title3 |author3 | 2 |


The app is served on port 3306 and has one GET route `/books/:userId`. In the case of userId = 2, the following GET request URL: 

```https://localhost:3306/books/2"```

returns the following JSON:

```[{"id":3,"title":"title0","author":"author0","userId":"2"},{"id":4,"title":"title1","author":"author1","userId":"2"},{"id":5,"title":"title2","author":"author2","userId":"2"}]```

## Version 2

TBD...

