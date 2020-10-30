### [<INDEX](https://b19kiit.github.io/OEE_DOCS/)

# OEE_Search

Oee search is search system built to perform search on TGS SmartFactory, this system is Micro Service of SmartFactory.

Oee Search come with a front end driver built on socket.io, with 'websocket' transport to initaiate a continous connection with the OEE_Search server.

[Repo: Backend End Source Code](https://bitbucket.org/rishavbhowmiktgs/oee-search/src/master/)

[Repo: Front End Driver](https://bitbucket.org/rishavbhowmiktgs/oee-search-driver/src/master/)

## OEE_Search Backend

### Deployment Guide

#### > Arragement of folder
```
// crucial componets that must be present during execution
+--- 📁 private               (The file should not be accessable by any other entity other than OEE Search)
+------ 📄 manifest.json      (ALTERABLE, may need creation/alteration prior to execution)
+--- 📁 oee-search
+------ 📄 manifest.json      (ALTER ONLY WHEN NECESSARY)
+------ 📄 package.json       (ALTER ONLY WHEN NECESSARY)
+------ 📄 server.js          (Server's starting point)
+------ 📁 search
```
#### > Setup

- Important manifest files:

  - **`private/manifest.json`** : This file stores username, password & host_name of mongoDB database of OEE
    ```json
    {
      "mongodb": {
        "username": "<username>",
        "password": "<password>",
        "host": "119.81.0.44:27017"
      }
      "User_Token_Key":"<JWT TOKEN key><optional>",
      "Organisation_Token_Key":"<JWT TOKEN key><optional>"
    }
    ```
  - **`oee-search/manifest`** : This file stores mongodb_uri template, mongodb_connection_options ('mongodbOptions') and **oee_ui_host's url**
    ```json
    {
      "port": "8393",
      "mongodb_uri": "mongodb://<username>:<password>@<host>/oee?authSource=admin",
      "mongodbOptions": {
        "useNewUrlParser": true,
        "useUnifiedTopology": true
      },
      "oee_ui_host": "http://smartfactory.thingsgosocial.com/"
    }
    ```
- To integrate JSON webtoken
  - Perform required modifications in json `private/manifest.json`
  
  - Execute `npm i jsonwebtoken`
  
  - Alter `line No: 16` in `oee-search/server.js` with this code
  ```js
  data = Object.assign(
      (require('jsonwebtoken')).verify(data.user_token, (require("../private/manifest.json"))['User_Token_Key'] ),
      (require('jsonwebtoken')).verify(data.org_token, (require("../private/manifest.json"))['Organisation_Token_Key'] )
    )
   //whatever you do make sure the 'if' condition below (in line 17) is NOT satisfied, when the request is valid
  ```
  
  - Alterations in OEE Search Driver [Repo: Front End Driver](https://bitbucket.org/rishavbhowmiktgs/oee-search-driver/src/master/)
  ```
  - Alter constructor of class 'OEESearch'
  - Replace this.use_id & this.org_id with their JWT TOKENS of user_id & org_id respectively over raw user_id & org_id
  - Replace line which currently has 
      {user_id:this_class.use_id, organisation_id:this_class.org_id}
      with
      {user_token:this_class.use_id, org_token:this_class.org_id}
  ```

Vola, JWT Token integrated :-)

### [<INDEX](https://b19kiit.github.io/OEE_DOCS/)
