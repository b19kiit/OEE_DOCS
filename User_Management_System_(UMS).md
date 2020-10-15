### [<INDEX](https://b19kiit.github.io/OEE_DOCS/)

***

# User Management System (UMS)

## Introduction

UMS is a stateless micro service, developed to enable ThingsGoSocial users to access all the services with single user autorization.

***

## Endpoints

### `api`/`user`/`register`  - **POST**

#### Request:

**Body**

```js
{
    "name": <string>,
    "username": <string>,
    "countryCode": <string> <Numeric String>,
    "phone": <string> <Numeric String>,
    "email": <string> <Email : Regex /^[a-zA-Z0-9+_.-]+@[a-zA-Z0-9.-]+$/>,
    "password": <string>
}
```

#### Response:

- **Success**
    
    **Body**
    ```js
    <UserSchema - Create - Respose>
    ```

- **Errors**

    - `Wrong api key`

        **Header**
        ```
        status: 200
        ```
        **Body**
        ```
        Wrong api key
        ```
        
***

### `api`/`user`/`login`  - **POST**

#### Request:

**Body**
```js
{
    "identifier": <string> <Email : Regex /^[a-zA-Z0-9+_.-]+@[a-zA-Z0-9.-]+$/>,
    "password": <string>,
    "countryCode": <string>
}
```

#### Response:

- **Success**

**Body**
```js
{ 
    "msg": "logged in",
    "user":{
            "userId": <string> <MongoDBObjectID 24-bytes>,
            'username": <string>,
        }
    "token": <string> <JWT Token>
}
```
- **Errors**

    - `Wrong api key`

        **Header**
        ```
        status: 200
        ```
        **Body**
        ```
        Wrong api key
        ```

***

### `api`/`project`  - **POST**

TO add project to any specific user

#### Request:

**Body**
```js
{
    "username": <string>,
    "name": <string>,
    "pid": <string> <MongoDBObjectID 24-bytes>
}
```

#### Response:

**Success**

**Body**
```js
{
    name: <string>,
    pid: <string> <MongoDBObjectID 24-bytes>
}
```

***

### `api`/`sendMail` - **POST**

#### Request:
**Body**
```js
 {
    "replyTo": <string> <Email : Regex /^[a-zA-Z0-9+_.-]+@[a-zA-Z0-9.-]+$/>,
    "to": <string> <Email : Regex /^[a-zA-Z0-9+_.-]+@[a-zA-Z0-9.-]+$/>,
    "subject": <string> <Email : Regex /^[a-zA-Z0-9+_.-]+@[a-zA-Z0-9.-]+$/>,
    "cc": <string> <Email : Regex /^[a-zA-Z0-9+_.-]+@[a-zA-Z0-9.-]+$/>,
    "bcc": <string> <Email : Regex /^[a-zA-Z0-9+_.-]+@[a-zA-Z0-9.-]+$/>,
    "text": <string>,
    "html": <string>,
    "attachments":["?????"]
}
```
#### Response:

**Success**

**body**
```js
<Email Transporter Reponse . info>
```

***

### [<INDEX](https://b19kiit.github.io/OEE_DOCS/)
