### [<INDEX](https://b19kiit.github.io/OEE_DOCS/)

# Storage Design

## `file_store` Table

| field       | type                                                  |
| --- | ----------- |
| id (PK)     | TEXT < SERVERID + MongoDBObjectId > < LENGTH 6 + 24 > |
| owner_id    | TEXT < MongoDBObjectId >                              |
| time_added  | BIGINT < seconds >                                    |
| time_expire | BIGINT < seconds >                                    |
| buffer      | BLOB                                                  |

### `file_store.id`
This fields can also be called `file_id` as more appropriate term, and its always unique.

Since cassandra can to evaluate constraints, we have to ensure file_id is always unique

|`file_id` = `distribution_config.server_id` +  `MongoObjectId`|

**distribution_config.server_id** Must be uniquely assigned to all file_store server dristibutions during deployment 

### [<INDEX](../)
