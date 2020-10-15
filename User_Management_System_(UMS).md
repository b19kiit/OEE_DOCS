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
    "email": <string> <Regex /^[a-zA-Z0-9+_.-]+@[a-zA-Z0-9.-]+$/>,
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
