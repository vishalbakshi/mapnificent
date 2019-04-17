# Notes - List Of Data Conversion Methods - 20190415

The purpose of this note is to track the progress/learnings associated with converting data between different file formats and structures.

Currently we may be dealing with the following types of data:

  - delimited file (txt, csv, etc. from SQL query results)
  - .bin file (current choice of format in mapnificent)
  - .zip file (as received from transitfeeds GTFS feed)
  - Cloud SQL database records
  - Google Cloud/Firebase Storage buckets/objects
  - Firebase Firestore or Realtime Database documents/collections
  - Protocol Buffers (not sure if it's worth seeing this as a separate data type or as part of the binary file streaming process)
  
## Conversions
  
Here's the current progress on conversions between the different data types:
  
### .zip to Google Cloud Storage
  - Yet Another UnZipping Library: https://www.npmjs.com/package/yauzl
  - Uploading Objects to Google Cloud Storage: https://cloud.google.com/storage/docs/uploading-objects#storage-upload-object-nodejs
  - IAM Permissions: https://cloud.google.com/storage/docs/access-control/using-iam-permissions
      
### .zip (or directory) to .bin
  - Mapnificent Generator: https://github.com/vishalbakshi/mapnificent_generator
  - **You can perform the conversion with a single file (magnificent.go)**
    - https://github.com/vishalbakshi/mapnificent_generator/blob/master/mapnificent.go
    - `go run mapnificent.go -d <folder containing gtfs files> -o <destination file>`

### delimited file to Cloud SQL
  - WIP


### delimited file to Firestore/Realtime Database
  - WIP
  
### .bin to Protocol Buffers
  - I believe this is taken care of inside of Mapnificent by `mapnificent.js`: https://github.com/vishalbakshi/mapnificent/blob/master/static/js/mapnificent.js#L391-L433
