# GTFS API
This note file is intended to document the ideas/process for creating a separate server that hosts an api to handle GTFS data requests from the mapnificent app.

I've created another repo to test out a NodeJS server that can connect to Cloud SQL using the mysql driver.

  - https://github.com/vishalbakshi/gtfsapi

Right now this is barebones as I want to setup a basic environment which does the following:
  [x] Connects to a Google Cloud SQL database 
  [x] Serves responses using Express
  [x] Handles queries to the database and sends JSON responses

The test data for this database looks like:


