# mantis-resize-journal-cover
It's optimizes and resizes uploaded journal cover images in Mantis Academic products. By default it resizes images to 70x100 pixel and saves them with 65% quality in PNG format. 

## Usage
We suggest that run this script as Kubernetes job. 

**Required environment variables:**
* DB_HOST:  Product's database host
* DB_PORT: Optional. Default: 5432
* DB_USER
* DB_PASS
* DB_DATABASE: Product's database name
* LOG_LEVEL: Optional. Default: DEBUG
* FILE_SERVICE_API_URL: Mantis File Service API base path. Ex: `http://file.myarchive.svc/api/v1`
* COVER_SELECT_SQL_PATH: File/Config path that contains sql for fetching cover images file keys. 

Example sql:
```sql
select * from journal where cover_path_s3 is not null;
```

*     COVER_UPDATE_SQL_PATH: File/Config path that contains sql for updating cover images file keys.

Example sql:
```sql
update journal set cover_path_s3 = %s where cover_path_s3 = %s;
```

*     COVER_DELETE_SQL_PATH: File/Config path that contains sql for removing broken file keys from table.

Example sql:
```sql
update journal set cover_path_s3 = null where cover_path_s3 = %s;
```
