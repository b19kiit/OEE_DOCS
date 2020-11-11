# Storing Messages of Chat System

## On DataBase

### `messages` table

| field | type |
| ----- | ---- | 
| _id (PK) | INT UNSIGNED |
| sender_id | VARCHAR(32) |
| receiver_id | VARCHAR(32) |
| sent_at | INT UNSIGNED |
| recived_at | INT UNSIGNED |
| data | MEDIUMBLOB |

- `messages._id`: Stores index of a messages, it primary key of the messages tables. It is the most squen
