##### [<INDEX](https://b19kiit.github.io/OEE_DOCS/)

# User Management System (UMS)

## Introduction

UMS is a stateless micro service, developed to enable ThingsGoSocial users to access all the services with single user autorization.

## Endpoints

### `api`/`user`/`register`

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

**Body**

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
        
### `api`/`user`/`login`

#### Request:

```js
{
    "identifier": <string> <Email : Regex /^[a-zA-Z0-9+_.-]+@[a-zA-Z0-9.-]+$/>,
    "password": <string>,
    "countryCode": <string>
}
```

#### Response:

- **Success**

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
