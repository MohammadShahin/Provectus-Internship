# Level 1

## Files definitions:

* src_data - Path with source data needed to be processed.
* processed_data - Path with output processed data.
* user_id.jpg - User image file, for example, 0001.jpg. Could be several for different users in source data path.
* user_id.csv - User info file, for example, 0001.csv. Could be several for different users in source data path.

User csv file contains next columns:

* first_name - User first name
* last_name - User last name
* birthts - User birthdate timestamp in milliseconds UTC

Test csv and img files could be found in the 02-src-data folder

For example:

    first_name, last_name, birthts
    Ivan, Ivanov, 946674000000

Data processing description

1. Read csv file

2. Match images for each user

3. Combine data from CSV and image path

4. Update processed_data/output.csv CSV file and add new data. Important we can update data for previously processed user. In output CSV and DB we should not duplicate records. Output CSV file format: user_id, first_name, last_name, birthts, img_path

<hr>

## Task

Implement a script to process files from the src_data folder.

<hr>

## Results delivery format

Results should be implemented as a python script with demo data. Also should be provided the README.md file with the description of your solution.
  
<hr>

# Level 2

The same as Level 1 with the following extras.
  
 <hr> 
 
## Results delivery format

Results should be implemented as a service. The service should periodically read source data and process it. Also, the service should implement web server with next endpoints:

    GET /data - get all records from DB in JSON format. Need to implement filtering by: is_image_exists = True/False, user min_age and max_age in years.
    POST /data - manually run data processing in src_data

Should be provided the README.md file with the description of your solution.

      
# Level 3

The same as Level 2 but with next differences.

## Files definitions:

Source data and processed data should store in Minio. Minio service already defined in docker-compose file.

## Data processing description

1. Read csv file

2. Match images for each user

3. Combine data from CSV and image path

4. Update processed_data/output.csv CSV file and add new data. Important we can update data for previously processed user. In output CSV and DB we should not to duplicate records. Output CSV file format: user_id, first_name, last_name, birthts, img_path

5. Write this combined data to DB. Record should contain next columns: id, user_id, first_name, last_name, birthdate, img_path. id - autoincrement unique record id. Postgres DB service already defined in docker-compose

## Results delivery format

Results should be implemented as a service. The service should periodically read source data and process it. Also, the service should implement web server with next endpoints:

    GET /data - get all records from DB in JSON format. Need to implement filtering by: is_image_exists = True/False, user min_age and max_age in years.
    POST /data - manually run data processing in src_data

The solution should work in docker-compose. As base template can be taken docker-compose file.
