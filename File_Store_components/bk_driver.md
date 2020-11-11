### [<INDEX](../)

# File Store Backend driver

Perform queries on cassandra DB

## Actions:-

### SetFile class

#### ` SetFile.insert_new_file `

> This funtion generates primarykey for the file, and stores it on the database

> ***Arguments***:
>  - `buffer`           : `<Buffer>`
>  - `_owner_id`        : `<string><MongodbOjectId asString>`
>  - `life_time_seconds`: `<number><time in seconds>`

> ***Return***
> `Promise`
>  - On Resolve : 
  
```js
{
  file_id, // <string>
  owner_id, // <string>
  time_added, // <number><UNIX epoch time in seconds>
  time_expire // <number><UNIX epoch time in seconds>
}
```
>  - On Error :
  
```js
<Error>
```

#### ` expire_file_as_owner_safe `

> ***Arguments***:
>  - `_owner_id`       : `<string ><MongodbOjectId asString>`
>  - `_file_id`        : `<string>`

> ***Return***
> `Promise`
>  - On Resolve : 

> `Promise`
>  - On Resolve : 
  
```js
  achievedConsistency // Number
```
>  - On Error :
  
```js
<Error>
```

#### ` expire_file_as_public_safe `

> ***Arguments***:
>  - `_file_id`        : `<string>`

> ***Return***
> `Promise`
>  - On Resolve : 
```js
  achievedConsistency // Number
```
>  - On Error :
  
```js
<Error>
```

### [<INDEX](../)
