### [<INDEX](https://b19kiit.github.io/OEE_DOCS/)

# File Store Backend driver

Perform queries on cassandra DB

## Actions:-

### SetFile class

#### ` SetFile.insert_new_file `

> This funtion generates primarykey for the file, and stores it on the database

> ***Arguments***:
>  - `buffer`           : `<Buffer>`
>  - `_owner_id`        : `<string ><MongodbOjectId String>`
>  - `life_time_seconds`: `<number><time in seconds>`

> ***Return***
> `Promise`
  - On Resolve : 
  ```js
  {
    file_id, // <string>
    owner_id, // <string>
    time_added, // <number><UNIX epoch time in seconds>
    time_expire // <number><UNIX epoch time in seconds>
  }
  ```
  - On Error :
  ```js
  <Error>
  ```



### [<INDEX](https://b19kiit.github.io/OEE_DOCS/)
