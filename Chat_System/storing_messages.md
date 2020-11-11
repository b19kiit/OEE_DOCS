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

- `messages._id`: Stores index of a messages, it primary key of the messages tables. It is the most squential field of the messages

- `messages.data`: This is blob, which stores buffer data of message lines.

Chat lines is tured to buffer using net_FM request enscapsulation protocol.

```js
header : { 
    time : <Number><UNIX epoch time in seconds>,
    buffer_map : <Array>< [ Number ] >, //size of each chat line
  }
body : <Buffer> < [ {ChatLines} ] >
```
